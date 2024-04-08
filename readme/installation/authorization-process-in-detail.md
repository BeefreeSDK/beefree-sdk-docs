# Authorization v2 Process

## Auth v2 Overview

BEE Plugin Authorization v2 is nearly the same as v1, with an improved endpoint and an extra security layer.\
\
We moved the uid from the client-side to the server-side. Additionally, the automatic token refreshing expires, but the host app can “keep alive” the token for 12 hours, as long as the user is active.

### BEE Plugin Client-side Configuration

Currently, BEE Plugin requires the host application to pass a uid parameter.

```javascript
var config = {
    uid: 'string,'
    container: 'string'
}
```

In Auth v2, the host app will remove the uid from the client-side configuration and pass it during the server-side login request.

#### Example

<div align="left">

<figure><img src="../../.gitbook/assets/CleanShot 2024-04-08 at 16.26.19.png" alt=""><figcaption></figcaption></figure>

</div>

### BEE Plugin Server-side Login

To initialize your instance of the BEE editor, call the “loginV2” endpoint shown in the sample code below with your Client ID, Client Secret, and UID. The Client ID and Secret are available on the application details page of the [BEE Plugin developer portal](https://dam.beefree.io/devportal). UID represents your user as described in [How the UID parameter works](https://docs.beefree.io/how-the-uid-parameter-works/).

The BEE Plugin system uses OAuth2 as the authorization framework.

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

{% hint style="info" %}
We strongly suggest not to put your BEE credentials in client-side code - they are specific to your account and could be easily read and used by other people.
{% endhint %}

The BEE Plugin authorization service will return a temporary access token if the authentication is successful. The client application can use the full response that contains the token to start or refresh a Bee Plugin session.

{% hint style="info" %}
The token you receive from the authorization server should be passed to the BeePlugin.create(...) as it is. We strongly suggest not altering it in any way. Also, don’t rely on the token response's content or structure. If you do, any change to the schema could make your integration stop working.
{% endhint %}

The token expires after 5 minutes for security reasons. BEE Plugin will refresh an expired token automatically for 12 hours without re-authenticating the application. The Plugin will trigger the onError callback when the token cannot be refreshed automatically.

{% hint style="info" %}
**NOTE:** When a refreshable token expires, the plugin receives a 401 error and attempts to refresh it automatically. The 401 errors are nothing to worry about as they are part of this process.
{% endhint %}

Here is an example of how to call the BEE Plugin endpoint, obtain a token and then start the plugin:

```javascript
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
  if (req.readyState === 4 && req.status === 200) {
    // Obtain token
    var token = req.responseText;
    // Call create method and pass token and beeConfig to obtain an instance of BEE Plugin
    BeePlugin.create(token, beeConfig, function(beePluginInstance) {
	// Call start method of bee plugin instance
	beePluginInstance.start(template); // template is the JSON to be loaded in BEE
    });
  }
};

// This is a sample call to YOUR server-side application that calls the loginV2 endpoint on BEE the side
req.open(
	'POST', 	// Method
	'/YOUR_BACKEND_TOKEN_ENDPOINT', // your server endpoint
	false 		// sync request
);

```

Ensure to call the authorization endpoint server-side to protect your credentials.

Once you obtain the token, the [configuration parameters](https://docs.beefree.io/configuration-parameters/) object is passed to BEE Plugin to set up the options you wish (e.g., setting the editor’s language to “Spanish”).

Then, you can use BEE plugin methods to [start your instance and display the editor](./) on your page.

The plugin will keep this session alive for 12 hours from the login.

After 12 hours, you have to manage the token expiration, as follows:

1. Obtain a new token via the new authorization endpoint
2. Inject the token obtained from step one via the updateToken method (see examples below)

Here is an example of how to inject the token in the current BEE Plugin instance:

```json
// obtain a new token with a new LoginV2 call
// update the token in the current BeePlugin instance
beePluginInstance.updateToken(token);
```

Here is an example of how to get the current JSON from the expiration error:

```json
onError: function (error) {
  var code = error.code
  var detail = error.detail

  // the template the user was working on before the error occurred
  var currentJson = error.template
  ... 


  beePluginInstance.updateToken(token);
  // the beePluginInstance comes from the BeePlugin.create 
  ...

```

## Error Management

When you set up an `onError` callback you will get the `error` object as a parameter.

From that object, you can grab the `code` property and use it as explained in the table below.

| Code | Message                           | Detail                                                                                                                                                                                                                                                                                                               |
| ---- | --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 5101 | Expired token cannot be refreshed | You need to do a new login and update the token in the current Builder instance using `updateToken` method.                                                                                                                                                                                                          |
| 5102 | Expired token must be refreshed   | <p>You need to do a new login and create a new Builder instance using the new token, <code>BeePlugin.create()</code> and the current JSON template present in this event<br></p><p>Example scenarios:</p><ul><li>The version is outdated</li><li>BEE releases a security fix and every client must refresh</li></ul> |
