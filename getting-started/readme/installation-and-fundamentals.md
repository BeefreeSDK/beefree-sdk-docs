# Installation and Fundamentals

## **Introduction**

Beefree SDK is an embeddable no-code content builder that enables your end users to build stunning marketing assets, such as emails, landing pages, and popups, without writing a single line of code.&#x20;

The following list includes a few key features within Beefree SDK:

* Drag-and-drop visual editors
* File manager
* Multi-user collaboration
* Responsive design capabilities
* Extensive template library
* Secure authentication workflow

This guide provides comprehensive instructions and best practices for implementing Beefree SDK.

### **Getting Started**

This section discusses how to get started with Beefree SDK.&#x20;

#### **Prerequisites**

Prior to integrating Beefree SDK, ensure you have:

1. A Beefree SDK [developer account](https://developers.beefree.io/signup).
2. Node.js (v14 or higher) installed.
3. A modern web browser (Chrome, Firefox, Safari, Edge).

#### **Local Development Setup**

To test the SDK locally before production deployment:

1.  Clone the demo repository:

    ```bash
    git clone https://github.com/BeefreeSDK/beefree-sdk-npm-official.git
    ```
2.  Install dependencies:

    ```bash
    npm install
    # or
    yarn install
    ```
3.  Configure environment:

    ```bash
    cp .env.sample .env
    ```
4.  Start the dev server:

    ```bash
    npm start
    ```
5. Access at `http://localhost:8081`

#### **Package Installation**

You can install Beefree SDK using either [npm](https://www.npmjs.com/package/@beefree.io/sdk) or [yarn](https://yarnpkg.com/):

**Using npm**

```bash
npm install @beefree.io/sdk --save
```

**Using Yarn**

```bash
yarn add @beefree.io/sdk
```

**Package Details:**

* TypeScript Support: Included
* License: Apache-2.0
* Repository: [Beefree SDK GitHub](https://github.com/BeefreeSDK/beefree-sdk-npm-official)

### **Authentication Process**

This section discusses the authentication process.

#### **Server-Side Authentication**

The secure authentication flow requires a server-to-server call to obtain a JWT token. This process ensures your client credentials remain protected.

**Authentication Endpoint**

```
POST https://auth.getbee.io/loginV2
```

**Required Parameters**

The following table lists and descibes the required authentication parameters.

| Parameter       | Type   | Description                 | Example             |
| --------------- | ------ | --------------------------- | ------------------- |
| `client_id`     | string | Your application client ID  | "abc123-client-id"  |
| `client_secret` | string | Your application secret key | "xyz456-secret-key" |
| `UID`           | string | Unique user identifier      | "user-12345"        |

**Example Implementation (Node.js)**

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

// This is a sample call to YOUR server side application that calls the loginV2 endpoint on BEE the side
req.open(
	'POST', 	// Method
	'/YOUR_BACKEND_TOKEN_ENDPOINT', // your server endpoint
	false 		// sync request
);
```

{% hint style="warning" %}
**Important Notes:**

* The UID must be consistent between authentication and SDK configuration.
* Tokens are valid for 12 hours.
* Ensure client\_secret and client\_id aren't exposed in the client-side code.
{% endhint %}

**JSON Authorization Response**

```json
{
    "access_token": "...",
    "v2": true
}
```

### **Beefree SDK Initialization**

This section discusses how to initialize Beefree SDK.

#### **Container Setup**

Create a container element in your HTML where the editor will render:

```html
<div id="bee-plugin-container" style="width: 100%; height: 800px;"></div>
```

#### **Configuration Options**

Beefree SDK requires a configuration object with the following essential property:

```javascript
var config = {
    container: 'string'
}
```

**Full Configuration Reference**

The following table explains the container property.

| Property  | Type   | Required | Description                   |
| --------- | ------ | -------- | ----------------------------- |
| container | string | Yes      | DOM element ID for the editor |

### **Working with Templates**

#### **Loading a Template**

Initialize the editor with a template JSON object:

```javascript
// After successful initialization
const template = {
  // Your template JSON here
  // Sample templates available at:
  // https://github.com/BeefreeSDK/beefree-sdk-assets-templates
};

bee.start(template);
```

Reference the [beefree-sdk-assets-templates repository](https://github.com/BeefreeSDK/beefree-sdk-assets-templates) in GitHub for example templates.&#x20;

#### **Template Management Methods**

The following table lists template management methods that are important for getting started.

| Method             | Description           | Example                       |
| ------------------ | --------------------- | ----------------------------- |
| `load(template)`   | Load new template     | `bee.load(newTemplate)`       |
| `reload(template)` | Force reload template | `bee.reload(updatedTemplate)` |
| `save()`           | Trigger save callback | `bee.save()`                  |
| `saveAsTemplate()` | Save as template      | `bee.saveAsTemplate()`        |

{% hint style="warning" %}
The instance method `bee.start(template)` does not need to be called immediately after `create`. In a SPA (Single Page Application) or React app, you can `create` the editor in a hidden global state but then call the `start` method when the template is selected and available. The application loads quickly when all steps are completed consecutively. However, by separating the loading workflow into two parts, the end-user will perceive loading in a fraction of the overall time. Remember, if the `client_id` belongs to a File Manager application, `bee.start()` can be called without any parameters.
{% endhint %}

### **Advanced Features**

#### **Token Refresh Implementation**

Implement automatic token refresh to maintain uninterrupted sessions:

```javascript
// Refresh expired token (call before 12-hour expiry)
bee.updateToken(newToken); 
```

How to use:

1. Get a fresh token from your backend
2. Pass it to `updateToken()`

#### **Collaborative Editing**

Enable real-time collaboration with these additional methods:

```javascript
// Join a co-editing session
bee.join({ uid: "user-123" }, "shared-session-id"); 
```

How to use:

1. Generate a unique `session-id` on your server
2. Call `join()` with the same ID for all collaborators

### **Troubleshooting**

The following list includes the most common issues and steps for troubleshooting them.

* **Authentication Failures**
  * Verify `client_id` and `client_secret`
  * Ensure UID matches between auth and config
  * Check network connectivity to auth.getbee.io
* **Editor Not Loading**
  * Confirm container element exists
  * Verify container ID matches config
  * Check for JavaScript errors in console
* **Token Expiration Issues**
  * Implement `onTokenExpired` callback
  * Test token refresh flow

### **Frequently Asked Questions**

**Q: Can I use the SDK without server-side authentication?**\
A: While possible for testing, production implementations must use server-side auth for security.

**Q: How do I customize the editor's appearance?**\
A: The SDK supports UI customization through configuration options. Refer to the advanced documentation.

**Q: What happens when the token expires?**\
A: When your token expires after 12 hours:

1. The editor will become unresponsive
2.  You must proactively:

    ```javascript
    // 1. Get a fresh token from your backend
    const newToken = await fetch('/refresh-token');

    // 2. Update the SDK instance
    bee.updateToken(newToken);
    ```
3. Best practice is to refresh tokens **before expiration** (recommended at 11 hours)

**Q: Where can I find sample templates?**\
A: Visit our [template repository](https://github.com/BeefreeSDK/beefree-sdk-assets-templates) for examples.

### **Conclusion**

This comprehensive guide covers all aspects of Beefree SDK integration, from initial setup to advanced features.

Remember to:

* Always use server-side authentication
* Implement proper token refresh logic
* Test thoroughly before production deployment
* Monitor for SDK updates and new features
