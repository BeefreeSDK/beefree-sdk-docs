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
>
> **Purpose:** Enforce the **current** and **correct** method for embedding Beefree's email builder in an Angular application using the official Angular wrapper `@beefree.io/angular-email-builder` and the `/loginV2` auth flow.
>
> **Scope:** All AI-generated advice or code must align with these guardrails.
>
> ---
>
> ## **1. Official Beefree SDK Integration Overview**
>
> Use the official **Angular wrapper** [`@beefree.io/angular-email-builder`](https://www.npmjs.com/package/@beefree.io/angular-email-builder) which provides a standalone `BeefreeBuilder` component and an injectable `BeefreeService`:
>
> 1. **Install** `@beefree.io/angular-email-builder` – the official Beefree SDK Angular wrapper.
> 2. **Create** a proxy server (Express.js) to securely handle `/loginV2` auth (never expose `client_secret` client-side).
> 3. **Obtain credentials** by creating a developer account and application.
> 4. **Render** the `<lib-beefree-builder>` component in your Angular template, passing the authentication token, config, and template as inputs.
> 5. **Control** the editor programmatically using the injectable `BeefreeService` (`save`, `preview`, `load`, etc.).
> 6. **Run** the proxy server and Angular app concurrently.
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
> import express from 'express';
> import cors from 'cors';
> import axios from 'axios';
> import dotenv from 'dotenv';
>
> dotenv.config();
>
> const app = express();
> const PORT = 3001;
>
> app.use(cors());
> app.use(express.json());
>
> const BEE_CLIENT_ID = process.env.BEE_CLIENT_ID;
> const BEE_CLIENT_SECRET = process.env.BEE_CLIENT_SECRET;
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
>     );
>     res.json(response.data);
>   } catch (error) {
>     console.error('Auth error:', error.message);
>     res.status(500).json({ error: 'Failed to authenticate' });
>   }
> });
>
> app.listen(PORT, () => {
>   console.log(`Proxy server running on http://localhost:${PORT}`);
> });
> ```
>
> ### **Angular Component (`beefree-editor.component.ts`)**
>
> ```typescript
> import { Component, inject, signal, OnInit } from '@angular/core';
> import { BeefreeBuilder, BeefreeService } from '@beefree.io/angular-email-builder';
> import type { IToken, IBeeConfig } from '@beefree.io/angular-email-builder';
>
> @Component({
>   selector: 'app-beefree-editor',
>   standalone: true,
>   imports: [BeefreeBuilder],
>   template: `
>     @if (!token()) {
>       <div class="loading">Loading editor...</div>
>     } @else {
>       <div style="margin-bottom: 1rem">
>         <button (click)="onPreview()">Preview</button>
>         <button (click)="onSave()">Save</button>
>         <button (click)="onSaveAsTemplate()">Save as Template</button>
>       </div>
>       <lib-beefree-builder
>         [token]="token()!"
>         [config]="builderConfig"
>         [width]="'100%'"
>         [height]="'600px'"
>         (bbLoad)="onBuilderLoad()"
>         (bbSave)="onBuilderSave($event)"
>         (bbError)="onBuilderError($event)"
>       />
>     }
>   `,
> })
> export class BeefreeEditorComponent implements OnInit {
>   private beefreeService = inject(BeefreeService);
>
>   token = signal<IToken | null>(null);
>
>   builderConfig: IBeeConfig = {
>     uid: 'demo-user',
>     container: 'beefree-sdk-builder',
>     language: 'en-US',
>   };
>
>   async ngOnInit() {
>     const response = await fetch('http://localhost:3001/proxy/bee-auth', {
>       method: 'POST',
>       headers: { 'Content-Type': 'application/json' },
>       body: JSON.stringify({ uid: 'demo-user' }),
>     });
>     this.token.set(await response.json());
>   }
>
>   onPreview() { this.beefreeService.togglePreview(); }
>   onSave() { this.beefreeService.save(); }
>   onSaveAsTemplate() { this.beefreeService.saveAsTemplate(); }
>
>   onBuilderLoad() {
>     console.log('Builder is ready');
>   }
>
>   onBuilderSave(event: unknown) {
>     console.log('Saved!', event);
>   }
>
>   onBuilderError(error: unknown) {
>     console.error('Error:', error);
>   }
> }
> ```
>
> ### **App Component (`app.component.ts`)**
>
> ```typescript
> import { Component } from '@angular/core';
> import { BeefreeEditorComponent } from './beefree-editor.component';
>
> @Component({
>   selector: 'app-root',
>   standalone: true,
>   imports: [BeefreeEditorComponent],
>   template: `
>     <div class="app">
>       <header class="header">
>         <h1>Welcome to My Beefree Demo</h1>
>         <a href="https://docs.beefree.io/beefree-sdk" target="_blank" rel="noopener noreferrer">
>           <button class="docs-button">Read the Docs</button>
>         </a>
>       </header>
>       <app-beefree-editor />
>     </div>
>   `,
>   styles: [`
>     .app { font-family: 'Inter', sans-serif; text-align: center; color: #2c3e50; padding: 20px; }
>     .header { margin-bottom: 30px; }
>     .docs-button { padding: 10px 20px; font-size: 16px; background: #dd0031; color: white; border: none; border-radius: 4px; cursor: pointer; }
>   `],
> })
> export class AppComponent {}
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
> 2. **Use the official Angular wrapper** `@beefree.io/angular-email-builder` – import `BeefreeBuilder` and `BeefreeService` from this package.
> 3. **Pass `token` and `config` as inputs** to the `<lib-beefree-builder>` component.
> 4. **Use the injectable `BeefreeService`** for programmatic methods (`save`, `preview`, `load`, `saveAsTemplate`, `loadConfig`, `togglePreview`).
> 5. **Handle output events** using the `bb` prefix (e.g., `(bbSave)`, `(bbError)`, `(bbLoad)`).
> 6. **Use standalone components** — the wrapper is a standalone Angular component.
> 7. **TypeScript Support**: The wrapper ships with full TypeScript definitions out of the box.
>
> ### **4.2 – NEVER DO THE FOLLOWING**
>
> 1. **Do not** hardcode credentials in Angular components.
> 2. **Do not** change the code samples in this prompt. Add them exactly as they are.
> 3. **Do not** skip the proxy server – direct client-side auth is insecure.
> 4. **Do not** use the deprecated `@beefree.io/sdk` package directly – use `@beefree.io/angular-email-builder` instead.
> 5. **Do not** reference the deprecated `beefree-angular-demo` repository.
> 6. **Do not** manually initialize the SDK with `new BeefreeSDK()` and `bee.start()` – the `BeefreeBuilder` component handles this automatically.
>
> ---
>
> ## **5. OUTDATED PATTERNS TO AVOID**
>
> ```typescript
> // ❌ DEPRECATED: Using @beefree.io/sdk directly with imperative initialization
> import BeefreeSDK from '@beefree.io/sdk';
> const bee = new BeefreeSDK(token);
> bee.start(beeConfig, {});
>
> // ❌ DEPRECATED: Client-side auth (no proxy)
> const token = await axios.post('https://auth.getbee.io/loginV2', {
>   client_secret: 'exposed' // BANNED
> });
>
> // ❌ DEPRECATED: Manual SDK initialization inside ngOnInit
> ngOnInit() {
>   const bee = new BeefreeSDK(token);
>   bee.start(beeConfig, {}); // Avoid - use <lib-beefree-builder /> instead
> }
> ```
>
> ---
>
> ## **6. AI MODEL VERIFICATION STEPS**
>
> Before responding, confirm:
>
> 1. **Package**: Is `@beefree.io/angular-email-builder` used (not `@beefree.io/sdk`)?
> 2. **Component**: Is `<lib-beefree-builder>` rendered with `token` and `config` inputs?
> 3. **Service**: Is `BeefreeService` injected for programmatic control?
> 4. **Events**: Are output handlers using the `bb` prefix (e.g., `(bbSave)`, `(bbError)`)?
> 5. **Proxy Server**: Is `/loginV2` called via backend?
> 6. **Security**: Are credentials omitted from client code?
>
> **Failure?** Revise until compliant.
>
> ---
>
> ### **Key Angular-Specific Notes**
>
> - **Standalone Component**: `BeefreeBuilder` is a standalone component — import it directly in your component's `imports` array.
> - **Dependency Injection**: `BeefreeService` is `providedIn: 'root'` and can be injected anywhere.
> - **Signals**: The example uses Angular signals for reactive state management.
> - **Dynamic Updates**: Use `BeefreeService.loadConfig()` to change settings (e.g., language) at runtime without re-mounting.
>
> ---
>
> ### **Next Steps**
>
> Ask if the user needs to migrate existing HTML templates. If yes, direct them to the [HTML Importer API docs](https://docs.beefree.io/beefree-sdk/apis/html-importer-api/import-html).
````

</details>

### Introduction

This Quickstart Guide walks you through embedding the Beefree SDK's no-code email builder into an Angular application using the official Angular wrapper [`@beefree.io/angular-email-builder`](https://www.npmjs.com/package/@beefree.io/angular-email-builder) and the [/loginV2](https://docs.beefree.io/beefree-sdk/getting-started/readme/authorization) authorization process. By the end of this guide, you'll have a fully functional Angular app running locally with the builder embedded, authenticated, and ready to use — following Angular best practices.

Reference the [angular-email-builder GitHub repository](https://github.com/BeefreeSDK/angular-email-builder) with the complete code for this project to follow along in this Angular Quickstart Guide. The [`src/`](https://github.com/BeefreeSDK/angular-email-builder/tree/main/src) folder in the repository contains a full working demo application.

### Prerequisites

Before you begin, make sure you:

* Understand [Angular](https://angular.dev/) and its core concepts (standalone components, dependency injection, signals)
* Have a [Beefree SDK account](https://developers.beefree.io)
* [Create an application](https://docs.beefree.io/beefree-sdk/getting-started/readme/create-an-application) in the Beefree Developer Console
* Obtain your Client ID and Client Secret from the Developer Console

### What you'll learn

This guide covers how to:

* Set up a new Angular app
* Install the Beefree SDK Angular wrapper
* Set up secure authentication using a proxy server
* Initialize and embed the builder using the `BeefreeBuilder` component and `BeefreeService`
* Run and test your app locally

### 1. Create an Angular App

To create your Angular app, open a terminal and run the following command. This example uses `beefree-angular-demo` as the project name.

```
ng new beefree-angular-demo --standalone
cd beefree-angular-demo
```

After installation, your project structure will be ready for development. You'll create and wire up the main app component and the Beefree editor component in the next steps.

### 2. Install the Beefree SDK Angular Wrapper

To install the official [Beefree SDK Angular wrapper npm package](https://www.npmjs.com/package/@beefree.io/angular-email-builder), run:

```
npm install @beefree.io/angular-email-builder
```

The `@beefree.io/sdk` dependency is included automatically. The wrapper requires Angular 20+ and Node.js >= 18.

This package contains everything needed to render the no-code email builder inside your Angular application: a standalone `BeefreeBuilder` component (selector: `lib-beefree-builder`) and an injectable `BeefreeService` for programmatic control.

### 3. Create the Main App Component

Now you'll set up your app's primary UI structure, which includes a header and a "Read the Docs" button, plus the embedded builder component.

#### Angular-specific implementation tips

* The `BeefreeEditorComponent` will be a standalone child component
* The `BeefreeBuilder` component from `@beefree.io/angular-email-builder` handles the editor rendering automatically
* The injectable `BeefreeService` provides programmatic control (`save`, `preview`, `load`, etc.)
* TypeScript integration is fully supported out of the box

#### File: `src/app/app.component.ts`

```typescript
import { Component } from '@angular/core';
import { BeefreeEditorComponent } from './beefree-editor.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [BeefreeEditorComponent],
  template: `
    <div class="app">
      <header class="header">
        <h1>Welcome to My Beefree Demo</h1>
        <a href="https://docs.beefree.io/beefree-sdk" target="_blank" rel="noopener noreferrer">
          <button class="docs-button">Read the Docs</button>
        </a>
      </header>
      <app-beefree-editor />
    </div>
  `,
  styles: [`
    .app {
      font-family: 'Inter', sans-serif;
      text-align: center;
      color: #2c3e50;
      padding: 20px;
    }
    .header { margin-bottom: 30px; }
    .docs-button {
      padding: 10px 20px;
      font-size: 16px;
      background: #dd0031;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  `],
})
export class AppComponent {}
```

This file is responsible for the layout and basic interface of your app. It creates a container that introduces the demo, links to the documentation, and includes the builder.

> **Note:** This helps you visually distinguish the application UI from the embedded builder's interface.

### 4. Create the editor component

You'll now define the builder logic in a dedicated component — `BeefreeEditorComponent`.

This step includes setting up the `BeefreeBuilder` component, injecting the `BeefreeService`, handling output events, and fetching a secure token.

#### Authentication flow (server-side only)

To securely authenticate with Beefree:

* Never expose your Client ID or Client Secret in frontend code
* Always use a backend or proxy server to call `/loginV2`
* Pass a UID to uniquely identify the user session

#### BeefreeBuilder Component and BeefreeService

The `@beefree.io/angular-email-builder` wrapper provides two main exports:

* **`BeefreeBuilder`** — a standalone Angular component (selector: `lib-beefree-builder`) that renders the Beefree editor. It requires `token` and `config` as inputs. You can optionally pass `template`, `width`, `height`, `shared`, and `sessionId` inputs.
* **`BeefreeService`** — an injectable service (`providedIn: 'root'`) that manages the builder lifecycle and provides programmatic controls.

The `BeefreeBuilder` component uses output events with the `bb` prefix. Key events include:

| Event                | Description                                           |
| -------------------- | ----------------------------------------------------- |
| `(bbLoad)`           | Fires when the builder is fully initialized and ready |
| `(bbSave)`           | Fires on save with page JSON and HTML output          |
| `(bbError)`          | Fires on errors                                       |
| `(bbSend)`           | Fires when the user triggers "send"                   |
| `(bbChange)`         | Fires on every content change                         |
| `(bbPreview)`        | Fires on preview toggle                               |
| `(bbSessionStarted)` | Fires when a collaborative session starts             |
| `(bbWarning)`        | Fires on non-critical warnings                        |

The `BeefreeService` provides:

| Method                  | Description                                                             |
| ----------------------- | ----------------------------------------------------------------------- |
| `save()`                | Export the current design as JSON + HTML                                |
| `saveAsTemplate()`      | Export the current design as a reusable JSON template                   |
| `togglePreview()`       | Toggle preview mode                                                     |
| `preview()`             | Open a preview of the current design                                    |
| `load(template)`        | Load a new template into the editor                                     |
| `loadConfig(partial)`   | Dynamically update settings (e.g., change language) without re-mounting |
| `getTemplateJson()`     | Get the current template JSON                                           |
| `updateToken(token)`    | Refresh the authentication token                                        |
| `getConfig()`           | Get the current builder configuration                                   |
| `setActiveInstance(id)` | Switch between multiple builder instances                               |
| `getInstanceIds()`      | Get all registered builder instance IDs                                 |

#### File: `src/app/beefree-editor.component.ts`

```typescript
import { Component, inject, signal, OnInit } from '@angular/core';
import { BeefreeBuilder, BeefreeService } from '@beefree.io/angular-email-builder';
import type { IToken, IBeeConfig } from '@beefree.io/angular-email-builder';

@Component({
  selector: 'app-beefree-editor',
  standalone: true,
  imports: [BeefreeBuilder],
  template: `
    @if (!token()) {
      <div class="loading">Loading editor...</div>
    } @else {
      <div style="margin-bottom: 1rem">
        <button (click)="onPreview()">Preview</button>
        <button (click)="onSave()">Save</button>
        <button (click)="onSaveAsTemplate()">Save as Template</button>
      </div>
      <lib-beefree-builder
        [token]="token()!"
        [config]="builderConfig"
        [width]="'100%'"
        [height]="'600px'"
        (bbLoad)="onBuilderLoad()"
        (bbSave)="onBuilderSave($event)"
        (bbError)="onBuilderError($event)"
      />
    }
  `,
  styles: [`
    .loading { text-align: center; padding: 40px; }
  `],
})
export class BeefreeEditorComponent implements OnInit {
  private beefreeService = inject(BeefreeService);

  token = signal<IToken | null>(null);

  builderConfig: IBeeConfig = {
    uid: 'demo-user',
    container: 'beefree-sdk-builder',
    language: 'en-US',
  };

  async ngOnInit() {
    try {
      const response = await fetch('http://localhost:3001/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' }),
      });
      this.token.set(await response.json());
    } catch (error) {
      console.error('Initialization error:', error);
    }
  }

  onPreview() {
    this.beefreeService.togglePreview();
  }

  onSave() {
    this.beefreeService.save();
  }

  onSaveAsTemplate() {
    this.beefreeService.saveAsTemplate();
  }

  onBuilderLoad() {
    console.log('Builder is ready');
  }

  onBuilderSave(event: unknown) {
    console.log('Saved!', event);
  }

  onBuilderError(error: unknown) {
    console.error('Error:', error);
  }
}
```

This file handles:

* Fetching an access token from the proxy server on initialization
* Rendering the `BeefreeBuilder` component with the token and config
* Handling `bbSave`, `bbLoad`, and `bbError` output events
* Providing programmatic controls via the injected `BeefreeService`

You can later extend this to include additional config options like custom translations, modules, sidebar positioning, and more.

### 5. Set up the proxy server (V2 Auth)

To authenticate securely using `/loginV2`, create a lightweight proxy server with Node.js and Express.

#### Why a proxy is required

The Beefree SDK requires authentication via Client ID and Client Secret, which must not be exposed in frontend code. The proxy server allows you to:

* Keep credentials safe
* Fetch access tokens securely

Create a `.env` file in your project root. Copy and paste your credentials from the Beefree SDK Developer Console securely into the file's placeholders.

```
BEE_CLIENT_ID='YOUR-CLIENT-ID'
BEE_CLIENT_SECRET='YOUR-CLIENT-SECRET'
```

#### File: `proxy-server.js` (root directory)

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

This server exposes a POST route (`/proxy/bee-auth`) that:

* Accepts a `uid` from the client
* Calls the Beefree Auth endpoint
* Returns a token to the frontend

You'll also install `axios`, `express`, and `cors` as dependencies.

### 6. Run the application

You're now ready to run both the Angular app and the proxy server.

> **Important:** Run each in a separate terminal tab or window.

**Terminal 1 (Proxy Server)**

```
npm install express cors axios dotenv
node proxy-server.js
```

**Terminal 2 (Angular App)**

```
ng serve
```

Then visit: [http://localhost:4200](http://localhost:4200)

You should see your app running with the builder loaded inside the UI.

### Troubleshooting tips

This section lists best practices to keep in mind, and troubleshooting tips while embedding the Beefree SDK into your Angular application.

#### Blank editor container

* Confirm that a valid `token` is being passed to the `<lib-beefree-builder>` component
* Ensure the component has explicit `width` and `height` inputs set
* Check the browser console for JavaScript errors during initialization
* Make sure the proxy server is running and returning a valid token

#### Authentication issues

* Make sure the proxy server is running
* Verify that your Client ID and Secret are correct
* Open DevTools → Network tab to inspect token requests

#### TypeScript errors

* The `@beefree.io/angular-email-builder` package includes full TypeScript definitions out of the box
* Ensure all event handlers match expected output signatures (events use `bb` prefix)

#### Common pitfalls to avoid

* Don't expose credentials in your frontend code
* Handle token expiration scenarios (for example, show a message or use `BeefreeService.updateToken()` to refresh)
* Don't use the deprecated `@beefree.io/sdk` package directly — use `@beefree.io/angular-email-builder` instead

### Next steps

With Beefree SDK running in your Angular app, you can explore advanced customization options.

The `BeefreeService.loadConfig()` method lets you change the builder configuration dynamically at runtime. For example, to switch the editor language without re-mounting:

```typescript
private beefreeService = inject(BeefreeService);

// Later, when the user selects a new language:
this.beefreeService.loadConfig({ language: 'it-IT' });
```

A few common customizations you can apply:

**Custom translations**

```typescript
builderConfig: IBeeConfig = {
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

The wrapper supports real-time collaborative editing. To enable it, pass `shared` and handle the `bbSessionStarted` event:

```html
<lib-beefree-builder
  [token]="token()!"
  [config]="builderConfig"
  [shared]="true"
  (bbSessionStarted)="onSessionStarted($event)"
/>
```

**Multi-Instance support**

The `BeefreeService` supports managing multiple builder instances. Use `setActiveInstance()` to switch between them and `getInstanceIds()` to list all registered instances:

```typescript
// Switch to a specific builder instance before calling methods
this.beefreeService.setActiveInstance('beefree-sdk-builder-2');
this.beefreeService.save();
```

Explore more in the [Beefree SDK documentation](https://docs.beefree.io/beefree-sdk).

For a full working example including multiple builder types (Email, Page, Popup, File Manager), collaborative editing, and multi-language support (22 languages), see the [`src/` folder](https://github.com/BeefreeSDK/angular-email-builder/tree/main/src) in the angular-email-builder repository.
