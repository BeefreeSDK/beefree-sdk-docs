# Authorization Process

## Authorization Process Overview

The Authorization Process is an important step throughout your [Beefree SDK installation process](./). This steps validates your Beefree SDK credentials and provides you with a token. Take the steps outlined in this document to ensure you accurately complete the authorization process.&#x20;

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

The Beefree SDK system uses OAuth2 as the authorization framework.

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

The token you receive from the authorization server should be passed to the BeePlugin.create(...) as it is. We strongly suggest not altering it in any way. Also, don’t rely on the token response's content or structure. If you do, any change to the schema could make your integration stop working.

The token expires after 5 minutes for security reasons. Beefree SDK will refresh an expired token automatically for 12 hours without re-authenticating the application. Beefree SDK will trigger the `onError` callback when the token can't be refreshed automatically.

{% hint style="info" %}
**Note:** When a refreshable token expires, Beefree SDK receives a [401 error](../../error-management/json-parser-errors.md#authentication-errors) and attempts to refresh it automatically. 401 errors are expected and part of the process.
{% endhint %}

The following code sample displays an example of how to call the Beefree SDK endpoint, obtain a token, and then start it.

```javascript
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
  if (req.readyState === 4 && req.status === 200) {
    // Obtain token
    var token = req.responseText;
    // Call create method and pass token and beeConfig to obtain an instance of Beefree SDK
    BeePlugin.create(token, beeConfig, function(beePluginInstance) {
	// Call start method of beefree SDK instance
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

Once you obtain the token, the [configuration parameters](https://docs.beefree.io/configuration-parameters/) object is passed to Beefree SDK to set up your customization options, for example setting the editor’s language to “Spanish”.

Then, you can use Beefree SDK methods to [start your instance and display the editor](./) on your page.

Beefree SDK will keep this session alive for 12 hours from the login. After 12 hours, you have to manage the token expiration, as follows:

1. Obtain a new token via the new authorization endpoint.
2. Inject the token obtained from step one via the `updateToken` method. Reference examples of this in the following section.

The following code example shows how to inject the token in the current Beefree SDK instance:

```json
// obtain a new token with a new LoginV2 call
// update the token in the current Beefree SDK instance
beePluginInstance.updateToken(token);
```

The following code example displays how to get the current JSON from the expiration error:

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

| Code | Message                           | Detail                                                                                                                                                                                                                                                                                                                       |
| ---- | --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 5101 | Expired token cannot be refreshed | You need to do a new login and update the token in the current Builder instance using `updateToken` method.                                                                                                                                                                                                                  |
| 5102 | Expired token must be refreshed   | <p>You need to do a new login and create a new Builder instance using the new token, <code>BeePlugin.create()</code> and the current JSON template present in this event<br></p><p>Example scenarios:</p><ul><li>The version is outdated</li><li>Beefree SDK releases a security fix and every client must refresh</li></ul> |

### Handling error management

The following code samples display how to handle the 5101 and 5102 errors.

{% tabs %}
{% tab title="Handle 5101" %}
Error management error 5101

```javascript
onError: function (error) {
 var code = error.code
 var detail = error.detail
 switch (code) {
   case 5101: // re-login and update token in the beeInstance
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
 if (req.readyState === 4 && req.status === 200) {
   // Obtain token
   var token = req.responseText;
   // Call update method and pass the new token existent BeePlugin instance
   BeePlugin.updateToken(token);
 }
};
req.open(
 'POST',  // Method
 '/token',  // The server side endpoint that calls BEE REST auth endpoint
 false   // sync request
);

     break
   case 5102: // re-login and create a new beeInstance
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
 if (req.readyState === 4 && req.status === 200) {
   // Obtain token
   var token = req.responseText;
   // Call update method and pass token and beeConfig to obtain an instance of BEE Plugin
   BeePlugin.create(token, beeConfig, function(beePluginInstance) {
     // Call start method of bee plugin instance
     beePluginInstance.start(template); // template is the json to be loaded in BEE
   });
 }
};
req.open(
 'POST',  // Method
 '/token',  // The server side endpoint that calls BEE REST auth endpoint
 false   // sync request
);
     break
 }
},

```
{% endtab %}

{% tab title="Hande 5102" %}
Error management 5102

```javascript
onError: function (error) {
 var code = error.code
 var detail = error.detail
 switch (code) {
   case 5101: // re-login and update token in the beeInstance
...
   case 5102: // re-login and create a new beeInstance
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
 if (req.readyState === 4 && req.status === 200) {
   // Obtain token
   var token = req.responseText;
   // Call update method and pass token and beeConfig to obtain an instance of BEE Plugin
   BeePlugin.create(token, beeConfig, function(beePluginInstance) {
     // Call start method of bee plugin instance
     beePluginInstance.start(detail.template); // the template the user was working on before the error occurred
   });
 }
};
req.open(
 'POST',  // Method
 '/token',  // The server side endpoint that calls BEE REST auth endpoint
 false   // sync request
);
     break
 }
},

```
{% endtab %}
{% endtabs %}

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
