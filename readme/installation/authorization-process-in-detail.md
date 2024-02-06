# Authorization process in detail

To initialize your Beefree application, call the endpoint shown in the sample code below with your **Client ID** and **Client Secret**, which are available in the application details page of the [Beefree SDK Console](https://dam.beefree.io/devportal) (if you don’t have an account, [sign up](https://dam.beefree.io/devportalsignup)).

The Beefree platform uses **OAuth2** as the authorization framework.

```http
POST /apiauth HTTP/1.1
Host: auth.getbee.io
Accept: application/json
Content-Type: application/x-www-form-urlencoded
client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET
```

We strongly suggest not to put your Beefree application credentials in front-end code - they are specific to your account, and they could be easily read and used by other people.

The `grant_type` parameter, which was mandatory in the past, can now be omitted.

If the authentication is successful, the Beefree platform’s authorization service will return a temporary **access token** to the client application. The token can then be passed by the client application to the Beefree resource server in order to start the session.

Note: the **entire response** from the auth endpoint must be passed here, not just the access token you receive. The access token itself must also be converted to valid JSON with **JSON.parse(token)**.

The token you receive from the authorization server should be passed to the Beefree resource server as it is. We strongly suggest not to integrate or alter it in any way - if so, any change on our side could make your integration stop working.

The token expires after 5 minutes for security reasons. An expired token can be refreshed for 7 days without re-authenticating the application. Once the application has started communicating with the Beefree resource server, the plugin will take care of refreshing the token automatically, as long as someone is actively using the editor, with a heartbeat every 28 minutes.

If a token has expired, your Beefree application will receive a 401 error and attempts to refresh it automatically. The 401 errors are nothing to worry about as they are part of this process.

Here is an example of how to call the Beefree platform endpoint, obtain a token and then start the plugin:

```javascript
var req = new XMLHttpRequest();
req.onreadystatechange = function() {
	if (req.readyState === 4 && req.status === 200) {
		// Obtain token
    	var token = req.responseText;
    	// Call create method and pass token and beeConfig to obtain an instance of BEE Plugin
    	BeePlugin.create(token, beeConfig, function(beePluginInstance) {
			// Call start method of bee plugin instance
	    	beePluginInstance.start(template); // template is the json to be loaded in BEE
		});
	}
};
req.open(
	'POST', 	// Method
	'/token', 	// The server side endpoint that calls BEE REST auth endpoint
	false 		// sync request
);
```

You can call the authorization endpoint clientside or serverside: just make sure to use HTTPS if your call is from a web client.

Once you obtain the token, [configuration parameters](configuration-parameters/) are passed to your Beefree application to set up the options you wish to use (e.g. setting your email editor’s language to “Spanish”).\
Then, you can [start your Beefree application and display the builder](./).
