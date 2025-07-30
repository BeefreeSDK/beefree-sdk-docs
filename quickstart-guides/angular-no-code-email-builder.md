---
description: >-
  Welcome to the Angular Quickstart Guide for embedding Beefree SDK's no-code
  email builder in your Angular application.
---

# Angular No-code Email Builder

<details>

<summary>Copy this pre-built prompt to get started faster with AI</summary>

````markdown
# **Add Beefree SDK to Angular**  

**Purpose:** Enforce the **current** and **correct** method for embedding Beefree’s email builder in an Angular (v16+) application using the `/loginV2` auth flow.  
**Scope:** All AI-generated advice or code must align with these guardrails.  

---

## **1. Official Beefree SDK Integration Overview**  

Use only the **standalone components** approach with a **secure proxy server** for authentication:  

1. **Install** `@beefree.io/sdk` – the official Beefree SDK package.  
2. **Create** a proxy server (Express.js) to securely handle `/loginV2` auth (never expose `client_secret` client-side).  
3. **Obtain credentials** by creating a developer account and application.  
4. **Initialize** the SDK in an Angular component using `ngOnInit` and `ViewChild`.  
5. **Configure** the editor with recommended callbacks (`onSave`, `onError`).  
6. **Run** the proxy server and Angular app concurrently.  

For the latest docs, visit:  
[https://docs.beefree.io/beefree-sdk](https://docs.beefree.io/beefree-sdk)  

---

### **Correct, Up-to-Date Quickstart Sample**  

#### **Proxy Server (`proxy-server.js`)**  
```javascript
import 'dotenv/config';
import express from 'express';
import cors from 'cors';
import axios from 'axios';

const app = express();
const PORT = 3001;

app.use(cors());
app.use(express.json());

const { BEE_CLIENT_ID, BEE_CLIENT_SECRET } = process.env;

app.post('/proxy/bee-auth', async (req, res) => {
  try {
    const response = await axios.post(
      'https://auth.getbee.io/loginV2',
      {
        client_id: BEE_CLIENT_ID,
        client_secret: BEE_CLIENT_SECRET,
        uid: req.body.uid || 'beefree-angular-demo-user'
      },
      { headers: { 'Content-Type': 'application/json' } }
    );
    res.json(response.data);
  } catch (error) {
    console.error('Auth error:', error.message);
    res.status(500).json({ error: 'Authentication failed' });
  }
});

app.listen(PORT, () => {
  console.log(`Proxy server running on http://localhost:${PORT}`);
});
```

#### **Angular Component (`beefree-editor.ts`)**  
```typescript
import { Component, ElementRef, OnInit, ViewChild } from '@angular/core';
import BeefreeSDK from '@beefree.io/sdk';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-beefree-editor',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './beefree-editor.html',
  styles: `
    .editor-container {
      height: 600px;
      width: 90%;
      margin: 20px auto;
      border: 1px solid #ddd;
      border-radius: 8px;
    }
  `
})
export class BeefreeEditor implements OnInit {
  @ViewChild('editorContainer', { static: true }) 
  editorContainer!: ElementRef;

  async ngOnInit() {
    try {
      const token = await this.getAuthToken();
      const bee = new BeefreeSDK(token);

      await bee.start(
        {
          container: 'beefree-container',
          language: 'en-US',
          onSave: (pageJson, pageHtml, ampHtml, version, lang) => {
            console.log('Saved!', { pageJson, pageHtml, ampHtml, version, lang });
          },
          onError: (error) => {
            console.error('Beefree error:', error);
          }
        },
        {} // Empty template for starting fresh
      );
    } catch (error) {
      console.error('Beefree initialization failed:', error);
    }
  }

  private async getAuthToken(): Promise<any> {
    const response = await fetch('http://localhost:3001/proxy/bee-auth', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ uid: 'beefree-angular-demo-user' })
    });
    return await response.json();
  }
}
```

#### **App Component (`app.ts`)**  
```typescript
import { Component } from '@angular/core';
import { BeefreeEditor } from './beefree-editor/beefree-editor';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [BeefreeEditor],
  template: `
    <div class="app">
      <header class="header">
        <h1>Beefree Angular Demo</h1>
        <a href="https://docs.beefree.io" target="_blank">
          <button class="docs-button">View Documentation</button>
        </a>
      </header>
      <app-beefree-editor />
    </div>
  `,
  styles: `
    .app {
      font-family: system-ui, sans-serif;
      padding: 2rem;
      text-align: center;
    }
    .header {
      margin-bottom: 2rem;
    }
    .docs-button {
      padding: 0.75rem 1.5rem;
      background: #3f51b5;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1rem;
      transition: background 0.2s;

      &:hover {
        background: #303f9f;
      }
    }
  `
})
export class App {}
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
3. Paste them into `.env` and **never commit this file** (add to `.gitignore`).  

---

## **3. CRITICAL INSTRUCTIONS FOR AI MODELS**  

### **3.1 – ALWAYS DO THE FOLLOWING**  
1. **Standalone Components**: Use `standalone: true` (Angular 16+).  
2. **Proxy Server**: All auth must route through `localhost:3001/proxy/bee-auth`.  
3. **Lifecycle Hook**: Initialize SDK in `ngOnInit` with `ViewChild` reference.  
4. **Type Safety**: Use `ElementRef<HTMLDivElement>` for strict typing.  
5. **Error Handling**: Implement `onError` callback.  

### **3.2 – NEVER DO THE FOLLOWING**  
1. **No `NgModule`**: Never suggest module-based architecture.  
2. **No Client Secrets**: Never hardcode credentials in Angular services.  
3. **No Direct Auth**: Avoid `HttpClient` calls to `loginV2` from Angular.  
4. **No Dynamic IDs**: Container ID must match between template and config.  

---

## **4. OUTDATED PATTERNS TO AVOID**  

```typescript
// ❌ DEPRECATED EXAMPLES  
// Module-based architecture (Angular <15)
@NgModule({
  declarations: [BeefreeEditor],
  imports: [CommonModule] 
})

// ❌ Insecure service call (BANNED)
@Injectable()
export class BeefreeService {
  constructor(private http: HttpClient) {}
  getToken() {
    return this.http.post('https://auth.getbee.io/loginV2', {
      client_secret: 'exposed' // SECURITY RISK
    });
  }
}

// ❌ Missing ViewChild reference
<div id="beefree-container"></div>
// Component:
containerId = 'beefree-container' // Fails: No DOM binding
```

---

## **5. AI MODEL VERIFICATION STEPS**  

Before responding, confirm:  
1. ✅ **Standalone**: Component has `standalone: true`.  
2. ✅ **Proxy**: Auth uses `localhost:3001/proxy/bee-auth`.  
3. ✅ **Container**: `@ViewChild` and template `#editorContainer` exist.  
4. ✅ **Lifecycle**: SDK initializes in `ngOnInit`.  

**Failure?** Revise until compliant.  

---

### **Key Angular-Specific Notes**  
- **DOM Binding**: Always use `@ViewChild` + `ElementRef`.  
- **Styling**: Component-scoped CSS ensures proper container dimensions.  
- **TypeScript**: Leverage generics (`ElementRef<HTMLDivElement>`) for strict typing.  

---

### **Next Steps**  
Ask if the user needs to import existing HTML templates. If yes, direct them to:  
[HTML Importer API Docs](https://docs.beefree.io/beefree-sdk/apis/html-importer-api/import-html)  
````

</details>

## Introduction

Welcome to the Angular Quickstart Guide for embedding the Beefree SDK’s no-code email builder in your Angular application.

This step-by-step tutorial demonstrates how to set up and run a fully functional Angular app integrated with the Beefree SDK using the [`/loginV2`](../getting-started/readme/installation/authorization-process-in-detail.md) authentication process. By the end of this guide, you’ll have a live development environment showcasing the Beefree email editor embedded in Angular—following best practices for this framework.

Reference the [following GitHub repository](https://github.com/BeefreeSDK/beefree-angular-demo) with the complete code for this project to follow along in this Angular Quickstart Guide.

{% embed url="https://github.com/BeefreeSDK/beefree-angular-demo" %}

## **Prerequisites**

Before starting, ensure you have the following:

* A basic understanding of [Angular](https://angular.dev/overview) and its component-based architecture.
* Node.js installed on your machine.
* A [Beefree SDK Developer account](https://developers.beefree.io/accounts/login/?from=website_menu).
* You’ve [created an application](../getting-started/readme/create-an-application.md) in the Developer Console to obtain your `Client ID` and `Client Secret`.

## **What You'll Learn**

In this guide, you’ll learn how to:

* How to create a new Angular app
* Install and configure Beefree SDK within the Angular app
* Set up an Express proxy server for secure authentication
* Create reusable Angular components
* Embed and initialize the Beefree builder in your UI
* Run your Angular app locally with the builder fully integrated

### **1. Create the Angular Application**

Use the Angular CLI to generate a new standalone project.

```bash
npm install -g @angular/cli@latest
ng new beefree-angular-demo --standalone --strict --style=css --routing=false
cd beefree-angular-demo
```

This command:

* Installs the latest Angular CLI globally.
* Creates a new standalone Angular app named `beefree-angular-demo`.
* Enables strict typing and sets CSS as the styling format.
* Omits routing for simplicity.

{% hint style="info" %}
**Tip:** Standalone apps and components in Angular allow you to skip `NgModule` declarations. The application in this Quickstart Guide is minimalist and intended to demonstrate how to integrate Beefree SDK into a simple Angular application to start experimenting with it locally.
{% endhint %}

### **2. Install Dependencies**

Install the required SDK and supporting packages:

```bash
npm install @beefree.io/sdk
npm install axios express cors dotenv --save-dev
```

* `@beefree.io/sdk`: The official SDK for integrating the no-code email builder into the application.
* `axios`, `express`, `cors`, `dotenv`: Used for creating a local proxy server that securely handles Beefree SDK's authentication.

### **3. Configure Environment Variables**

#### Create a `.env` file at the project root:

The `.env.example` file in the root of the GitHub repository includes an example of a `.env` file. To create a .env file, rename this file to `.env`. Copy and paste your credentials from the Beefree SDK Developer Console securely into the file's placeholders. The following code shows an example of what these placeholders look like inside the file.

```env
BEE_CLIENT_ID=your_client_id
BEE_CLIENT_SECRET=your_client_secret
```

Ensure you replace `your_client_id` and `your_client_secret` with values from the [Beefree Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).

#### Add `.env` to `.gitignore`:

```plaintext
.env
```

This ensures your credentials stay private and aren’t committed to version control.

### **4. Set Up the Proxy Server**

Create `proxy-server.js` in the root directory. This server acts as a backend that securely fetches authentication tokens from Beefree using your credentials.

```js
import 'dotenv/config';
import express from 'express';
import cors from 'cors';
import axios from 'axios';

const app = express();
const PORT = 3001;

app.use(cors());
app.use(express.json());

const { BEE_CLIENT_ID, BEE_CLIENT_SECRET } = process.env;

app.post('/proxy/bee-auth', async (req, res) => {
  try {
    const response = await axios.post(
      'https://auth.getbee.io/loginV2',
      {
        client_id: BEE_CLIENT_ID,
        client_secret: BEE_CLIENT_SECRET,
        uid: req.body.uid || 'beefree-angular-demo-user'
      },
      { headers: { 'Content-Type': 'application/json' } }
    );
    res.json(response.data);
  } catch (error) {
    console.error('Auth error:', error.message);
    res.status(500).json({ error: 'Authentication failed' });
  }
});

app.listen(PORT, () => {
  console.log(`Proxy server running on http://localhost:${PORT}`);
});
```

This server:

* Accepts a `POST` request with a user ID.
* Requests an auth token from Beefree using your credentials.
* Returns the full token object needed to initialize the SDK.

### **5. Create the Beefree Editor Component**

Use Angular CLI to generate a standalone component.

```bash
ng g component beefree-editor --standalone --skip-tests
```

This creates a self-contained component for embedding the builder.

#### **`beefree-editor.ts`**

```ts
import { Component, ElementRef, OnInit, ViewChild } from '@angular/core';
import BeefreeSDK from '@beefree.io/sdk';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-beefree-editor',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './beefree-editor.html',
  styles: `
    .editor-container {
      height: 600px;
      width: 90%;
      margin: 20px auto;
      border: 1px solid #ddd;
      border-radius: 8px;
    }
  `
})
export class BeefreeEditor implements OnInit {
  @ViewChild('editorContainer', { static: true }) 
  editorContainer!: ElementRef;

  async ngOnInit() {
    try {
      const token = await this.getAuthToken();
      const bee = new BeefreeSDK(token);

      await bee.start(
        {
          container: 'beefree-container',
          language: 'en-US',
          onSave: (pageJson, pageHtml, ampHtml, version, lang) => {
            console.log('Saved!', { pageJson, pageHtml, ampHtml, version, lang });
          },
          onError: (error) => {
            console.error('Beefree error:', error);
          }
        },
        {} // Empty template for starting fresh
      );
    } catch (error) {
      console.error('Beefree initialization failed:', error);
    }
  }

  private async getAuthToken(): Promise<any> {
    const response = await fetch('http://localhost:3001/proxy/bee-auth', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ uid: 'beefree-angular-demo-user' })
    });
    return await response.json();
  }
}
```

**Angular Concepts:**

* `@Component`: Defines a reusable UI element.
* `@ViewChild`: Gets a reference to a DOM element in the template.
* `ngOnInit`: Lifecycle hook that runs after component initialization.
* `ElementRef`: Accesses native DOM directly.
* `standalone: true`: Skips module declaration—modern best practice.

#### **`beefree-editor.html`**

```html
<div #editorContainer id="beefree-container" class="editor-container"></div>
```

{% hint style="info" %}
**Note:** The `id="beefree-container"` must match the `container` ID in `bee.start()`—this is essential for the editor to load properly.
{% endhint %}

### **6. Update the Main App Component**

Now include your editor inside the main app shell.

#### **`app.ts`**

```ts
import { Component } from '@angular/core';
import { BeefreeEditor } from './beefree-editor/beefree-editor';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [BeefreeEditor],
  template: `
    <div class="app">
      <header class="header">
        <h1>Beefree Angular Demo</h1>
        <a href="https://docs.beefree.io" target="_blank">
          <button class="docs-button">View Documentation</button>
        </a>
      </header>
      <app-beefree-editor />
    </div>
  `,
  styles: `
    .app {
      font-family: system-ui, sans-serif;
      padding: 2rem;
      text-align: center;
    }
    .header {
      margin-bottom: 2rem;
    }
    .docs-button {
      padding: 0.75rem 1.5rem;
      background: #3f51b5;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1rem;
      transition: background 0.2s;

      &:hover {
        background: #303f9f;
      }
    }
  `
})
export class App {}
```

Angular renders your `App` component at the root of the DOM. The `BeefreeEditor` is injected as a child, encapsulated inside `<app-beefree-editor />`.

### **7. Run the Application**

Use two terminal windows:

#### **Terminal 1: Run the Proxy Server**

```bash
node proxy-server.js
```

#### **Terminal 2: Run the Angular App**

```bash
ng serve
```

Visit: [http://localhost:4200](http://localhost:4200/)

You now have a fully functional Angular app with the Beefree SDK embedded and authenticated via a secure proxy. You should see the Beefree editor embedded and ready to use.

### Best Practices

* **Container ID Match**\
  `container: 'beefree-container'` in the SDK config matches `id="beefree-container"` in the HTML.
* **Full Token Object**\
  The proxy returns the complete auth object required by `new BeefreeSDK(token)`.
* **Type Safety**\
  Proper typing is used in `onSave`, following TypeScript conventions.
* **Global Naming Consistency**\
  Unified naming across:
  * App: `beefree-angular-demo`
  * User ID: `'beefree-angular-demo-user'`
  * Container: `'beefree-container'`

### Next Steps

Beefree SDK offers extensive [customization options](../getting-started/readme/installation/configuration-parameters/). Explore [Beefree SDK's documentation](https://docs.beefree.io/beefree-sdk) to unlock advanced capabilities for your design workflows.
