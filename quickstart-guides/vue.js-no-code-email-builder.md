---
description: >-
  Welcome to the Vue.js Quickstart Guide for embedding Beefree SDK's no-code
  email builder in your Vue.js application.
---

# Vue.js No-code Email Builder

## **Introduction**

This Quickstart Guide walks you through embedding the Beefree SDK’s no-code email builder into a Vue 3 application using the [`/loginV2`](https://docs.beefree.io/beefree-sdk/docs/authorization-process-in-detail) authorization process. By the end of this guide, you’ll have a fully functional Vue app running locally with the builder embedded, authenticated, and ready to use—following Vue best practices.

### **Prerequisites**

Before you begin, make sure you:

* Understand [Vue.js](https://vuejs.org/guide/introduction.html) and its core concepts (for example,  `ref`, `onMounted`)
* Have a [Beefree SDK account](https://developers.beefree.io/accounts/login/?from=website_menu)
* [Create an application](https://docs.beefree.io/beefree-sdk/docs/create-an-application) in the Beefree Developer Console
* Obtain your **Client ID** and **Client Secret** from the Developer Console

### **What You’ll Learn**

This guide covers how to:

* [Set up a new Vue 3 app](vue.js-no-code-email-builder.md#id-1.-create-a-vue-3-app)
* [Install the Beefree SDK](vue.js-no-code-email-builder.md#id-2.-install-beefree-sdk)
* [Set up secure authentication using a proxy server](vue.js-no-code-email-builder.md#authentication-flow-server-side-only)
* [Initialize and embed the builder](vue.js-no-code-email-builder.md#id-4.-create-the-editor-component)
* [Run and test your app locally](vue.js-no-code-email-builder.md#id-6.-run-the-application)

### **1. Create a Vue 3 App**

To create your Vue 3 app, open a terminal and run the following command. This example uses `beefree-vue-demo` as the project name.

```bash
npm init vue@latest beefree-vue-demo
cd beefree-vue-demo
npm install
```

After installation, your project structure will be ready for development. You’ll create and wire up the main app component and the Beefree editor component in the next steps.

### **2. Install Beefree SDK**

To install the official [Beefree SDK npm package](https://www.npmjs.com/package/@beefree.io/sdk), run:

```bash
npm install @beefree.io/sdk
```

This package contains everything needed to instantiate and render the no-code email builder inside your Vue application.

### **3. Create the Main App Component**

Now you’ll set up your app’s primary UI structure, which includes a header and a “Read the Docs” button, plus the embedded builder component.

#### **Vue-Specific Implementation Tips**

* The `<BeefreeEditor />` component will be a custom child component
* You'll use the `ref` function to get a DOM reference for the builder
* Lifecycle logic (like initializing the builder) goes inside `onMounted`
* TypeScript integration is supported

#### **File: `src/App.vue`**

```typescript
<template>
  <div class="app">
    <header class="header">
      <h1>Welcome to My Beefree Demo</h1>
      <a
        href="https://docs.beefree.io/beefree-sdk"
        target="_blank"
        rel="noopener noreferrer"
      >
        <button class="docs-button">Read the Docs</button>
      </a>
    </header>
    <BeefreeEditor />
  </div>
</template>

<script setup lang="ts">
import BeefreeEditor from './components/BeefreeEditor.vue'
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  padding: 20px;
}
.header {
  margin-bottom: 30px;
}
.docs-button {
  padding: 10px 20px;
  font-size: 16px;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>

```

This file is responsible for the layout and basic interface of your app. It creates a container that introduces the demo, links to the documentation, and includes the builder.

{% hint style="info" %}
**Note:** This helps you visually distinguish the application UI from the embedded builder’s interface.
{% endhint %}

### **4. Create the Editor Component**

You’ll now define the builder logic in a dedicated component—`BeefreeEditor.vue`.

This step includes setting up the container, initializing the SDK, handling callbacks, and fetching a secure token.

#### **Authentication Flow (Server-Side Only)**

To securely authenticate with Beefree:

* Never expose your Client ID or Client Secret in frontend code
* Always use a backend or proxy server to call `/loginV2`
* Pass a `UID` to uniquely identify the user session

#### **Editor Configuration**

The SDK needs a configuration object with at least one **required** field:

* `container`: the ID of the DOM element where the builder should mount

You can also pass optional parameters like `language`, `onSave`, `onError`, and more.

#### **File: `src/components/BeefreeEditor.vue`**

```typescript
<template>
  <div
    id="beefree-container"
    ref="containerRef"
    class="editor-container"
  />
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import BeefreeSDK from '@beefree.io/sdk'

const containerRef = ref<HTMLElement | null>(null)

onMounted(async () => {
  try {
    const beeConfig = {
      container: 'beefree-container',
      language: 'en-US',
      onSave: (pageJson: string, pageHtml: string, ampHtml: string | null, templateVersion: number, language: string | null) => {
        console.log('Saved!', { pageJson, pageHtml, ampHtml, templateVersion, language })
      },
      onError: (error: unknown) => {
        console.error('Error:', error)
      }
    }

    const token = await fetch('http://localhost:3001/proxy/bee-auth', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ uid: 'demo-user' })
    }).then(res => res.json())

    const bee = new BeefreeSDK(token)
    bee.start(beeConfig, {})

  } catch (error) {
    console.error('Initialization error:', error)
  }
})
</script>

<style scoped>
.editor-container {
  height: 600px;
  width: 90%;
  margin: 20px auto;
  border: 1px solid #ddd;
  border-radius: 8px;
}
</style>

```

This file handles:

* Creating a DOM reference using Vue’s `ref`
* Initializing the builder in `onMounted`
* Fetching an access token from the proxy server
* Handling `onSave` and `onError` callbacks

You can later extend this to include additional config options like custom translations, modules, sidebar positioning, and more.

### **5. Set Up the Proxy Server**

To authenticate securely using `/loginV2`, create a lightweight proxy server with Node.js and Express.

#### **Why a Proxy is Required**

The Beefree SDK requires authentication via Client ID and Client Secret, which must **not** be exposed in frontend code. The proxy server allows you to:

* Keep credentials safe
* Fetch access tokens securely

#### **File: `proxy-server.js` (root directory)**

```javascript
import express from 'express'
import cors from 'cors'
import axios from 'axios'

const app = express()
const PORT = 3001

app.use(cors())
app.use(express.json())

// Replace with your actual credentials
const BEE_CLIENT_ID = 'YOUR-CLIENT-ID'
const BEE_CLIENT_SECRET = 'YOUR-CLIENT-SECRET'

app.post('/proxy/bee-auth', async (req, res) => {
  try {
    const response = await axios.post(
      'https://auth.getbee.io/loginV2',
      {
        client_id: BEE_CLIENT_ID,
        client_secret: BEE_CLIENT_SECRET,
        uid: req.body.uid || 'demo-user'
      },
      { headers: { 'Content-Type': 'application/json' } }
    )
    res.json(response.data)
  } catch (error) {
    console.error('Auth error:', error.message)
    res.status(500).json({ error: 'Failed to authenticate' })
  }
})

app.listen(PORT, () => {
  console.log(`Proxy server running on http://localhost:${PORT}`)
})

```

This server exposes a POST route (`/proxy/bee-auth`) that:

* Accepts a `uid` from the client
* Calls the Beefree Auth endpoint
* Returns a token to the frontend

You’ll also install `axios`, `express`, and `cors` as dependencies.

### **6. Run the Application**

You’re now ready to run both the Vue app and the proxy server.

{% hint style="info" %}
**Important:** Run each in a separate terminal tab or window.
{% endhint %}

**Terminal 1 (Proxy Server)**

```bash
npm install express cors axios
node proxy-server.js
```

**Terminal 2 (Vue App)**

```bash
npm run dev
```

Then visit: [http://localhost:5173](http://localhost:5173/)

You should see your app running with the builder loaded inside the UI.

## **Troubleshooting Tips**

This section lists best practices to keep in mind, and troubleshooting tips while embedding Beefree SDK into your Vue.js application.&#x20;

#### **Blank Editor Container**

* Double-check that the `container` ID in the config matches the element’s `id`
* Confirm the container has a set height and width in CSS
* Look at the console for JavaScript errors during initialization

#### **Authentication Issues**

* Make sure the proxy server is running
* Verify that your Client ID and Secret are correct
* Open DevTools → Network tab to inspect token requests

#### **TypeScript Errors**

* Use types from `@beefree.io/sdk/dist/types/bee`
* Ensure all required parameters (like `container`) are present
* Check that all callbacks match expected signatures

### **Common Pitfalls to Avoid**

* Don’t expose credentials in your frontend code
* Handle token expiration scenarios (for example, show a message or refresh)

### **Next Steps**

With Beefree SDK running in your Vue 3 app, you can explore advanced customization options such as:

* [Custom translations](https://docs.beefree.io/beefree-sdk/docs/custom-languages)
* [Module ordering](https://docs.beefree.io/beefree-sdk/docs/content-tile-sorting)
* [Sidebar positioning](https://docs.beefree.io/beefree-sdk/docs/custom-sidebar-position)
* [Grouping modules](https://docs.beefree.io/beefree-sdk/docs/content-tile-grouping)

Explore more in the [Beefree SDK documentation](https://docs.beefree.io/beefree-sdk).
