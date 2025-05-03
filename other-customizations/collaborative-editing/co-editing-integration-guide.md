# Co-editing Integration Guide

## Introduction

The following is the recommended method to integrate with the co-editing feature. Using a row-level database lock during the operation will help prevent race conditions, like opening different co-edit sessions for the same message at the same time.

### Start or Join Session

The following must be performed as a single backend operation.

1. Check the database to find if there is already a saved session ID
2. If so, call the API using the session ID. View the API documentation for Authentication details

```http
GET /v1/coedit/session/{id}
Authorization: Bearer {token}
```

Response body:

```
{
    "template": {
        "page": {...},
        "comments": {}
    },
    "users": {
        "test": {
            "userId": "test",
            "username": "test",
            "userColor": "#c0ffee"
        }
    }
}
```

3. Parse the response JSON:
   * If session exists, check the total number of users
   * If session not exist, there will be a 404
   * If there are no users in an active session or the session does not exist, then create a new session

{% hint style="info" %}
**Note:** When creating a session, you'll pass the latest saved version of the JSON.
{% endhint %}

```http
POST /v1/coedit/session
```

Request body:

```json
{
  "template": { //… latest JSON here },
  "userid": "string"
}
```

Response body:

```json
{
  "historyEntry": {
    "version": 1,
    "timestamp": "2024-08-28T23:43:24.445Z",
    "changeId": "string",
    "label": "string",
    "type": "string",
    "userId": "string",
    "diff": []
  },
  "sessionId": "string",
  "template": {
    "page": {},
    "comments": {}
  }
}
```

4. Now join the user to the session using the old or new session ID (depending on the outcome of #3)
5. Save the new session ID in the database for this template

### Versioning and onChange

Learn more about Tracking Changes and Versioning in the [Tracking Changes technical documentation page](../../getting-started/tracking-message-changes.md).

A key concept outlined in the documentation above is that each template has an incremental version number: 1, 2, 3, and so on. This version acts as a simple integration counter.

However, the version number in the onChange callback may not always match what you expect. For example, if two users make changes at the same time, the version number passed to each user's onChange callback might be the same. This is because the callback fires immediately and reflects the version the change was made on. At that point, the next version hasn't been assigned yet. Both changes will race to the backend, where they'll be merged into the master template and assigned a new version number.

If you're saving based on the onChange callback, be sure to review the recommendations in the following section.

### Saving

1. User makes a change in SDK frontend UI.
2. The onChange event is triggered and returns the JSON and version #
3. The host app checks whether the version # is greater than or equal to the previous version. (see special cases #3)
4. If the version is greater than or equal, then the host app will save the JSON to the database.

### Special Cases

* Every page change should have a new version #. If the host app receives multiple onChange events with the same version #, then it could signal a network error occurred during the session, and the user's changes are being synchronized with other users. The host app may refresh that user's session to establish a new WebSocket connection.
* If error 5100 is received, the session does not exist. The user will need to start a new session from the last save point.
  * If this occurs at login, then it's likely that the session expired, it's the wrong sessionId, or it's a race condition.
  * If this occurs during a session, then it's likely the internet was disconnected for more than 5 minutes.
* When saving using the onChange callback, there may be a case where you don't want to save versions that are greater than or equal to the current one, which is typically when the user is browsing through the history. When there is only one user in the session, the history feature is available. When changing the history, a new version is not created, but the onChange event is triggered. The choice is up to the host application, which behavior you want to support. If you'd like to skip auto-saving while the user is browsing the history but has not committed to the change, you can check for the onChange event code 1609. Once the user commits to reverting to a previous version permanently by initiating another change or exiting the app, you can then save the change in the host app.
