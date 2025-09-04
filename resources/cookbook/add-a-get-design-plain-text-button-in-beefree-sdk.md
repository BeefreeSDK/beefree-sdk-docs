---
description: >-
  Learn how to enable end users to export their designs as Plain Text by adding
  a simple button to your UI.
---

# Add a “Get design Plain Text” Button in Beefree SDK

## Why Export Plain Text?

With Beefree SDK’s drag-and-drop builder, anyone can design beautiful emails without writing code. Behind the scenes, the builder [transforms the design's JSON into HTML](add-a-get-design-html-button-in-beefree-sdk.md) that can be exported to ESPs and CRMs for large-scale email campaigns. But, every email also needs a plain text version.

Why? Because many email clients and spam filters look for it. Some subscribers even prefer reading emails that way. Without it, carefully designed campaigns risk missing the inbox, or missing portions of audience altogether.

That’s why you need to give end users an easy way to export their designs as **plain text**. In this recipe, you’ll add a button to the builder UI that:

1. Takes the current email design JSON.
2. Sends it to the [Content Services API’s `/plain-text` endpoint](../../apis/content-services-api/export.md#plain-text).
3. Returns the plain text result in the UI, ready to be copied or downloaded.

### Project Map: Where to Look in the Sample Project

This recipe is based on the [beefree-sdk-csapi-simple-integration](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration) GitHub project. Clone it, then explore these key files:

| File                                                                                                                             | Purpose                  | What You’ll Learn                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------- | ------------------------ | -------------------------------------------------------------------------------------------------- |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)                | Node proxy server        | How to securely authenticate with LoginV2 and forward export requests to the Content Services API. |
| [`vite.config.ts`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/vite.config.ts)                  | Dev server proxy setup   | How to forward frontend requests (`/proxy`, `/v1`) to your Node proxy, avoiding CORS issues.       |
| [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx)    | Editor wrapper component | How to initialize the SDK, track live JSON with `onChange`, and keep it in React state.            |
| [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)                        | Main app logic           | How to add the “Get design Plain Text” button and send JSON to your proxy.                         |
| [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/components/PlainTextResult.tsx) | Result display           | How to present the exported plain text, with copy and download options for end users.              |

{% hint style="info" %}
**Note:** Use this working project and its core concepts to implement the same functionality in your own host application.
{% endhint %}

### Data Flow Diagram

Here’s how the data moves through the system:

```
+----------------+        +----------------+        +---------------------+
|                |        |                |        |                     |
|  Beefree SDK   | JSON → |   Node Proxy   | JSON → |  Content Services   |
|   (Frontend)   |        |  (proxy-server)|        |     API (/plain-text)|
|                |        |                |        |                     |
+----------------+        +----------------+        +---------------------+
       |                           |                          |
       |                           |                          v
       |                           |                Plain text result
       |                           |                          |
       v                           v                          |
+-------------------------------------------------------------+
|                  Frontend UI (React App)                    |
|  "Get design Plain Text" button → PlainTextResult component |
|      (copy to clipboard / download as .txt file)            |
+-------------------------------------------------------------+
```

**Why this flow?** Secrets ([Client Secret](../../getting-started/readme/create-an-application.md), [Client ID](../../getting-started/readme/create-an-application.md), and [Content Services API token](../../apis/content-services-api/authentication.md)) stay server-side, and the frontend focuses on UI and displaying the plain text to the end user.

### Step 1: Clone the Project

Clone the repo and install dependencies:

```bash
git clone https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration.git
cd beefree-sdk-csapi-simple-integration
npm install
```

Create `.env` (see the repository’s example in the [README.md](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration) file):

### Step 2: The Proxy Server

**File to reference**: [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)

The proxy does two things:

* Authenticates the editor using LoginV2 (server-side).
  * See [LoginV2 docs](../../getting-started/readme/installation/authorization-process-in-detail.md) for the full auth flow.
* Forwards design JSON to the [`/plain-text` Content Services API endpoint](../../apis/content-services-api/export.md#plain-text).

Key snippet in the repo:

```js
// proxy-server.js
app.post('/v1/message/plain-text', async (req, res) => {
  const response = await axios.post(
    'https://api.getbee.io/v1/message/plain-text',
    req.body, // the design JSON
    { headers: { Authorization: `Bearer ${process.env.CS_API_TOKEN}` } }
  );
  res.send(response.data); // plain text returned to the frontend
});
```

{% hint style="info" %}
**Note:** Keep secrets on the server—never expose your Client Secret or Content Services API key to the browser.
{% endhint %}

### Step 3: The Frontend Proxy Setup

**File to reference**: [`vite.config.ts`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/vite.config.ts)

The dev proxy forwards frontend calls to your backend so you don’t deal with CORS:

```ts
// vite.config.ts
server: {
  proxy: {
    '/v1': { target: 'http://localhost:3001', changeOrigin: true },
    '/proxy': { target: 'http://localhost:3001', changeOrigin: true },
  },
},
```

{% hint style="info" %}
**Note:** This allows you to use `fetch('/v1/...')` in the sample project without running into CORS issues.
{% endhint %}

### Step 4: Tracking JSON in the Editor

**File to reference**: [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx)

The editor tracks live JSON with `onChange`. That JSON is what you’ll send to the export endpoint.

```tsx
// BeefreeEditor.tsx
const beeConfig = {
  container: 'beefree-editor',
  trackChanges: true,
  onChange(json: unknown) {
    onChangeJson(json); // keeps React state updated
  },
};
```

{% hint style="info" %}
**Note:** You’ll use the latest JSON for the API call to the `/plain-text` endpoint.
{% endhint %}

### Step 5: Adding the Button

**File to reference**: [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)

The button is what end users will interact with:

```tsx
// App.tsx (excerpt)
async function onGetPlainText() {
  const res = await fetch('/v1/message/plain-text', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(currentJson), // current design JSON
  });
  setPlainText(await res.text()); // save plain text to state
}

<button onClick={onGetPlainText}>Get design Plain Text</button>
```

This is the heart of the recipe: a button that transforms JSON into a ready-to-use plain text export.

### Step 6: Displaying the Result

**File to reference**: [`src/components/PlainTextResult.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/components/PlainTextResult.tsx)

Make the result useful to your end users with copy and download options:

```tsx
// PlainTextResult.tsx
function PlainTextResult({ text }: { text?: string }) {
  if (!text) return <div>No export yet</div>;

  return (
    <div>
      <button onClick={() => navigator.clipboard.writeText(text)}>Copy</button>
      <a href={`data:text/plain,${encodeURIComponent(text)}`} download="design.txt">
        Download
      </a>
      <pre>{text}</pre>
    </div>
  );
}
```

### Running the Sample

From the project root:

```bash
npm run dev:proxy   # starts the Node proxy
npm run dev         # starts the React app
```

Then visit [http://localhost:3000](http://localhost:3000/). Build a design, click **Get design Plain Text**, and see the export in action.

### Learn More

* Full example project: [beefree-sdk-csapi-simple-integration](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration)
* API docs: [Plain Text Export](https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#plain-text)

### Key Takeaway

API docs tell you what the `/plain-text` endpoint does.\
This recipe shows you how it’s implemented end-to-end as a button in a real app:

* **Proxy server** (`proxy-server.js`)
* **Frontend proxy setup** (`vite.config.ts`)
* **JSON tracking** (`BeefreeEditor.tsx`)
* **Plain text button** (`App.tsx`)

Clone it, explore the files, and then take these core concepts into your own host application.
