# Collaborative Editing



1. [Overview](broken-reference)
2. [Use cases](broken-reference)
3. [Availability](broken-reference)
4. [How it works](broken-reference)
5. [Join a session](broken-reference)
6. [Monitor a session](broken-reference)
7. [Usage Limitations](broken-reference)
8. [Versioning](broken-reference)
9. [Custom Languages](broken-reference)
10. [Session lifecycle and error codes](broken-reference)

### Overview <a href="#overview" id="overview"></a>

With **Co-editing**, multiple users can **work on the same asset (email, page or popup) simultaneously**. Co-editors can see what each other is doing, as their changes are synced to the stage in real-time.

![Co-editing avatars](https://docs.beefree.io/wp-content/uploads/2020/11/Co-editing-avatars.png)

Each user is represented by a round icon with the initial of the user, and hovering the mouse on the icon will show the full name for that user.

When a user selects a row or a content block, other co-editors will see it highlighted with that user’s color. To avoid conflicting edits, only one user at a time can edit a row or block. A feedback message will guide users when this situation happens.

![Content locked by another user](https://docs.beefree.io/wp-content/uploads/2020/11/Content-locked-by-another-user.gif)

### Use cases <a href="#use-cases" id="use-cases"></a>

In many companies, it’s rare that someone works alone on everything related to an email and or a landing page. Your customers may have **multiple people sharing duties** – copywriting, designing, testing, reviewing, etc. That is why SaaS applications typically offer additional users or seats, so that more people can log into an account at the same time and collaborate.

When multiple people collaborate on creating content, co-editing is the logical solution for an **authentic teamwork experience**, **Google-doc style**.

![Co-editing + Commenting](https://docs.beefree.io/wp-content/uploads/2020/11/coediting\_min.gif)

If you add [**Commenting**](https://docs.beefree.io/commenting/) to the mix, Beefree SDK becomes an **all-around, real-time, collaborative content creation platform** to design and review emails, landing pages, and popups, unifying your customers’ workflow under one roof.

### Availability <a href="#availability" id="availability"></a>

Co-editing is available for Beefree SDK [Superpowers](https://dam.beefree.io/pluginpricing) and [**Enterprise**](https://dam.beefree.io/pluginpricing) plans:

* Superpowers plans are limited to a maximum of **5 co-editors per session**.
* **Enterprise** plans are limited to a maximum of **20 co-editors per session.**

This means that on the Superpowers plan, **no more than 5 users can edit the same email or web page** simultaneously. Your application will only receive an error code from the Beefree platform when the limit is reached and the editor will not load – you’ll need to add a user notification to let them know they cannot join the editing session (e.g. “Sorry, you cannot edit this message because you’ve reached the limit of 5 co-editors, try again later”).

Even better, you can [monitor sessions](broken-reference) and disable editing for an email or landing page once the limit is reached.

### How it works <a href="#how-it-works" id="how-it-works"></a>

Creating a co-edit session is nearly identical to starting a traditional, single-user session of your Beefree application. You simply need to pass a shared flag, indicating the template is sharable, along with some simple user settings.

**User settings**

The following parameters are all required.

| Description | Type   | Value                         |
| ----------- | ------ | ----------------------------- |
| username    | string | The user’s display name       |
| userColor   | string | Hex color code (e.g. #FFFFFF) |

**Example beeConfig:**

```


var config = {
  uid: '1234', 
  ...
  username: 'Jane Doe', 
  userColor: 'black',
  ...
}


```

**Options**

The following shared parameter is required to start a co-editing session.

| Description | Type    | Value         |
| ----------- | ------- | ------------- |
| shared      | boolean | true or false |

You pass this argument in the start instance method’s options parameter.

**Example instance method when not using co-editing:**

```


bee.start(template)


```

**Example instance method with co-editing enabled:**

```


bee.start(template, { shared: true })


```

**Session started callback**

Once the session is started, a globally unique id will be created and returned to the host application via the onSessionStarted callback. The host application will save this session id, and use it when users want to join the same session.

| Description | Type   | Value                                                   |
| ----------- | ------ | ------------------------------------------------------- |
| sessionId   | string | globally unique id saved from onSessionStarted callback |

**Example callback handler:**

```


onSessionStarted: function(sessionInfo) {
  console.log('*** [integration] --> (onSessionStarted) ', sessionInfo)
  prompt('press ctrl+c to copy the session ID', sessionInfo.sessionId)
}


```

#### Join a session <a href="#join-a-session" id="join-a-session"></a>

The host application can add a user to any active co-edit session by using the new join instance method. The join method replaces the bee.start method and accepts the session id as a parameter, and loads the current template directly from the active session.

```


bee.join(sessionId)


```

#### Monitor a session <a href="#monitor-a-session" id="monitor-a-session"></a>

Once the session is started, all changes to the session are reported to the onSessionChange callback. The host application can monitor this callback to understand the session’s status.

| Description | Type   | Value                                                                        |
| ----------- | ------ | ---------------------------------------------------------------------------- |
| change      | object | An object containing the type of change and a value containing more details. |
| sessionData | object | An object containing useful session data, such as a list of users.           |

**Example return JSON:**

```


{
  change: { 
    type: "USER_JOINED", 
    value: {
      username: "John Doe", 
      userColor: "#c0ffee" 
      userId: "johndoe"
    }
  },
  sessionData: {
    users: {
      668bf8aa-97b9-4f5d-80a2-dc3e0986a370: { 
        userId: "johndoe", 
        username: "John Doe", 
        userColor: "#c0ffee" 
      },
      ...
    }
  }
}


```

**Example onSessionChange handler:**

```


onSessionChange: function(data) {
  console.log('*** [integration] --> (onSessionChange) ', data)
}


```

**Use cases to monitor a session**

* Only display a “join” button when a session is active
* Display a “edit” session only if there is at least one free co-editing spot (see [Availability](broken-reference))
* Know when someone logs on or logs off, and notify other users in the host application
* Know when the session contains only a single user, so the user knows it’s safe to send a campaign

#### Usage Limitations <a href="#usage-limitations" id="usage-limitations"></a>

There are some limitations set for the Co-editing feature to preserve the integrity of the experience. These are:

* Undo/redo:  If only a single user is present in the co-editing session at any given time, undo/redo will function the same as in a normal session. When a second user is present, undo/redo will be limited to only allow changes while the content or row is locked, and users cannot undo the changes of other users or those that have been synchronized across all sessions.
* Load/reload:  The host application cannot trigger any action that overwrites the user’s changes.
* Autosave: The autosave timer is set on the instance that started the session; it’s not recommended for co-editing sessions.
* onChange:  The onChange callback occurs only for the user that makes the change. For example, if user A makes a change, the onChange event fires only for their instance, and user B won’t receive the notification.

### Versioning <a href="#versioning" id="versioning"></a>

During the co-edit session, the host application may receive callbacks for saving JSON and HTML. However, with multiple users editing the content, potentially all over the world, the host application needs to confirm which changes are new vs. old. For this reason, a new version parameter has been added to all of the callbacks that return JSON or HTML.

The version is a simple integration counter: 1, 2, 3, …

**New onSave callback handler:**

```


onSave: function(jsonFile, htmlFile, version) {
   console.log(`*** [integration] (onSave) version ${version}, ${new Date().toISOString()}`);
},


```

**New onSaveAsTemplate callback handler:**

```


onSaveAsTemplate: function(jsonFile, version) {
   console.log(`*** [integration] (onSaveAsTemplate) version ${version}, ${new Date().toISOString()}`);
},


```

**New onSend callback handler:**

```


onSend: function(htmlFile, version) {
   console.log(`*** [integration] (onSend) version ${version}, ${new Date().toISOString()}`);
},


```

### Custom Languages <a href="#custom-languages" id="custom-languages"></a>

You may override any of the default language strings using [custom translations](https://docs.beefree.io/custom-languages/).  The code block below contains the JSON required to replace all co-editing strings.

```

translations: {
  "mailup-bee-newsletter-collaboration": {
    "locked-module-warning-message": "This module is being edited by another user and therefore its content cannot be edited.",
    "locked-module-warning-title": "This module is locked",
    "locked-row-warning-message": "This row is being edited by another user and therefore its content cannot be edited.",
    "locked-row-warning-title": "This row is locked",
    "row-delete-confirm-title": "Are you sure you want to delete this row?",
    "row-delete-confirm-message": "Another user is currently editing a module inside this row. By deleting it, you might cause their work to be lost.",
    "lock-rejected-title": "Element was locked by another user.",
    "lock-rejected-message": "The element is currently being edited by another user. Please wait until they are finished with their changes."
  }
},

```

### Session lifecycle and error codes <a href="#session-lifecycle-and-error-codes" id="session-lifecycle-and-error-codes"></a>

**Heartbeat**

Both the server and client regularly check the connection using the “ping-pong” heartbeat.&#x20;

If the client misses 5 consecutive pings (ping is emitted every 10s), the server considers the connection to be lost and disconnects the client.

If the server misses 5 consecutive pings (also every 10s), the client considers the connection to be lost and will attempt to _reconnect_ (see below).

**Reconnect mechanism**

If the server disconnects without reason (the disconnection is not _clean_), or it misses 5 consecutive pings, the client will attempt to reconnect to the session. It will keep trying for the 60s before emitting an error with code 5400.

Reconnect mechanism is also employed after certain recoverable errors, specifically 5001, 5100 and 5300. The error itself is only emitted if the reconnect fails.

The server will wait for 60s after the last user of the session disconnects (or the connection is lost) before erasing the session data.

**Error state**

During reconnecting, the builder is covered with an overlay to prevent the user from doing any changes (since they cannot be synchronized). This overlay also appears if the server has missed a ping.

In case of error, another overlay modal is displayed to prevent the user from interacting with the builders in an error state. The host application should handle the errors and restart the Beefree application.

**Error codes**

You can monitor the onError callback to know when a problem occurs, and then alert users of the problem.  For example, if a user loses internet connection, you can display an alert in the host application to let them know their changes have not been saved.

Here is the full list of error codes that can be returned for Co-editing.

| Code   | Message                                            | Details                                                                                              | Is recoverable? |
| ------ | -------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | --------------- |
| `5001` | Unexpected error occurred during co-editing.       | General error.                                                                                       | Yes             |
| `5100` | Failed to open co-editing session.                 | Unexpected error when creating/joining a co-editing session.                                         | Yes             |
| `5150` | Session does not exist.                            | The client attempted to join a non-existing (or expired) session.                                    | No              |
| `5200` | Failed to synchronize changes.                     | Emitted if an unexpected error occurs on the server during the real-time synchronization of changes. | No              |
| `5300` | Connection to the synchronization server was lost. | The server closed the connection. Reason is given in the detail field.                               | Yes             |
| `5400` | Connection to the synchronization server was lost. | Caused by network connection error or the server unexpectedly dying.                                 | No              |
| `5500` | Co-editing is not supported for your current plan. | If the client attempts to initiate or join a co-editing session with a lower plan.                   | No              |
| `5600` | Co-editing server is not available.                | Please try again later.                                                                              | No              |
