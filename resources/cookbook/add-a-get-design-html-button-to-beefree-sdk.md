---
description: >-
  Learn how to enable end users to export their designs as HTML by adding a
  simple button to your UI.
---

# Add a “Get design HTML” Button to Beefree SDK

## Why Export HTML?

When end users design emails in Beefree SDK’s no-code, drag-and-drop builder, they eventually will need to export their design's HTML to put it to work. For end users, exporting their designs is an important step in preparing to send out their email campaigns. This recipe shows you how to give end users a button in the UI that:

1. Captures the current design JSON from the editor.
2. Sends it to the [Content Services API’s `/html` endpoint](../../apis/content-services-api/export.md#html).
3. Returns the design's HTML on the frontend with the option to copy or download it.

The purpose of this recipe is to go beyond simply making an API call to the `/html` endpoint. Instead of stopping at the technical step, we’ll walk through a tangible example that shows how the endpoint can be implemented in a way that truly benefits your end users. By looking at a real use case, you’ll see how this functionality supports end users and teams export their designs and prepare to launch their campaigns.

### Project Map: Where to Look in the Sample Project

This recipe is based on the working example in this GitHub repository: [**beefree-sdk-csapi-simple-integration**](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration). Clone it and explore these files:

| File                                                                                                                          | Purpose           | What You’ll Learn                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)             | Node proxy server | How to keep secrets server-side, perform LoginV2 auth, and forward export requests (including **/v1/message/html**) to the [Content Services API](../../apis/content-services-api/export.md#html). |
| [`vite.config.ts`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/vite.config.ts)               | Dev proxy setup   | How to proxy `/proxy` and `/v1` calls from the browser to your Node server (no CORS headaches).                                                                                                    |
| [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx) | Editor wrapper    | How to initialize the SDK, enable `trackChanges`, and keep live JSON in React state.                                                                                                               |
| [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)                     | Main app logic    | How to wire the **“Get design HTML”** button, call `/v1/message/html`, and show results.                                                                                                           |
| [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)                     | Result display    | A simple pattern to render the HTML string with **Copy** and **Download** actions.                                                                                                                 |

{% hint style="info" %}
**Note:** Use this working project and its core concepts to implement the same functionality in your own host application.
{% endhint %}

### Data Flow Diagram

```
+----------------+        +----------------+        +---------------------+
|                | JSON   |                | JSON   |                     |
|  Beefree SDK   |  →     |   Node Proxy   |  →     |  Content Services   |
|   (Frontend)   |        | (proxy-server) |        |  API (/html export) |
|                |        |                |        |                     |
+----------------+        +----------------+        +---------------------+
       |                           |                          |
       |                           |                          v
       |                           |                     HTML (text)
       |                           |                          |
       v                           v                          |
+-------------------------------------------------------------+
|                  Frontend UI (React App)                    |
|    "Get design HTML" button → Copy / Download controls       |
+-------------------------------------------------------------+
```

**Why this flow?** Secrets ([Client Secret](../../getting-started/readme/create-an-application.md), [Client ID](../../getting-started/readme/create-an-application.md), and [Content Services API token](../../apis/content-services-api/authentication.md)) stay server-side, and the frontend focuses on UI and displaying the HTML.

### Prerequisites

* Node.js 20+
* Beefree SDK credentials: `BEE_CLIENT_ID`, `BEE_CLIENT_SECRET`
* [Content Services API key](../../apis/content-services-api/authentication.md)

Create `.env` (see the repository’s example in the [README.md](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration) file):

```bash
BEE_CLIENT_ID=your-client-id
BEE_CLIENT_SECRET=your-client-secret
CS_API_TOKEN=your-csapi-token-or-"Bearer ..."
PORT=3001
```

{% hint style="info" %}
**Important:** Add `.env` to `.gitignore` so you don’t commit secrets.
{% endhint %}

### Step 1: Clone the Project

```bash
git clone https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration.git
cd beefree-sdk-csapi-simple-integration
npm install
```

### Step 2: Proxy Server (LoginV2 and HTML Forwarder)

**Reference:** [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)

* Performs **LoginV2** on the server (see [LoginV2 docs](../../getting-started/readme/installation/authorization-process-in-detail.md)).
* Forwards the template's JSON to the Content Services API `/html` endpoint.
* Returns the HTML response back to the browser.

**Example code snippet**

```js
// proxy-server.js
// POST /v1/message/html → forwards to Content Services API /html and returns text
app.post('/v1/message/html', async (req, res) => {
  const response = await axios.post(
    'https://api.getbee.io/v1/message/html',
    req.body, // current design JSON
    { headers: { Authorization: `Bearer ${process.env.CS_API_TOKEN}` }, responseType: 'text' }
  );
  res.status(200).send(response.data); // raw HTML or JSON-with-HTML as text
});
```

{% hint style="info" %}
**Note:** Keep secrets on the server—never expose your Client Secret or Content Services API key to the browser.
{% endhint %}

### Step 3: Vite Dev Proxy (Frontend → Proxy)

**Reference:** [`vite.config.ts`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/vite.config.ts)

```ts
// vite.config.ts (excerpt)
server: {
  proxy: {
    '/v1':   { target: 'http://localhost:3001', changeOrigin: true },
    '/proxy':{ target: 'http://localhost:3001', changeOrigin: true },
  },
},
```

{% hint style="info" %}
**Note:** This allows you to use `fetch('/v1/...')` in the sample project without running into CORS issues.
{% endhint %}

### Step 4: Initialize Beefree SDK and Track JSON

**Reference:** [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx)

```tsx
// BeefreeEditor.tsx
const beeConfig = {
  container: 'beefree-editor',
  trackChanges: true,
  onChange(json: unknown) {
    onChangeJson(json); // keep React state synced to the builder
  },
};
```

{% hint style="info" %}
**Important:** You’ll `POST` this **current JSON** to `/v1/message/html` on button click.
{% endhint %}

### Step 5: Add the “Get design HTML” Button

**Reference:** [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)

Short, focused handler that sends JSON and accepts either **raw HTML** or **JSON-wrapped HTML**:

```tsx
// App.tsx (excerpt)
async function onGetHtml() {
  const res = await fetch('/v1/message/html', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(currentJson), // send current design JSON
  });
  if (!res.ok) return alert('Failed to convert to HTML');

  const raw = await res.text();       // support raw HTML or JSON-as-text
  let html = raw;
  try {
    const parsed = JSON.parse(raw);   // if JSON wrapper, pull html from body
    const candidate =
      parsed?.body?.html ?? parsed?.body?.result ?? parsed?.body;
    if (typeof candidate === 'string') html = candidate;
  } catch { /* raw HTML case—use as-is */ }

  setHtmlResult(html); // save for UI display & download
}
```

### Step 6: Display Results (Copy or Download)

**Reference:** inline in [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx).

```tsx
function HtmlResult({ html }: { html?: string }) {
  if (!html) return <div>Export results will appear here.</div>;
  return (
    <div>
      <div style={{ display: 'flex', gap: 8, marginBottom: 8 }}>
        <button onClick={() => navigator.clipboard.writeText(html)}>Copy to clipboard</button>
        <a href={`data:text/html;charset=utf-8,${encodeURIComponent(html)}`} download="design.html">
          Download HTML
        </a>
      </div>
      <pre style={{ whiteSpace: 'pre-wrap' }}>{html}</pre>
    </div>
  );
}
```

### Running the Sample

From the project root:

```bash
npm run dev:proxy   # start the Node proxy (LoginV2 and Content Services API forwarding)
npm run dev         # start the React app
```

Open [**http://localhost:3000**](http://localhost:3000/), design something, and click **Get design HTML**.

### Troubleshooting

* **401/403 from CS API**\
  Check `CS_API_TOKEN` and ensure it includes the `Bearer` prefix.
* **CORS**\
  Ensure the Vite dev proxy forwards `/v1` and `/proxy` to `http://localhost:3001`.
* **Editor sizing and tiles visibility**\
  Use a viewport-based container height (see the repository’s `BeefreeEditor.tsx`) so the side tiles remain visible on different monitor and computer sizes.

### Learn More

* Working example: [**beefree-sdk-csapi-simple-integration**](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration)
* API docs (**Export → HTML**): [**https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#html**](https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#html)

### Key Takeaway

API docs tell you what the `/html` endpoint does.\
This recipe shows you how it’s implemented end-to-end as a button in a real app:

* **Secure proxy** (`proxy-server.js`) with server-side LoginV2
* **Frontend dev proxy** (`vite.config.ts`)
* **Live JSON tracking** (`BeefreeEditor.tsx`)
* **“Get design HTML” button** (`App.tsx`)

Clone the project, explore the files, and reuse these core concepts in your own host application so your users can export production-ready HTML with a single click.
