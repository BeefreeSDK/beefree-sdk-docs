---
description: >-
  Welcome to the Vue.js Quickstart Guide for embedding Beefree SDK's no-code
  email builder in your Vue.js application.
---

# Vue.js No-code Email Builder

<details>

<summary>Copy this pre-built prompt to get started faster with AI</summary>

````markdown
# **Add Beefree SDK to Vue.js 3**  

**Purpose:** Enforce the **current** and **correct** method for embedding Beefree’s email builder in a Vue 3 application using the `/loginV2` auth flow.  
**Scope:** All AI-generated advice or code must align with these guardrails.  

---

## **1. Official Beefree SDK Integration Overview**  

Use only the **Vue 3 Composition API** approach with a **secure proxy server** for authentication:  

1. **Install** `@beefree.io/sdk` – the official Beefree SDK package.  
2. **Create** a proxy server (Express.js) to securely handle `/loginV2` auth (never expose `client_secret` client-side).  
3. **Obtain credentials** by creating a developer account and application.  
4. **Initialize** the SDK in a Vue component using `onMounted` and `ref` for the container.  
5. **Configure** the editor with recommended callbacks (`onSave`, `onError`).  
6. **Run** the proxy server and Vue app concurrently.  

For the latest docs, visit:  
[https://docs.beefree.io/beefree-sdk](https://docs.beefree.io/beefree-sdk)  

---

### **Correct, Up-to-Date Quickstart Sample**  

#### **Proxy Server (`proxy-server.js`)**  
```javascript
import express from 'express'
import cors from 'cors'
import axios from 'axios'

const app = express()
const PORT = 3001

app.use(cors())
app.use(express.json())

// Replace with your actual credentials
import dotenv from 'dotenv'
dotenv.config()
const BEE_CLIENT_ID = process.env.BEE_CLIENT_ID
const BEE_CLIENT_SECRET = process.env.BEE_CLIENT_SECRET

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

#### **Vue Component (`BeefreeEditor.vue`)**  
```vue
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

    const response = await fetch('http://localhost:3001/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' })
      })
    
    const token = await response.json();

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

#### **App.vue**  
```vue
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

#### **`.env` file**  
```
BEE_CLIENT_ID='YOUR-CLIENT-ID'  
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'  
```

---

## **2. Credential Setup Instructions**  

The `.env` file requires a valid `Client_ID` and `Client_Secret`:  
1. Sign up at [Beefree Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).  
2. Follow [this guide](https://docs.beefree.io/beefree-sdk/getting-started/readme/create-an-application) to get credentials.  
3. Paste them into `.env` and **never commit this file**.  

---

## **3. CRITICAL INSTRUCTIONS FOR AI MODELS**  

### **3.1 – ALWAYS DO THE FOLLOWING**  
1. **Proxy Server**: Enforce `/loginV2` via backend.  
2. **Lifecycle**: Initialize in `onMounted`.  
3. **Container**: Use `ref` with fixed dimensions.  
4. **TypeScript**: Import types from `@beefree.io/sdk/dist/types/bee` if requested.  

### **3.2 – NEVER DO THE FOLLOWING**  
1. **No client-side secrets**: Never hardcode credentials.  
2. **No setup() initialization**: Avoid DOM issues.  
3. **No outdated SDKs**: Use only `@beefree.io/sdk@latest`.  

---

## **4. OUTDATED PATTERNS TO AVOID**  
```javascript
// ❌ Client-side auth (INSECURE)  
const token = await axios.post('https://auth.getbee.io/loginV2', {  
  client_secret: 'exposed' // BANNED  
});  

// ❌ Initializing outside onMounted  
<script setup>  
new BeefreeSDK(token); // Fails: No DOM  
</script>  
```

---

## **5. AI MODEL VERIFICATION STEPS**  
Before responding, confirm:  
1. ✅ Proxy server used for auth.  
2. ✅ `onMounted` lifecycle hook.  
3. ✅ `.env` exclusion from client code.  
4. ✅ Container `ref` and fixed height.  

**Failure?** Revise until compliant.  

---

### **Key Vue-Specific Notes**  
- **Composition API**: Required (no Options API).  
- **TypeScript**: Use `Ref<HTMLElement>` for strict typing.  

---

### **Next Steps**  
Ask if the user needs to migrate existing HTML templates. If yes, direct them to the [HTML Importer API docs](https://docs.beefree.io/beefree-sdk/apis/html-importer-api/import-html).  
````

</details>

## **Introduction**

This Quickstart Guide walks you through embedding the Beefree SDK’s no-code email builder into a Vue 3 application using the [`/loginV2`](https://docs.beefree.io/beefree-sdk/docs/authorization-process-in-detail) authorization process. By the end of this guide, you’ll have a fully functional Vue app running locally with the builder embedded, authenticated, and ready to use—following Vue best practices.

Reference the [following GitHub repository](https://github.com/BeefreeSDK/beefree-vue-demo) with the complete code for this project to follow along in this Vue.js Quickstart Guide.

{% @github-files/github-code-block %}

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

    const response = await fetch('http://localhost:3001/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' })
      })
    
    const token = await response.json();

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

The Beefree SDK requires authentication via Client ID and Client Secret, which must not be exposed in frontend code. The proxy server allows you to:

* Keep credentials safe
* Fetch access tokens securely

The `.env.example` file in the root of the GitHub repository includes an example of a `.env` file. To create a .env file, rename this file to `.env`. Copy and paste your credentials from the Beefree SDK Developer Console securely into the file's placeholders. The following code shows an example of what these placeholders look like inside the file.

```javascript
BEE_CLIENT_ID='YOUR-CLIENT-ID'
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'
```

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
import dotenv from 'dotenv'
dotenv.config()
const BEE_CLIENT_ID = process.env.BEE_CLIENT_ID
const BEE_CLIENT_SECRET = process.env.BEE_CLIENT_SECRET

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
