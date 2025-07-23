---
description: >-
  Welcome to the React Quickstart Guide for embedding Beefree SDK's no-code
  email builder in your React application.
---

# React No-code Email Builder

## Introduction

This Quickstart Guide shows you step by step how to embed Beefree SDK’s Email Builder into a React application using the [`/loginV2`](../getting-started/readme/installation/authorization-process-in-detail.md) authorization process. By the end of the guide, you'll have a functional React app running locally, with Beefree SDK's no-code email builder integrated and properly authenticated—following best practices for React development.

Reference the [following GitHub repository](https://github.com/BeefreeSDK/beefree-react-demo) with the complete code for this project to follow along in this React Quickstart Guide.

{% embed url="https://github.com/BeefreeSDK/beefree-react-demo" %}

## **Prerequisites**

Prior to getting started, ensure you:

* Understand the [React framework](https://react.dev/learn) and what it is.
* Have a [Beefree SDK account](https://developers.beefree.io/accounts/login/?from=website_menu).&#x20;
* [Create an application](../getting-started/readme/create-an-application.md) within the Developer Console. &#x20;
  * Obtain your [Client ID and Client Secret](../getting-started/readme/create-an-application.md#obtain-your-client-id-and-client-secret).

## **What You'll Learn**

Throughout this guide, you'll learn how to:

* Create a React app
* Install Beefree SDK in the React app
* Successfully complete the authorization process using `/loginV2`
* Initialize the builder
* Run the React app and the builder

### **1. Create a React App**

First, set up a React app with TypeScript. Navigate to your terminal and run the following commands to create a React app with TypeScript. In the following example, the app is called **beefree-demo**. After creating the app, navigate to its directory.

<pre class="language-bash"><code class="lang-bash"><strong>npm create vite@latest beefree-react-demo -- --template react-ts
</strong>cd beefree-react-demo
npm install
</code></pre>

### **2. Install Beefree SDK**

Run the following command in your terminal to install the official[ Beefree SDK npm package](https://www.npmjs.com/package/@beefree.io/sdk).&#x20;

```bash
npm install @beefree.io/sdk
```

Now that the package is installed, the next step is to create a simple user interface (UI) to embed the builder within.&#x20;

{% hint style="info" %}
**Note (React and Beefree SDK Interaction):** The `@beefree.io/sdk` package provides a React-compatible wrapper for the Beefree builder. React manages the UI lifecycle, while the SDK handles the email builder logic.
{% endhint %}

### **3. Create a Simple UI**

The simple UI for this step is creating a "Read the Docs" Button with a link to the docs site. This serves as a simple visual to see the contrast between the application and builder UI once the app is running locally.&#x20;

Copy and paste the code below in your **`App.tsx`** file to modify it to include a button linking to Beefree SDK's docs. You can use any url you'd like to experiment with this locally, simply replace `href="https://docs.beefree.io/beefree-sdk"` in the code below with your preferred url.&#x20;

#### **Update `App.tsx`**

```tsx
import './App.css';

function DocsButton() {
  return (
    <a 
      href="https://docs.beefree.io/beefree-sdk" 
      target="_blank" 
      rel="noopener noreferrer"
    >
      <button style={{ padding: '10px 20px', fontSize: '16px' }}>
        Read the Docs
      </button>
    </a>
  );
}

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1>Welcome to My Beefree Demo</h1>
        <DocsButton />
      </header>
    </div>
  );
}

export default App;
```

This code uses React concepts that are important to understand. The key React concepts used in the code are the following:

* `DocsButton` is a **functional component**—a reusable UI piece.
* React **renders components** in a [tree structure](https://react.dev/learn/understanding-your-ui-as-a-tree) (`App` → `DocsButton`).

### **4. Set Up the Beefree Editor Component**

Create `src/BeefreeEditor.tsx` to initialize the SDK. Navigate to your `src` directory and add a new file called `BeefreeEditor.tsx`. Copy and paste the following code in this file. This code sets up the Beefree SDK builder component within the React app.

#### **Full `BeefreeEditor.tsx` Code**

```tsx
import { useEffect, useRef } from 'react';
import BeefreeSDK from '@beefree.io/sdk';

export default function BeefreeEditor() {
  const containerRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    async function initializeEditor() {
      // Beefree SDK configuration
      const beeConfig = {
        container: 'beefree-react-demo',
        language: 'en-US',
        onSave: (pageJson: string, pageHtml: string, ampHtml: string | null, templateVersion: number, language: string | null) => {
          console.log('Saved!', { pageJson, pageHtml, ampHtml, templateVersion, language });
        },
        onError: (error: unknown) => {
          console.error('Error:', error);
        }
      };

      // Get a token from your backend
      const response = await fetch('http://localhost:3001/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' })
      })
    
      const token = await response.json();

      // Initialize the editor
      const bee = new BeefreeSDK(token);
      bee.start(beeConfig, {});
    }

    initializeEditor();
  }, []);

  return (
    <div
      id="beefree-react-demo"
      ref={containerRef}
      style={{
        height: '600px',
        width: '90%',
        margin: '20px auto',
        border: '1px solid #ddd',
        borderRadius: '8px'
      }}
    />
  );
}
```

In the code above code, there are a few concepts related to both React and Beefree SDK that are important to be aware of for successfully launching your local environment. These concepts are the following:

* [Beefree SDK initialization](react-no-code-email-builder.md#beefree-sdk-initialization)
* [Container setup with useRef](react-no-code-email-builder.md#container-setup-with-useref)
* [Token Process](react-no-code-email-builder.md#token-process)
* [Beefree SDK Callbacks](react-no-code-email-builder.md#beefree-sdk-callbacks)

The following section discusses these concepts thoroughly.

#### Beefree SDK Initialization

Beefree SDK requires that you create a configuration object in order to initialize and load the builder within your application. In the following code, `beeConfig` represents this. While there are several optional [Configuration Parameters](../getting-started/readme/installation/configuration-parameters/) you can add to your configuration object to customize the builder for your application, there is only one mandatory parameter to successfully launch the Beefree SDK. This is the `container` parameter, which must always be included.

```tsx
useEffect(() => {
    async function initializeEditor() {
      // Beefree SDK configuration
      const beeConfig = {
        container: 'beefree-react-demo',
        language: 'en-US',
        onSave: (pageJson: string, pageHtml: string, ampHtml: string | null, templateVersion: number, language: string | null) => {
          console.log('Saved!', { pageJson, pageHtml, ampHtml, templateVersion, language });
        },
        onError: (error: unknown) => {
          console.error('Error:', error);
        }
      };
```

#### Container Setup with `useRef`

* `const containerRef = useRef<HTMLDivElement>(null)` creates a **reference** to a DOM element.
* The `<div id="bee-plugin-container">` is where Beefree SDK mounts the editor.
* `useEffect` ensures initialization **only runs once** (on component mount).

#### **Token Process**

1. React → Backend (`/proxy/bee-auth`) → [Beefree (`loginV2`)](react-no-code-email-builder.md#id-5.-set-up-the-proxy-server-v2-auth).
2. Beefree SDK returns a token, passed to `new BeefreeSDK(token)`.

#### Beefree SDK Callbacks

* **`onSave`**: Called when a user saves, returning `JSON` (template structure) and `HTML` (rendered output).
* **`onError`**: Handles errors (e.g., token expiration).

### **5. Set Up the Proxy Server (V2 Auth)**

Create `proxy-server.js` in the **root directory**. Copy and paste the code in the following section into the `proxy-server.js` file in the root directory. The following code is responsible for a very important part of running Beefree SDK within your React app, which is authentication and successfully completing the [authorization process](../getting-started/readme/installation/authorization-process-in-detail.md). Beefree SDK requires that you pass a `Client ID`, `Client Secret`, and `UID` on the server-side to successfully complete the authorization process. The following code shows an example of how you can use the `/loginV2` to complete this.   &#x20;

#### **`proxy-server.js`**

```javascript
import express from 'express';
import cors from 'cors';
import axios from 'axios';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
const PORT = 3001;

app.use(cors());
app.use(express.json());

const BEE_CLIENT_ID = process.env.BEE_CLIENT_ID;
const BEE_CLIENT_SECRET = process.env.BEE_CLIENT_SECRET;

// V2 Auth Endpoint
app.post('/proxy/bee-auth', async (req, res) => {
  try {
    const { uid } = req.body;
    
    const response = await axios.post(
      'https://auth.getbee.io/loginV2',
      {
        client_id: BEE_CLIENT_ID,
        client_secret: BEE_CLIENT_SECRET,
        uid: uid || 'demo-user'
      },
      { headers: { 'Content-Type': 'application/json' } }
    );
    
    res.json(response.data);
  } catch (error) {
    console.error('Auth error:', error.message);
    res.status(500).json({ error: 'Failed to authenticate' });
  }
});

app.listen(PORT, () => {
  console.log(`Proxy server running on http://localhost:${PORT}`);
});
```

The `.env.example` file in the root of the GitHub repository includes an example of a `.env` file. To create a .env file, rename this file to `.env`. Copy and paste your credentials from the Beefree SDK Developer Console securely into the file's placeholders. The following code shows an example of what these placeholders look like inside the file.

```javascript
BEE_CLIENT_ID='YOUR-CLIENT-ID'
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'
```

#### **Run the Proxy Server**

Once the authorization process is complete, it is important to run the proxy sever prior to launching the frontend. Run the following commands in your terminal to complete this step.

```bash
npm install express cors axios dotenv
node proxy-server.js
```

### **6. Update `App.tsx` to Include the Editor**

Now that the [Beefree SDK editor component](react-no-code-email-builder.md#id-4.-set-up-the-beefree-editor-component) is set up and so is the [proxy server](react-no-code-email-builder.md#id-5.-set-up-the-proxy-server-v2-auth), the `App.tsx` file can be updated to include the Beefree SDK builder. Copy and paste the following code into the `App.tsx` file to update it accordingly.

```tsx
import './App.css';
import BeefreeEditor from './BeefreeEditor';

function DocsButton() {
  return (
    <a 
      href="https://docs.beefree.io/beefree-sdk" 
      target="_blank" 
      rel="noopener noreferrer"
    >
      <button style={{ padding: '10px 20px', fontSize: '16px' }}>
        Read the Docs
      </button>
    </a>
  );
}

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1>Welcome to My Beefree Demo</h1>
        <DocsButton />
        <BeefreeEditor />
      </header>
    </div>
  );
}

export default App;
```

### **7. Run the App**

The final step is to run the application. Keep in mind that the proxy server needs to run in its own terminal, while the application runs in a separate terminal.

The terminal commands for running the application and proxy server are the following:

*   **Terminal 1 (React):**

    ```bash
    npm run dev
    ```
*   **Terminal 2 (Proxy):**

    ```bash
    node proxy-server.js
    ```

Now you can visit [**http://localhost:3000**](http://localhost:3000) and start experimenting with your new React application with Beefree SDK embedded. The following image shows what the final result should look like:

<figure><img src="../.gitbook/assets/CleanShot 2025-07-11 at 17.48.08@2x.png" alt=""><figcaption></figcaption></figure>

### **Summary**

Now you have a functional React app running locally, with Beefree SDK's no-code email builder integrated and properly authenticated—following best practices for React development.&#x20;

Remember the following core concepts covered throughout this guide to easily integrate Beefree SDK into your React application:

* **React Components**: Reusable UI (e.g., `DocsButton`, `BeefreeEditor`).
* **Beefree SDK**: Loads in a `useRef` container, with callbacks for `save/error`.
* **V2 Auth**: Securely handles tokens via a proxy server.
* **Proxy Server**: Must be in the **root directory** (`proxy-server.js`).

### **Next Steps**

Beefree SDK is highly customizable. Now that you have a React application running locally on your machine with the Beefree SDK Email Builder embedded, you can start experimenting with customizing the UI of the email of the builder.

A few common customizations you can easily apply to your [`beeConfig` object](react-no-code-email-builder.md#id-4.-set-up-the-beefree-editor-component) to continue experimenting are the following:

* [Custom Languages](../other-customizations/advanced-options/custom-languages.md) and overriding default text

```javascript
const beeConfig = {
  container: 'beefree-container',
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
```

* [Content Tile Sorting](../other-customizations/appearance/content-tile-sorting.md)

```javascript
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

* [Content Tile Grouping](../other-customizations/appearance/content-tile-grouping.md)

<pre class="language-javascript"><code class="lang-javascript"><strong>modulesGroups: [
</strong>  {
    label: "Text ✏️",
    collapsable: false,
    collapsedOnLoad: false,
    modulesNames: [
      "List",
      "Paragraph",
      "Heading"
    ]
  },
  {
    label: "Media",
    collapsable: true,
    collapsedOnLoad: false,
    modulesNames: [
      "Video",
      "Image"
    ]
  },
  {
    label: "AddOns",
    collapsable: true,
    collapsedOnLoad: true,
    modulesNames: [
      "Stickers",
      "Gifs"
    ]
  }
]
</code></pre>

* [Custom Sidebar Position](../other-customizations/appearance/custom-sidebar-position.md)

<pre class="language-javascript"><code class="lang-javascript"><strong>var beeConfig = {
</strong>        sidebarPosition: 'right',
        ...  
</code></pre>

Explore the [technical documentation](https://docs.beefree.io/beefree-sdk) to learn more about the other customization options within Beefree SDK.
