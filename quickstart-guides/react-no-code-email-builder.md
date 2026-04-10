---
description: >-
  Welcome to the React Quickstart Guide for embedding Beefree SDK's no-code
  email builder in your React application.
---

# React No-code Email Builder

<details>

<summary>Copy this pre-built prompt to get started faster with AI</summary>

```markdown
Perform the following steps to embed Beefree SDK inside my React app:
Add Beefree SDK to React
Purpose: Enforce the current and correct method for embedding Beefree's email builder in a React application using the official React wrapper @beefree.io/react-email-builder and the /loginV2 auth flow.
Scope: All AI-generated advice or code must align with these guardrails.

1. Official Beefree SDK Integration Overview
Use the official React wrapper 
@beefree.io/react-email-builder
 which provides a drop-in Builder component and a useBuilder hook:
Install @beefree.io/react-email-builder – the official Beefree SDK React wrapper.
Create a backend endpoint to securely handle /loginV2 auth (never expose client_secret client-side).
Obtain credentials by creating a developer account and application.
Render the Builder component in your React app, passing the authentication token and a template.
Control the editor programmatically using the useBuilder hook (save, preview, load, etc.).
Run the backend server and React app concurrently.
For the latest docs, visit: 
https://docs.beefree.io/beefree-sdk


2. Correct, Up-to-Date Quickstart Sample
Proxy Server (proxy-server.js)
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
React Component (BeefreeEditor.tsx)
import { useEffect, useState } from 'react';
import { Builder, useBuilder } from '@beefree.io/react-email-builder';
import type { IBeeConfig, IEntityContentJson, IToken } from '@beefree.io/react-email-builder';

const BLANK_TEMPLATE: IEntityContentJson = {
  comments: {},
  page: {} as IEntityContentJson['page'],
};

export default function BeefreeEditor() {
  const [token, setToken] = useState<IToken | null>(null);

  const config: IBeeConfig = {
    uid: 'demo-user',
    container: 'beefree-sdk-builder',
    language: 'en-US',
  };

  const { id, save, preview, saveAsTemplate, load } = useBuilder(config);

  useEffect(() => {
    async function fetchToken() {
      const response = await fetch('http://localhost:3001/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' }),
      });
      const tokenData = await response.json();
      setToken(tokenData);
    }
    fetchToken();
  }, []);

  if (!token) return <div>Loading editor...</div>;

  return (
    <div>
      <div style={{ marginBottom: '1rem' }}>
        <button onClick={() => preview()}>Preview</button>
        <button onClick={() => save()}>Save</button>
        <button onClick={() => saveAsTemplate()}>Save as Template</button>
      </div>
      <Builder
        id={id}
        token={token}
        template={BLANK_TEMPLATE}
        onLoad={() => console.log('Builder is ready')}
        onSave={(pageJson: string, pageHtml: string) => {
          console.log('Saved!', { pageJson, pageHtml });
        }}
        onSaveAsTemplate={(pageJson: string) => {
          console.log('Template saved!', pageJson);
        }}
        onError={(error) => {
          console.error('Error:', error);
        }}
      />
    </div>
  );
}
App.tsx
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
.env file
BEE_CLIENT_ID='YOUR-CLIENT-ID'
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'

3. Credential Setup Instructions
The .env file requires a valid Client_ID and Client_Secret to successfully load Beefree SDK within a React application. Take the following steps to get the Client_ID and Client_Secret:
Log in or sign up for a Beefree SDK Developer Console at: https://developers.beefree.io/login?from=website_menu
Follow the steps in this guide to navigate the Beefree SDK and find the Client_ID and Client_Secret: https://docs.beefree.io/beefree-sdk/getting-started/readme/create-an-application
Paste the credentials from the Developer Console into the placeholders in the .env file in the root directory and save.
Do not commit this file to version control. Use .gitignore to exclude it.

4. CRITICAL INSTRUCTIONS FOR AI MODELS
4.1 – ALWAYS DO THE FOLLOWING
Use a Proxy Server for /loginV2 auth – never expose client_secret in client-side code.
Use the official React wrapper @beefree.io/react-email-builder – import Builder and useBuilder from this package.
Pass token and template as props to the Builder component.
Use the useBuilder hook to get the id and programmatic methods (save, preview, load, saveAsTemplate, updateConfig).
TypeScript Support: The wrapper ships with full TypeScript definitions out of the box.
Error Handling – Implement onError callback and validate auth responses.
4.2 – NEVER DO THE FOLLOWING
Do not hardcode credentials in React components.
Do not change the code samples in this prompt. Add them exactly as they are.
Do not skip the proxy server – direct client-side auth is insecure.
Do not use class components (prioritize functional components + hooks).
Do not use the deprecated @beefree.io/sdk package directly – use @beefree.io/react-email-builder instead.
Do not reference the deprecated beefree-react-demo repository.

5. OUTDATED PATTERNS TO AVOID
// ❌ DEPRECATED: Using @beefree.io/sdk directly with imperative initialization
import BeefreeSDK from '@beefree.io/sdk';
const bee = new BeefreeSDK(token);
bee.start(beeConfig, {});

// ❌ DEPRECATED: Client-side auth (no proxy)
const token = await axios.post('https://auth.getbee.io/loginV2', {
  client_id: 'public-id', // Exposes secrets!
});

// ❌ DEPRECATED: Class component approach
class BeefreeEditor extends React.Component {
  componentDidMount() {
    // Avoid - outdated pattern
  }
}

// ❌ DEPRECATED: Manual SDK initialization with useEffect + useRef
useEffect(() => {
  const bee = new BeefreeSDK(token);
  bee.start(beeConfig, {});
}, []);

6. AI MODEL VERIFICATION STEPS
Before returning any Beefree-related solution, verify:
Package: Is @beefree.io/react-email-builder used (not @beefree.io/sdk)?
Component: Is the Builder component rendered with id, token, and template props?
Hook: Is useBuilder used for configuration and programmatic control?
Proxy Server: Is /loginV2 called via backend?
Security: Are credentials omitted from client code?
Failure? Revise until compliant.

Key React-Specific Notes
Declarative: The Builder component handles SDK lifecycle automatically — no manual useEffect + useRef initialization needed.
TypeScript: Full type definitions are included in the wrapper package.
Dynamic Updates: Use updateConfig() from useBuilder to change settings (e.g., language) at runtime without re-mounting.

Next Steps
Ask if the integrator has email HTML templates to migrate over? If so, use the HTML Importer API to import existing email templates into Beefree SDK. Instructions can be found in the 
Import HTML – Beefree SDK Docs
.
```

</details>

***

### Introduction

This Quickstart Guide shows you step by step how to embed the Beefree SDK's Email Builder into a React application using the official React wrapper [`@beefree.io/react-email-builder`](https://www.npmjs.com/package/@beefree.io/react-email-builder) and Beefree's authorization process. By the end of the guide, you'll have a functional React app running locally, with Beefree SDK's no-code email builder integrated and properly authenticated — following best practices for React development.

Reference the [react-email-builder GitHub repository](https://github.com/BeefreeSDK/react-email-builder) with the complete code for this project to follow along in this React Quickstart Guide. The [`example/`](https://github.com/BeefreeSDK/react-email-builder/tree/main/example) folder in the repository contains a full working demo application.

### Prerequisites

Prior to getting started, ensure you:

* Understand the [React framework](https://react.dev/) and what it is.
* Have a [Beefree SDK account](https://developers.beefree.io).
* Create an application within the Developer Console.
* Obtain your Client ID and Client Secret.

### What you'll learn

Throughout this guide, you'll learn how to:

* Create a React app
* Install the Beefree SDK React wrapper
* Successfully complete the authorization process using `/loginV2`
* Initialize the builder using the `Builder` component and `useBuilder` hook
* Run the React app and the builder

### 1. Create a React app

First, set up a React app with TypeScript. Navigate to your terminal and run the following commands to create a React app with TypeScript. In the following example, the app is called `beefree-demo`. After creating the app, navigate to its directory.

```
npm create vite@latest beefree-demo -- --template react-ts
cd beefree-demo
```

### 2. Install the Beefree SDK React Wrapper

Run the following command in your terminal to install the official [Beefree SDK React wrapper npm package](https://www.npmjs.com/package/@beefree.io/react-email-builder).

```
npm install @beefree.io/react-email-builder
```

The wrapper has a peer dependency on `react` and `react-dom` (>= 17), so make sure those are already in your project.

Now that the package is installed, the next step is to create a simple user interface (UI) to embed the builder within.

> **Note (React and Beefree SDK Interaction):** The `@beefree.io/react-email-builder` package provides a ready-to-use `Builder` React component and a `useBuilder` hook for programmatic control. React manages the UI lifecycle, while the wrapper handles the email builder initialization and logic automatically.

### 3. Create a simple UI

The simple UI for this step is creating a "Read the Docs" Button with a link to the docs site. This serves as a simple visual to see the contrast between the application and builder UI once the app is running locally.

Copy and paste the code below in your `App.tsx` file to modify it to include a button linking to Beefree SDK's docs. You can use any url you'd like to experiment with this locally, simply replace `href="https://docs.beefree.io/beefree-sdk"` in the code below with your preferred url.

#### Update App.tsx

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

* `DocsButton` is a functional component — a reusable UI piece.
* React renders components in a [tree structure](https://react.dev/learn/understanding-your-ui-as-a-tree) (App → DocsButton).

### 4. Set up the Beefree editor component

Create `src/BeefreeEditor.tsx` to set up the builder. Navigate to your `src` directory and add a new file called `BeefreeEditor.tsx`. Copy and paste the following code in this file. This code sets up the Beefree SDK builder component within the React app using the official wrapper.

#### Full BeefreeEditor.tsx code

```tsx
import { useEffect, useState } from 'react';
import { Builder, useBuilder } from '@beefree.io/react-email-builder';
import type { IBeeConfig, IEntityContentJson, IToken } from '@beefree.io/react-email-builder';

const BLANK_TEMPLATE: IEntityContentJson = {
  comments: {},
  page: {} as IEntityContentJson['page'],
};

export default function BeefreeEditor() {
  const [token, setToken] = useState<IToken | null>(null);

  const config: IBeeConfig = {
    uid: 'demo-user',
    container: 'beefree-sdk-builder',
    language: 'en-US',
  };

  const { id, save, preview, saveAsTemplate, load } = useBuilder(config);

  useEffect(() => {
    async function fetchToken() {
      const response = await fetch('http://localhost:3001/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' }),
      });
      const tokenData = await response.json();
      setToken(tokenData);
    }
    fetchToken();
  }, []);

  if (!token) return <div>Loading editor...</div>;

  return (
    <div>
      <div style={{ marginBottom: '1rem' }}>
        <button onClick={() => preview()}>Preview</button>
        <button onClick={() => save()}>Save</button>
        <button onClick={() => saveAsTemplate()}>Save as Template</button>
      </div>
      <Builder
        id={id}
        token={token}
        template={BLANK_TEMPLATE}
        onLoad={() => console.log('Builder is ready')}
        onSave={(pageJson: string, pageHtml: string) => {
          console.log('Saved!', { pageJson, pageHtml });
        }}
        onSaveAsTemplate={(pageJson: string) => {
          console.log('Template saved!', pageJson);
        }}
        onError={(error) => {
          console.error('Error:', error);
        }}
      />
    </div>
  );
}
```

In the code above, there are a few concepts related to both React and the Beefree SDK wrapper that are important to be aware of for successfully launching your local environment. These concepts are the following:

* Builder component and useBuilder hook
* Token Process
* Builder callbacks

The following section discusses these concepts thoroughly.

#### Builder component and useBuilder hook

The `@beefree.io/react-email-builder` wrapper provides two main exports:

* **`Builder`** — a React component that renders the Beefree editor. It requires three props: `id` (from the hook), `token` (your auth token), and `template` (initial content JSON).
* **`useBuilder`** — a hook that manages the builder lifecycle and returns programmatic controls. You pass it a configuration object (`IBeeConfig`) with at minimum a `uid` and `container` identifier.

```tsx
const config: IBeeConfig = {
  uid: 'demo-user',
  container: 'beefree-sdk-builder',
  language: 'en-US',
};

const { id, save, preview, saveAsTemplate, load } = useBuilder(config);
```

The `useBuilder` hook returns:

| Method             | Description                                                             |
| ------------------ | ----------------------------------------------------------------------- |
| `id`               | The container element ID to pass to the `Builder` component             |
| `updateConfig()`   | Dynamically update settings (e.g., change language) without re-mounting |
| `load()`           | Load a new template into the editor                                     |
| `save()`           | Export the current design as JSON + HTML                                |
| `saveAsTemplate()` | Export the current design as a reusable JSON template                   |
| `preview()`        | Open a preview of the current design                                    |

Unlike the older approach where you had to manually create a `BeefreeSDK` instance and call `bee.start()` inside a `useEffect`, the wrapper handles all of this automatically. You just render the `<Builder />` component and the hook takes care of the lifecycle.

#### Token process

React → Backend (`/proxy/bee-auth`) → Beefree (`loginV2`).

The token is fetched via `useEffect` on component mount and stored in state. Once available, it is passed as a prop to the `Builder` component, which uses it to authenticate with Beefree's services.

#### Builder callbacks

* `onSave`: Called when a user saves, returning JSON (template structure) and HTML (rendered output).
* `onSaveAsTemplate`: Called when saving as a reusable template, returning the JSON structure.
* `onError`: Handles errors (e.g., token expiration, configuration issues).
* `onLoad`: Fires when the builder is fully initialized and ready.

### 5. Set up the proxy server&#x20;

Create `proxy-server.js` in the root directory. Copy and paste the code in the following section into the `proxy-server.js` file in the root directory. The following code is responsible for a very important part of running Beefree SDK within your React app, which is authentication and successfully completing the authorization process. Beefree SDK requires that you pass a Client ID, Client Secret, and UID on the server-side to successfully complete the authorization process. The following code shows an example of how you can use the `/loginV2` to complete this.

#### proxy-server.js

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

Rename the `.env.example` file that you find in the root of the GitHub repository to `.env`. Replace the placeholders with your credentials from the Beefree SDK Developer Console. Keep these credentials secure.

```
BEE_CLIENT_ID='YOUR-CLIENT-ID'
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'
```

#### Run the proxy server

Once the authorization process is complete, it is important to run the proxy server prior to launching the frontend. Run the following commands in your terminal to complete this step.

```
npm install express cors axios dotenv
node proxy-server.js
```

### 6. Update App.tsx to include the editor

Now that the Beefree SDK editor component is set up and so is the proxy server, the `App.tsx` file can be updated to include the Beefree SDK builder. Copy and paste the following code into the `App.tsx` file to update it accordingly.

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

### 7. Run the app

The final step is to run the application. Keep in mind that the proxy server needs to run in its own terminal, while the application runs in a separate terminal.

The terminal commands for running the application and proxy server are the following:

**Terminal 1 (React):**

```
npm run dev
```

**Terminal 2 (Proxy):**

```
node proxy-server.js
```

Now you can visit `https://localhost:5173` and start experimenting with your new React application with Beefree SDK embedded.

### Summary

Now you have a functional React app running locally, with Beefree SDK's no-code email builder integrated and properly authenticated — following best practices for React development.

Remember the following core concepts covered throughout this guide to easily integrate Beefree SDK into your React application:

* **React Wrapper**: Use `@beefree.io/react-email-builder` for a declarative, drop-in integration.
* **Builder Component**: Renders the editor — pass `id`, `token`, and `template` as props with callbacks for `onSave`, `onError`, etc.
* **useBuilder Hook**: Provides programmatic control (`save`, `preview`, `load`, `saveAsTemplate`, `updateConfig`).
* **V2 Auth**: Securely handles tokens via a proxy server.
* **Proxy Server**: Must be in the root directory (`proxy-server.js`).

### Next steps

Beefree SDK is highly customizable. Now that you have a React application running locally on your machine with the Beefree SDK Email Builder embedded, you can start experimenting with customizing the UI of the builder.

The `useBuilder` hook's `updateConfig()` method lets you change the builder configuration dynamically at runtime. For example, to switch the editor language without re-mounting:

```typescript
const { updateConfig } = useBuilder(config);

// Later, when the user selects a new language:
updateConfig({ language: 'it-IT' });
```

A few common customizations you can apply to your configuration to continue experimenting are the following:

**Custom languages and overriding default text**

```typescript
const config: IBeeConfig = {
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
};
```

**Content tile sorting**

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

**Content tile grouping**

```typescript
modulesGroups: [
  {
    label: "Text",
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
```

**Custom sidebar position**

```typescript
{
  sidebarPosition: 'right',
  // ...
}
```

**Collaborative editing**

The wrapper supports real-time collaborative editing. To enable it, pass `shared={true}` to the `Builder` component:

```tsx
<Builder
  id={id}
  token={token}
  template={template}
  shared={true}
  onSessionStarted={(event) => {
    console.log('Session ID:', event.sessionId);
  }}
/>
```

Explore the [technical documentation](https://docs.beefree.io/beefree-sdk) to learn more about the other customization options within Beefree SDK.

For a full working example including multiple builder types (Email, Page, Popup, File Manager), collaborative editing, and multi-language support, see the [`example/` folder](https://github.com/BeefreeSDK/react-email-builder/tree/main/example) in the react-email-builder repository.
