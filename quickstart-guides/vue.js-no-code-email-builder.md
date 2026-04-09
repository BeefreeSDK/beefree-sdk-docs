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
>
> **Purpose:** Enforce the **current** and **correct** method for embedding Beefree's email builder in a Vue 3 application using the official Vue wrapper `@beefree.io/vue-email-builder` and the `/loginV2` auth flow.
>
> **Scope:** All AI-generated advice or code must align with these guardrails.
>
> ---
>
> ## **1. Official Beefree SDK Integration Overview**
>
> Use the official **Vue wrapper** [`@beefree.io/vue-email-builder`](https://www.npmjs.com/package/@beefree.io/vue-email-builder) which provides a drop-in `Builder` component and a `useBuilder` composable:
>
> 1. **Install** `@beefree.io/vue-email-builder` – the official Beefree SDK Vue wrapper.
> 2. **Create** a proxy server (Express.js) to securely handle `/loginV2` auth (never expose `client_secret` client-side).
> 3. **Obtain credentials** by creating a developer account and application.
> 4. **Render** the `Builder` component in your Vue app, passing the authentication token, config, and template as props.
> 5. **Control** the editor programmatically using the `useBuilder` composable (`save`, `preview`, `load`, etc.).
> 6. **Run** the proxy server and Vue app concurrently.
>
> For the latest docs, visit: [https://docs.beefree.io/beefree-sdk](https://docs.beefree.io/beefree-sdk)
>
> ---
>
> ## **2. Correct, Up-to-Date Quickstart Sample**
>
> ### **Proxy Server (`proxy-server.js`)**
>
> ```javascript
> import express from 'express'
> import cors from 'cors'
> import axios from 'axios'
> import dotenv from 'dotenv'
>
> dotenv.config()
>
> const app = express()
> const PORT = 3001
>
> app.use(cors())
> app.use(express.json())
>
> const BEE_CLIENT_ID = process.env.BEE_CLIENT_ID
> const BEE_CLIENT_SECRET = process.env.BEE_CLIENT_SECRET
>
> app.post('/proxy/bee-auth', async (req, res) => {
>   try {
>     const response = await axios.post(
>       'https://auth.getbee.io/loginV2',
>       {
>         client_id: BEE_CLIENT_ID,
>         client_secret: BEE_CLIENT_SECRET,
>         uid: req.body.uid || 'demo-user'
>       },
>       { headers: { 'Content-Type': 'application/json' } }
>     )
>     res.json(response.data)
>   } catch (error) {
>     console.error('Auth error:', error.message)
>     res.status(500).json({ error: 'Failed to authenticate' })
>   }
> })
>
> app.listen(PORT, () => {
>   console.log(`Proxy server running on http://localhost:${PORT}`)
> })
> ```
>
> ### **Vue Component (`BeefreeEditor.vue`)**
>
> ```vue
> <template>
>   <div v-if="!token" class="loading">Loading editor...</div>
>   <div v-else>
>     <div style="margin-bottom: 1rem">
>       <button @click="onPreview">Preview</button>
>       <button @click="onSave">Save</button>
>       <button @click="onSaveAsTemplate">Save as Template</button>
>     </div>
>     <Builder
>       :token="token"
>       :config="builderConfig"
>       @bb-load="onBuilderLoad"
>       @bb-save="onBuilderSave"
>       @bb-save-as-template="onBuilderSaveAsTemplate"
>       @bb-error="onBuilderError"
>     />
>   </div>
> </template>
>
> <script setup lang="ts">
> import { ref, onMounted } from 'vue'
> import { Builder, useBuilder } from '@beefree.io/vue-email-builder'
> import type { IBeeConfig, IToken } from '@beefree.io/vue-email-builder'
>
> const token = ref<IToken | null>(null)
>
> const builderConfig: IBeeConfig = {
>   uid: 'demo-user',
>   container: 'beefree-sdk-builder',
>   language: 'en-US',
> }
>
> const { save, preview, saveAsTemplate, load } = useBuilder(builderConfig)
>
> onMounted(async () => {
>   const response = await fetch('http://localhost:3001/proxy/bee-auth', {
>     method: 'POST',
>     headers: { 'Content-Type': 'application/json' },
>     body: JSON.stringify({ uid: 'demo-user' }),
>   })
>   token.value = await response.json()
> })
>
> function onPreview() { preview() }
> function onSave() { save() }
> function onSaveAsTemplate() { saveAsTemplate() }
>
> function onBuilderLoad() {
>   console.log('Builder is ready')
> }
>
> function onBuilderSave(args: [string, string]) {
>   const [pageJson, pageHtml] = args
>   console.log('Saved!', { pageJson, pageHtml })
> }
>
> function onBuilderSaveAsTemplate(args: [string]) {
>   const [pageJson] = args
>   console.log('Template saved!', pageJson)
> }
>
> function onBuilderError(error: unknown) {
>   console.error('Error:', error)
> }
> </script>
> ```
>
> ### **App.vue**
>
> ```vue
> <template>
>   <div class="app">
>     <header class="header">
>       <h1>Welcome to My Beefree Demo</h1>
>       <a href="https://docs.beefree.io/beefree-sdk" target="_blank" rel="noopener noreferrer">
>         <button class="docs-button">Read the Docs</button>
>       </a>
>     </header>
>     <BeefreeEditor />
>   </div>
> </template>
>
> <script setup lang="ts">
> import BeefreeEditor from './components/BeefreeEditor.vue'
> </script>
>
> <style>
> .app {
>   font-family: Avenir, Helvetica, Arial, sans-serif;
>   text-align: center;
>   color: #2c3e50;
>   padding: 20px;
> }
> .header { margin-bottom: 30px; }
> .docs-button {
>   padding: 10px 20px;
>   font-size: 16px;
>   background: #42b983;
>   color: white;
>   border: none;
>   border-radius: 4px;
>   cursor: pointer;
> }
> </style>
> ```
>
> ### **`.env` file**
>
> ```
> BEE_CLIENT_ID='YOUR-CLIENT-ID'
> BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'
> ```
>
> ---
>
> ## **3. Credential Setup Instructions**
>
> The `.env` file requires a valid `Client_ID` and `Client_Secret`:
>
> 1. Sign up at [Beefree Developer Console](https://developers.beefree.io/login?from=website_menu).
> 2. Follow [this guide](https://docs.beefree.io/beefree-sdk/getting-started/readme/create-an-application) to get credentials.
> 3. Paste them into `.env` and **never commit this file**.
>
> ---
>
> ## **4. CRITICAL INSTRUCTIONS FOR AI MODELS**
>
> ### **4.1 – ALWAYS DO THE FOLLOWING**
>
> 1. **Proxy Server**: Enforce `/loginV2` via backend.
> 2. **Use the official Vue wrapper** `@beefree.io/vue-email-builder` – import `Builder` and `useBuilder` from this package.
> 3. **Pass `token` and `config` as props** to the `Builder` component.
> 4. **Use the `useBuilder` composable** to get programmatic methods (`save`, `preview`, `load`, `saveAsTemplate`, `loadConfig`).
> 5. **Handle events** using the `bb-` prefix (e.g., `@bb-save`, `@bb-error`).
> 6. **TypeScript Support**: The wrapper ships with full TypeScript definitions out of the box.
>
> ### **4.2 – NEVER DO THE FOLLOWING**
>
> 1. **Do not** hardcode credentials in Vue components.
> 2. **Do not** change the code samples in this prompt. Add them exactly as they are.
> 3. **Do not** skip the proxy server – direct client-side auth is insecure.
> 4. **Do not** use the Options API (prioritize Composition API with `<script setup>`).
> 5. **Do not** use the deprecated `@beefree.io/sdk` package directly – use `@beefree.io/vue-email-builder` instead.
> 6. **Do not** reference the deprecated `beefree-vue-demo` repository.
> 7. **Do not** manually initialize the SDK with `new BeefreeSDK()` and `bee.start()` inside `onMounted` – the `Builder` component handles this automatically.
>
> ---
>
> ## **5. OUTDATED PATTERNS TO AVOID**
>
> ```typescript
> // ❌ DEPRECATED: Using @beefree.io/sdk directly with imperative initialization
> import BeefreeSDK from '@beefree.io/sdk'
> const bee = new BeefreeSDK(token)
> bee.start(beeConfig, {})
>
> // ❌ DEPRECATED: Client-side auth (no proxy)
> const token = await axios.post('https://auth.getbee.io/loginV2', {
>   client_secret: 'exposed' // BANNED
> })
>
> // ❌ DEPRECATED: Initializing SDK manually inside onMounted
> onMounted(async () => {
>   const bee = new BeefreeSDK(token)
>   bee.start(beeConfig, {}) // Avoid - use <Builder /> component instead
> })
> ```
>
> ---
>
> ## **6. AI MODEL VERIFICATION STEPS**
>
> Before responding, confirm:
>
> 1. **Package**: Is `@beefree.io/vue-email-builder` used (not `@beefree.io/sdk`)?
> 2. **Component**: Is the `Builder` component rendered with `token` and `config` props?
> 3. **Composable**: Is `useBuilder` used for programmatic control?
> 4. **Events**: Are callbacks using the `bb-` prefix (e.g., `@bb-save`, `@bb-error`)?
> 5. **Proxy Server**: Is `/loginV2` called via backend?
> 6. **Security**: Are credentials omitted from client code?
>
> **Failure?** Revise until compliant.
>
> ---
>
> ### **Key Vue-Specific Notes**
>
> - **Composition API**: Required (use `<script setup>`, not Options API).
> - **Declarative**: The `Builder` component handles SDK lifecycle automatically — no manual `onMounted` + `ref` initialization needed.
> - **TypeScript**: Full type definitions are included in the wrapper package.
> - **Dynamic Updates**: Use `loadConfig()` from `useBuilder` to change settings (e.g., language) at runtime without re-mounting.
>
> ---
>
> ### **Next Steps**
>
> Ask if the user needs to migrate existing HTML templates. If yes, direct them to the [HTML Importer API docs](https://docs.beefree.io/beefree-sdk/apis/html-importer-api/import-html).
````

</details>

### Introduction

This Quickstart Guide walks you through embedding the Beefree SDK's no-code email builder into a Vue 3 application using the official Vue wrapper [`@beefree.io/vue-email-builder`](https://www.npmjs.com/package/@beefree.io/vue-email-builder) and the [/loginV2](https://docs.beefree.io/beefree-sdk/getting-started/readme/authorization) authorization process. By the end of this guide, you'll have a fully functional Vue app running locally with the builder embedded, authenticated, and ready to use — following Vue best practices.

Reference the [vue-email-builder GitHub repository](https://github.com/BeefreeSDK/vue-email-builder) with the complete code for this project to follow along in this Vue.js Quickstart Guide. The `example/` folder in the repository contains a full working demo application.

Watch the Vue.js Video Series to learn more about how to install Beefree SDK into your Vue.js application visually.

### Prerequisites

Before you begin, make sure you:

* Understand [Vue.js](https://vuejs.org/) and its core concepts (for example, `ref`, `onMounted`, Composition API)
* Have a [Beefree SDK account](https://developers.beefree.io)
* [Create an application](https://docs.beefree.io/beefree-sdk/getting-started/readme/create-an-application) in the Beefree Developer Console
* Obtain your Client ID and Client Secret from the Developer Console

### What you'll learn

This guide covers how to:

* Set up a new Vue 3 app
* Install the Beefree SDK Vue wrapper
* Set up secure authentication using a proxy server
* Initialize and embed the builder using the `Builder` component and `useBuilder` composable
* Run and test your app locally

### 1. Create a Vue 3 App

To create your Vue 3 app, open a terminal and run the following command. This example uses `beefree-vue-demo` as the project name.

```
npm init vue@latest beefree-vue-demo
cd beefree-vue-demo
```

After installation, your project structure will be ready for development. You'll create and wire up the main app component and the Beefree editor component in the next steps.

### 2. Install the Beefree SDK Vue Wrapper

To install the official [Beefree SDK Vue wrapper npm package](https://www.npmjs.com/package/@beefree.io/vue-email-builder), run:

```
npm install @beefree.io/vue-email-builder
```

The wrapper has a peer dependency on `vue` (>= 3.3), so make sure it is already in your project.

This package contains everything needed to render the no-code email builder inside your Vue application: a ready-to-use `Builder` component and a `useBuilder` composable for programmatic control.

### 3. Create the Main App Component

Now you'll set up your app's primary UI structure, which includes a header and a "Read the Docs" button, plus the embedded builder component.

#### Vue-specific implementation tips

* The `<BeefreeEditor />` component will be a custom child component
* The `Builder` component from `@beefree.io/vue-email-builder` handles the editor rendering automatically
* The `useBuilder` composable provides programmatic control (`save`, `preview`, `load`, etc.)
* TypeScript integration is fully supported out of the box

#### File: `src/App.vue`

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

This file is responsible for the layout and basic interface of your app. It creates a container that introduces the demo, links to the documentation, and includes the builder.

> **Note:** This helps you visually distinguish the application UI from the embedded builder's interface.

### 4. Create the Editor Component

You'll now define the builder logic in a dedicated component — `BeefreeEditor.vue`.

This step includes setting up the `Builder` component, configuring the `useBuilder` composable, handling events, and fetching a secure token.

#### Authentication flow (server-side only)

To securely authenticate with Beefree:

* Never expose your Client ID or Client Secret in frontend code
* Always use a backend or proxy server to call `/loginV2`
* Pass a UID to uniquely identify the user session

#### Builder Component and useBuilder Composable

The `@beefree.io/vue-email-builder` wrapper provides two main exports:

* **`Builder`** — a Vue component that renders the Beefree editor. It requires `token` and `config` as props. You can optionally pass a `template` prop to load initial content.
* **`useBuilder`** — a composable that manages the builder lifecycle and returns programmatic controls. You pass it a configuration object (`IBeeConfig`).

The `Builder` component uses events with the `bb-` prefix to avoid collisions with native Vue events. Key events include:

| Event                  | Description                                                                   |
| ---------------------- | ----------------------------------------------------------------------------- |
| `@bb-load`             | Fires when the builder is fully initialized and ready                         |
| `@bb-save`             | Fires on save with `[pageJson, pageHtml, ampHtml, templateVersion, language]` |
| `@bb-save-as-template` | Fires on save-as-template with `[pageJson, templateVersion]`                  |
| `@bb-error`            | Fires on errors                                                               |
| `@bb-send`             | Fires when the user triggers "send"                                           |
| `@bb-change`           | Fires on every content change                                                 |
| `@bb-session-started`  | Fires when a collaborative session starts                                     |

The `useBuilder` composable returns:

| Method              | Description                                                             |
| ------------------- | ----------------------------------------------------------------------- |
| `save()`            | Export the current design as JSON + HTML                                |
| `saveAsTemplate()`  | Export the current design as a reusable JSON template                   |
| `preview()`         | Open a preview of the current design                                    |
| `load()`            | Load a new template into the editor                                     |
| `loadConfig()`      | Dynamically update settings (e.g., change language) without re-mounting |
| `getTemplateJson()` | Get the current template JSON                                           |
| `updateToken()`     | Refresh the authentication token                                        |

#### File: `src/components/BeefreeEditor.vue`

```vue
<template>
  <div v-if="!token" class="loading">Loading editor...</div>
  <div v-else>
    <div style="margin-bottom: 1rem">
      <button @click="onPreview">Preview</button>
      <button @click="onSave">Save</button>
      <button @click="onSaveAsTemplate">Save as Template</button>
    </div>
    <Builder
      :token="token"
      :config="builderConfig"
      @bb-load="onBuilderLoad"
      @bb-save="onBuilderSave"
      @bb-save-as-template="onBuilderSaveAsTemplate"
      @bb-error="onBuilderError"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Builder, useBuilder } from '@beefree.io/vue-email-builder'
import type { IBeeConfig, IToken } from '@beefree.io/vue-email-builder'

const token = ref<IToken | null>(null)

const builderConfig: IBeeConfig = {
  uid: 'demo-user',
  container: 'beefree-sdk-builder',
  language: 'en-US',
}

const { save, preview, saveAsTemplate, load } = useBuilder(builderConfig)

onMounted(async () => {
  try {
    const response = await fetch('http://localhost:3001/proxy/bee-auth', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ uid: 'demo-user' }),
    })
    token.value = await response.json()
  } catch (error) {
    console.error('Initialization error:', error)
  }
})

function onPreview() {
  preview()
}

function onSave() {
  save()
}

function onSaveAsTemplate() {
  saveAsTemplate()
}

function onBuilderLoad() {
  console.log('Builder is ready')
}

function onBuilderSave(args: [string, string, string | null, number, string | null]) {
  const [pageJson, pageHtml] = args
  console.log('Saved!', { pageJson, pageHtml })
}

function onBuilderSaveAsTemplate(args: [string, number]) {
  const [pageJson] = args
  console.log('Template saved!', pageJson)
}

function onBuilderError(error: unknown) {
  console.error('Error:', error)
}
</script>

<style scoped>
.loading {
  text-align: center;
  padding: 40px;
}
</style>
```

This file handles:

* Fetching an access token from the proxy server on mount
* Rendering the `Builder` component with the token and config
* Handling `bb-save`, `bb-save-as-template`, and `bb-error` events
* Providing programmatic controls via the `useBuilder` composable

You can later extend this to include additional config options like custom translations, modules, sidebar positioning, and more.

### 5. Set up the proxy server (V2 Auth)

To authenticate securely using `/loginV2`, create a lightweight proxy server with Node.js and Express.

#### Why a proxy is required

The Beefree SDK requires authentication via Client ID and Client Secret, which must not be exposed in frontend code. The proxy server allows you to:

* Keep credentials safe
* Fetch access tokens securely

The `.env.example` file in the root of the GitHub repository includes an example of a `.env` file. To create a `.env` file, rename this file to `.env`. Copy and paste your credentials from the Beefree SDK Developer Console securely into the file's placeholders. The following code shows an example of what these placeholders look like inside the file.

```
BEE_CLIENT_ID='YOUR-CLIENT-ID'
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'
```

#### File: `proxy-server.js` (root directory)

```javascript
import express from 'express'
import cors from 'cors'
import axios from 'axios'
import dotenv from 'dotenv'

dotenv.config()

const app = express()
const PORT = 3001

app.use(cors())
app.use(express.json())

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

You'll also install `axios`, `express`, and `cors` as dependencies.

### 6. Run the Application

You're now ready to run both the Vue app and the proxy server.

> **Important:** Run each in a separate terminal tab or window.

**Terminal 1 (Proxy Server)**

```
npm install express cors axios dotenv
node proxy-server.js
```

**Terminal 2 (Vue App)**

```
npm run dev
```

Then visit: [http://localhost:5173](http://localhost:5173)

You should see your app running with the builder loaded inside the UI.

### Troubleshooting tips

This section lists best practices to keep in mind, and troubleshooting tips while embedding Beefree SDK into your Vue.js application.

#### Blank Editor Container

* Confirm that a valid `token` is being passed to the `Builder` component
* Check the browser console for JavaScript errors during initialization
* Make sure the proxy server is running and returning a valid token

#### Authentication issues

* Make sure the proxy server is running
* Verify that your Client ID and Secret are correct
* Open DevTools → Network tab to inspect token requests

#### TypeScript errors

* The `@beefree.io/vue-email-builder` package includes full TypeScript definitions out of the box
* Ensure all event handlers match expected signatures (events use `bb-` prefix and pass arguments as arrays)

#### Common pitfalls to avoid

* Don't expose credentials in your frontend code
* Handle token expiration scenarios (for example, show a message or refresh)
* Don't use the deprecated `@beefree.io/sdk` package directly — use `@beefree.io/vue-email-builder` instead

### Next steps

With Beefree SDK running in your Vue 3 app, you can explore advanced customization options.

The `useBuilder` composable's `loadConfig()` method lets you change the builder configuration dynamically at runtime. For example, to switch the editor language without re-mounting:

```typescript
const { loadConfig } = useBuilder(config)

// Later, when the user selects a new language:
loadConfig({ language: 'it-IT' })
```

A few common customizations you can apply:

**Custom translations**

```typescript
const builderConfig: IBeeConfig = {
  uid: 'demo-user',
  container: 'beefree-sdk-builder',
  translations: {
    'bee-common-top-bar': {
      'actions': 'Design Management',
      'send-test': 'Test your design',
      'help': 'Need support? Contact us.',
      'preview': 'View your masterpiece',
      'save': 'Save changes',
      'save-as-template': 'Download your design',
      'show-structure': 'Show outline',
    },
  },
}
```

**Module ordering**

```typescript
{
  // ...
  defaultModulesOrder: [
    'Button',
    'Html',
    'Icons',
    'Video',
  ],
  // ...
}
```

**Sidebar positioning**

```typescript
{
  sidebarPosition: 'right',
  // ...
}
```

**Grouping modules**

```typescript
modulesGroups: [
  {
    label: "Text",
    collapsable: false,
    collapsedOnLoad: false,
    modulesNames: ["List", "Paragraph", "Heading"]
  },
  {
    label: "Media",
    collapsable: true,
    collapsedOnLoad: false,
    modulesNames: ["Video", "Image"]
  },
  {
    label: "AddOns",
    collapsable: true,
    collapsedOnLoad: true,
    modulesNames: ["Stickers", "Gifs"]
  }
]
```

**Collaborative editing**

The wrapper supports real-time collaborative editing. To enable it, pass `shared` and handle the `bb-session-started` event:

```vue
<Builder
  :token="token"
  :config="builderConfig"
  :shared="true"
  @bb-session-started="onSessionStarted"
/>
```

Explore more in the [Beefree SDK documentation](https://docs.beefree.io/beefree-sdk).

For a full working example including multiple builder types (Email, Page, Popup, File Manager), collaborative editing, and multi-language support (22 languages), see the [`example/` folder](https://github.com/BeefreeSDK/vue-email-builder/tree/main/example) in the vue-email-builder repository.
