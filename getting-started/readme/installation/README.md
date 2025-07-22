---
description: >-
  Learn and understand the core concepts related to how you can install the
  Beefree SDK npm package, authenticate, and get started with Beefree SDK.
coverY: 0
---

# Installation and Fundamentals

## Introduction <a href="#add-javascript-library" id="add-javascript-library"></a>

This page discusses the core concepts related to installing Beefree SDK within your application. These core concepts are the following:

* Installing the [Beefree SDK npm package](https://app.gitbook.com/o/hABGoPMOKISmuDmz4fbV/s/xZgBDrdhQLtWmkGqVR59/) within your application.
* Understanding the [Authorization process](authorization-process-in-detail.md) and how to successfully authenticate server-to-server.
* Adding the required [Beefree SDK configuration](configuration-parameters/) to your application.&#x20;

By the end of this guide, you'll understand the core concepts related to how you can install the package, authenticate, and get started with Beefree SDK. You'll have working a local environment set up on your machine to experiment with.

For a quick start, visit our [React](../../../quickstart-guides/react-no-code-email-builder.md), [Angular](../../../quickstart-guides/angular-no-code-email-builder.md), and [Vue.js](../../../quickstart-guides/vue.js-no-code-email-builder.md) Quickstart guides, which each include complete sample code by framework.

## **Prerequisites**

Prior to integrating Beefree SDK, ensure you have completed the following:

1. Signed up for a [Beefree SDK Developer Console](https://developers.beefree.io/signup) account.
   1. [Created an application](../create-an-application.md) within the Developer Console
   2. Obtained a Client ID and Client Secret for that application
2. Node.js (v14 or higher) installed.
3. A modern web browser (Chrome, Firefox, Safari, Edge).

## **Core Concepts**

This section covers the core concepts for installing Beefree SDK within your application and launching a local environment.

The concepts covered in this section are the following:

* [npm package installation](./#package-installation)
* [Authentication Process](./#authentication-process)
* [Beefree SDK Initialization](./#beefree-sdk-initialization) &#x20;

{% hint style="info" %}
**Note:** Reference the [React](../../../quickstart-guides/react-no-code-email-builder.md), [Angular](../../../quickstart-guides/angular-no-code-email-builder.md), or[ Vue.js](../../../quickstart-guides/vue.js-no-code-email-builder.md) Quickstart Guides for a guided walkthrough by framework and sample code using a simple implementations.
{% endhint %}

### **Package Installation**

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

This section discusses the authentication process. It explains important concepts related to how to successfully authenticate using a server-to-server call.&#x20;

The secure authentication flow requires a server-to-server call to obtain a JWT token. This process ensures your client credentials remain protected.

At a high level, the steps you need to take throughout the authentication process are the following:

1. **Secure Credentials**
   1. Never expose `client_id` or `client_secret` in frontend code.
   2. Store them in backend environment variables (`.env`).
2. **Backend Proxy Setup**
   1. Set up a server-to-server call.
   2. Forward the complete response `access_token` and `v2` to the frontend.
3. **Auth Request from Backend**

* Call Beefree SDK’s `loginV2` and include the following required parameters:
  * `client_id`&#x20;
  * `client_secret`&#x20;
  * `uid`

4. **Frontend Handling**
   1. Fetch token only from your proxy.
   2. Extract `access_token` from response.
   3. Initialize SDK: `new BeefreeSDK(access_token)`.

#### **Authentication Endpoint**

```hpkp
POST https://auth.getbee.io/loginV2
```

#### **Required Parameters**

The following table lists and describes the required authentication parameters.

| Parameter       | Type   | Description                 | Example             |
| --------------- | ------ | --------------------------- | ------------------- |
| `client_id`     | string | Your application client ID  | "abc123-client-id"  |
| `client_secret` | string | Your application secret key | "xyz456-secret-key" |
| `UID`           | string | Unique user identifier      | "user-12345"        |

**Example Implementation (Node.js)**

```javascript
async function initializeBeefreeEditor(templateJson, beeConfig) {
  try {
    const response = await fetch('http://localhost:3001/proxy/bee-auth', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ uid: 'demo-user' }) // customize UID if needed
    });

    if (!response.ok) {
      throw new Error('Failed to fetch token from proxy server');
    }

    const { token } = await response.json();

    BeefreeSDK.create(token, beeConfig, (beeInstance) => {
      beeInstance.start(templateJson); // templateJson is your design content
    });
  } catch (error) {
    console.error('Error initializing Beefree SDK:', error);
  }
}
```

{% hint style="warning" %}
**Important Notes:**

* The UID must be consistent between authentication and SDK configuration.
* Tokens are valid for 12 hours.
* Ensure client\_secret and client\_id aren't exposed in the client-side code.
{% endhint %}

#### **JSON Authorization Response**

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
<div id="beefree-sdk-container" style="width: 100%; height: 800px;"></div>
```

#### **Configuration Options**

Beefree SDK requires a configuration object with the required `container` property. [Optional parameters](configuration-parameters/) are also available to customize the builder, but `container` is the only required one for initializing Beefree SDK.

The following code snippet shows an example of this:

```javascript
var config = {
    container: 'string'
}
```

#### **Full Configuration Reference**

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

### **Frequently Asked Questions**

**Q: Can I use the SDK without server-side authentication?**\
A: While possible for testing, production implementations must use server-side auth for security.

**Q: How do I customize the editor's appearance?**\
A: The SDK supports UI customization through [configuration options](configuration-parameters/). While the Configuration parameters provides a high level example, there are several configuration options outlined throughout the comprehensive technical documentation.

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
* Monitor for Beefree SDK updates and new features
