# Authorization Process

## Authorization Process Overview

The Authorization Process is an important step throughout your [Beefree SDK installation process](./). This step validates your Beefree SDK credentials and provides you with a token. Take the steps outlined in this document to ensure you accurately complete the authorization process.&#x20;

### Beefree SDK NPM Package

Prior to getting started with the authorization process, ensure you reference the [Beefree SDK official npm package](https://www.npmjs.com/package/@beefree.io/sdk). Reference both the [wrapper](https://www.npmjs.com/package/@beefree.io/sdk) and the [GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-npm-official) to get the latest information. &#x20;

#### **Package Installation**

You can install Beefree SDK using either [npm](https://www.npmjs.com/package/@beefree.io/sdk) or [yarn](https://yarnpkg.com/):

**Using npm**

```bash
npm install @beefree.io/sdk
```

**Using Yarn**

```bash
yarn add @beefree.io/sdk
```

**Package Details:**

* TypeScript Support: Included
* License: Apache-2.0
* Repository: [Beefree SDK GitHub](https://github.com/BeefreeSDK/beefree-sdk-npm-official)

### Beefree SDK Client-side Configuration

Beefree SDK requires the host application to pass a container parameter in the [client-side configuration.](configuration-parameters/) This is the only required parameters for the configuration.

The following code sample shows an example of this parameter in the [client-side configuration](configuration-parameters/).

```javascript
var config = {
    container: 'string'
}
```

### Beefree SDK Server-side Login

To initialize your instance of the Beefree SDK builder, call the `/loginV2` endpoint shown in the sample code below with your Client ID, Client Secret, and UID. The Client ID and Secret are available on the application details page of the [Beefree SDK developer portal](https://dam.beefree.io/devportal). UID represents your user as described in [How the UID parameter works](https://docs.beefree.io/how-the-uid-parameter-works/).

{% hint style="danger" %}
**Important:** Do not put your Beefree SDK credentials in client-side code.
{% endhint %}

The Beefree SDK system uses [OAuth2 as the authorization framework](https://auth0.com/docs/authenticate/protocols/oauth).

#### Example

```http
POST /loginV2 HTTP/1.1
Host: auth.getbee.io
Accept: application/json
Content-Type: application/json
{
“client_id”: YOUR_CLIENT_ID,
“client_secret”: YOUR_CLIENT_SECRET,
“uid”: uid of choice
}
```

Reference [How the UID parameter works](how-the-uid-parameter-works.md) to learn more about UID.

The following code sample displays an example JSON response.

```json
{
    "access_token": "...",
    "v2": true
}
```

The Beefree SDK authorization service will return a temporary access token if the authentication is successful. The client application can use the full response that contains the token to start or refresh a Beefree SDK session.

The token expires after 5 minutes for security reasons. Beefree SDK will refresh an expired token automatically for 12 hours without re-authenticating the application. Beefree SDK will trigger the `onError` callback when the token can't be refreshed automatically.

{% hint style="info" %}
**Note:** When a refreshable token expires, Beefree SDK receives a [401 error](../../../resources/error-management/json-parser-errors.md#authentication-errors) and attempts to refresh it automatically. 401 errors are expected and part of the process.
{% endhint %}

You can reference `/loginV2` examples in the following Quickstart Guides:

* [React](../../../quickstart-guides/react-no-code-email-builder.md)
* [Vue](../../../quickstart-guides/vue.js-no-code-email-builder.md)
* [Angular](../../../quickstart-guides/angular-no-code-email-builder.md)

Ensure to call the authorization endpoint server-side to protect your credentials.

Once you obtain the token, the [configuration parameters](https://docs.beefree.io/configuration-parameters/) object is passed to Beefree SDK to set up your customization options, for example setting the editor’s language to “Spanish”.

Then, you can use Beefree SDK methods to [start your instance and display the editor](./) on your page.

Beefree SDK will keep this session alive for 12 hours from the login. After 12 hours, you have to manage the token expiration, as follows:

1. Obtain a new token via the new authorization endpoint.
2. Inject the token obtained from step one via the `updateToken` method. Reference examples of this in the following section.

The following code example shows how to inject the token in the current Beefree SDK instance:

```json
// obtain a new token with a new LoginV2 call
// update the token in the current Beefree SDK instance
beeInstance.updateToken(token);
```

## Error Management

When you set up an [`onError` callback](../../../resources/error-management/warning-error-info-callbacks.md#onerror-callback) you will get the `error` object as a parameter.

From that object, you can grab the `code` property and use it as explained in the table below.

| Code | Message                           | Detail                                                                                                                                                                                                                                                                                       |
| ---- | --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 5101 | Expired token cannot be refreshed | You need to do a new login and update the token in the current Builder instance using `updateToken` method.                                                                                                                                                                                  |
| 5102 | Expired token must be refreshed   | <p>You need to do a new login and create a new Builder instance using the new token, and the current JSON template present in this event<br></p><p>Example scenarios:</p><ul><li>The version is outdated</li><li>Beefree SDK releases a security fix and every client must refresh</li></ul> |

## Error Responses

Example error response for unsupported media type Only `Content-Type: application/json` is allowed.

```json
{
  "code": 5001,
  "message": "Unsupported media type 'application/x-www-form-urlencoded'",
  "status_code": 415
}
```

Example error response for an invalid UID. Look at the properties of [UID parameter](how-the-uid-parameter-works.md).

```json
{
  "code": 5005,
  "message": "Invalid UID",
  "status_code": 400
}

```

Example error response for invalid credentials. Obtain your credentials using the [authorization process](authorization-process-in-detail.md).&#x20;

```json
{
  "code": 5002,
  "message": "Unable to authenticate with provided credentials.",
  "status_code": 401
}
```

Example error response for disabled apps. Contact support if you encounter this error.

```json
{
  "code": 5003,
  "message": "Application is disabled.",
  "status_code": 403
}

```
