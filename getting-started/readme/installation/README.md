---
description: Install Beefree SDK to get started with your implementation.
coverY: 0
layout:
  cover:
    visible: false
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Installation and Fundamentals

## Add JavaScript Library <a href="#add-javascript-library" id="add-javascript-library"></a>

Congratulations on [creating your first application](../create-an-application.md)!  Now it’s time to install it. The first step is to add the Beefree SDK library to your application. You can use our [convenient NPM module](https://www.npmjs.com/package/@beefree.io/sdk) to add it.

### **NPM**

Use the command `npm i @beefree.io/sdk` to install the Beefree SDK library into your project.

```

npm i @beefree.io/sdk

```

## Initialize the application <a href="#initialize-the-application" id="initialize-the-application"></a>

Take the steps outlined in this section to initialize your application.

### Step 1. Create a container

The embedded application (email builder, page builder, popup builder, file manager) will load into any HTML element on your page.

We recommend starting with an empty div, as follows:

```markup

<div id="bee-plugin-container"></div>

```

### Step 2. Authentication

Beefree cares about your security. This is why we use a standard JSON Web Token, or JWT, to authenticate your application.

To authenticate your application, pass your **Client ID** and **Client Secret** to our authorization service, and we’ll send your unique token back to you.

We talk about this step in detail [here](authorization-process-in-detail.md), but here’s a quick example:

#### Authentication Code Samples

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

#### JSON Authorization Response

```json
{
    "access_token": "...",
    "v2": true
}
```

### Step 3. Create an application

Now that you have a token, you can initialize the application into your empty div.

To do so, you will call the `create` method, which has three parameters:

* `token`\
  This is the result of the previous step.
* `config`\
  This contains your settings and event handlers.
* `callback`\
  This is a function that receives the application instance

Here is an example in plain JavaScript:

```javascript


// Define a global variable to reference the application instance
// Tip: Later, you can call API methods on this instance, e.g. bee.load(template)
var bee;
 
// Define a simple Beefree SDK application configuration...
var config = {
    uid: 'string',
    container: 'string'
}

// Call the "create" method:
// Tip:  window.BeePlugin is created automatically by the library...
window.BeePlugin.create(token, config, function(instance) {
    bee = instance;
    // You may now use this instance...
});


```

The following table shows all of the required [configuration settings](configuration-parameters/):

<table><thead><tr><th width="121">Attribute</th><th width="77">Type</th><th>Description</th></tr></thead><tbody><tr><td>uid</td><td>string</td><td><p>An alphanumeric string that identifies the user and allows the embedded application to load resources for that user (e.g. images).</p><ul><li>Min length: 3 characters</li><li>Can contain letters from a to z (uppercase or lowercase), numbers and the special characters _ (underscore) and – (dash)</li><li>It is a string and not a numeric value</li></ul><p>It uniquely identifies a user of the Beefree application. When we say “uniquely”, we mean that:</p><ul><li>It will be counted as a unique user for monthly billing purposes.</li><li>Images (and other files) used by the user when creating and editing messages will be associated with it and not visible to other users (when using the default storage).</li></ul></td></tr><tr><td>container</td><td>string</td><td>Identifies the id of div element that contains the application</td></tr></tbody></table>

### Step 4. Start the application

The final step is to start the application, using the `start` method.

* If the application is one of the builders, do so by loading a template.
* If the application is the File Manager, no parameters are needed.

Call the `start` method as follows:

```javascript

var template = { ... }; // Any valid template, as JSON object
 
bee.start(template);

```

{% hint style="info" %}
The instance method <mark style="color:red;">`bee.start(template)`</mark> does not need to be called immediately after <mark style="color:red;">`create`</mark>. In a SPA (Single Page Application) or React app, you can <mark style="color:red;">`create`</mark> the editor in a hidden global state but then call the `start` method when the template is selected and available.\
\
The application loads quickly when all steps are completed consecutively. However, by separating the loading workflow into two parts, the end-user will perceive loading in a fraction of the overall time.\
\
Remember, if the <mark style="color:red;">`client_id`</mark> belongs to a File Manager application, <mark style="color:red;">`bee.start()`</mark> can be called without any parameters.
{% endhint %}
