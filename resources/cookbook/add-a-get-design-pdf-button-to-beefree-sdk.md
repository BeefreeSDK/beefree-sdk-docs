---
description: >-
  Learn how to enable end users to export their designs as PDFs by adding a
  simple button to your UI.
---

# Add a “Get design PDF” Button to Beefree SDK

## Why Export PDFs?

Sometimes stakeholders don’t need an editable template—they need a shareable, printable PDF for approvals, legal archiving, or offline review. In this recipe, you’ll add a button that end users can click to generate a PDF of their design. It works by:

1. Converting the design's JSON to HTML as a first step. This is important, because the [/pdf endpoint](../../apis/content-services-api/export.md#pdf) requires three fields in the `POST` request and HTML is one of them.&#x20;
2. Completing the remaining two fields `page_size` and `page_orientation`, and sending the POST request.
3. Returning a **URL** to the generated PDF that end users can click to open or download.

### Project Map: Where to Look in the Sample Project

This recipe is based on the working example in this GitHub repository: [**beefree-sdk-csapi-simple-integration**](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration). Clone it and explore these files:

| File                                                                                                                          | Purpose           | What You’ll Learn                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)             | Node proxy server | How to keep secrets server-side, perform LoginV2 auth, and forward export requests (including **/v1/message/pdf**) to the CS API, then pass the JSON response back. |
| [`vite.config.ts`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/vite.config.ts)               | Dev proxy setup   | How to proxy `/proxy` and `/v1` calls from the browser to your Node server (no CORS headaches).                                                                     |
| [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx) | Editor wrapper    | How to initialize the SDK, enable `trackChanges`, and keep live JSON in React state.                                                                                |
| [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)                     | Main app logic    | How to wire the **“Get design PDF”** button, call `/v1/message/pdf`, and present the returned `body.url`.                                                           |
| `src/``App.tsx`                                                                                                               | Result display    | A simple pattern to show an **Open PDF** link from the returned URL.                                                                                                |

{% hint style="info" %}
**Note:** Use this working project and its core concepts to implement the same functionality in your own host application.
{% endhint %}

### Data Flow Diagram

```
+----------------+        +----------------+        +---------------------+
|                | JSON   |                | HTML   |                     |
|  Beefree SDK   |  →     |   Node Proxy   |  →     |  Content Services   |
|   (Frontend)   |        | (proxy-server) |        |   API (/pdf)        |
|                |        |                |        |                     |
+----------------+        +----------------+        +---------------------+
       |                           |                          |
       |                           |                          v
       |                           |                   JSON response with URL
       |                           |                          |
       v                           v                          |
+-------------------------------------------------------------+
|                  Frontend UI (React App)                    |
| "Get design HTML" → "Get design PDF" → show "Open PDF" link |
+-------------------------------------------------------------+
```

**Why this flow?** Secrets ([Client Secret](../../getting-started/readme/create-an-application.md), [Client ID](../../getting-started/readme/create-an-application.md), and [Content Services API token](../../apis/content-services-api/authentication.md)) stay server-side, and the frontend focuses on UI and displaying the PDF URL.

### Prerequisites

* Node.js **20+**
* Beefree SDK credentials: `BEE_CLIENT_ID`, `BEE_CLIENT_SECRET`
* Content Services API token (server-side only)

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

### Step 2: Proxy Server (LoginV2 and PDF Forwarder)

**Reference:** [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)

* Performs **LoginV2** on the server (see [LoginV2 docs](../../getting-started/readme/installation/authorization-process-in-detail.md)).
* Forwards the required design HTML to the [Content Services API `/pdf` endpoint](../../apis/content-services-api/export.md#pdf).
* Returns JSON (e.g., `{ body: { url: "..." } }`) back to the browser.

**Example code snippet**

```js
// proxy-server.js (excerpt)
// POST /v1/message/pdf → forwards to CS API /pdf and returns JSON (with body.url)
app.post('/v1/message/pdf', async (req, res) => {
  const response = await axios.post(
    'https://api.getbee.io/v1/message/pdf',
    req.body, // { html, page_size, page_orientation, ... }
    { headers: { Authorization: `Bearer ${process.env.CS_API_TOKEN}` } }
  );
  res.status(200).json(response.data); // pass through the JSON with body.url
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

### Step 4: Initialize Beefree SDK & Track JSON

**Reference:** [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx)

```tsx
// BeefreeEditor.tsx (excerpt)
const beeConfig = {
  container: 'beefree-editor',
  trackChanges: true,
  onChange(json: unknown) {
    onChangeJson(json); // keep React state in sync with the builder
  },
};
```

{% hint style="info" %}
**Note:** You’ll use the latest JSON to produce **HTML** (for PDF export) and any other export flows.
{% endhint %}

### Step 5: Add the “Get design PDF” Button

**Reference:** [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)

PDF requires **HTML first**. Follow the same UX pattern used in the repository:

* First, generate HTML (for example, through your **Get design HTML** button), and **cache it**.
* Then, when the user clicks **Get design PDF**, send that cached HTML to `/v1/message/pdf`.

**Core UI logic (guard → request → show link):**

```tsx
// App.tsx
const lastHtmlRef = useRef<string | undefined>(undefined);

// after HTML export completes somewhere else:
// lastHtmlRef.current = html;

async function onGetPdf() {
  if (!lastHtmlRef.current) {
    alert('Convert template to HTML first'); // same UX as the sample repo
    return;
  }

  const res = await fetch('/v1/message/pdf', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      html: lastHtmlRef.current,  // required by the PDF endpoint
      page_size: 'Full',          // example—adjust per your needs
      page_orientation: 'landscape'
    }),
  });

  if (!res.ok) return alert('Failed to convert to PDF');

  const data = await res.json();          // { body: { url: "..." } }
  setPdfUrl(data?.body?.url || undefined);
}
```

{% hint style="info" %}
**Hint:** Prefer a two-step UX (HTML first → PDF), or compute HTML on demand inside `onGetPdf` by calling your `/v1/message/html` endpoint first.
{% endhint %}

### Step 6: Display the PDF Result

**Reference:** inline in [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx) or a tiny `PdfResult` component

```tsx
function PdfResult({ url }: { url?: string }) {
  if (!url) return <div>Export results will appear here.</div>;
  return (
    <div>
      <a href={url} target="_blank" rel="noreferrer">Open PDF</a>
      <div style={{ marginTop: 8 }}>PDF created. Use the link above to view or download.</div>
    </div>
  );
}
```

{% hint style="info" %}
**Note:** The [Content Services API](../../apis/content-services-api/) hosts the generated PDF and returns a URL you can open/download.
{% endhint %}

### Running the Sample

From the project root:

```bash
npm run dev:proxy   # start the Node proxy (LoginV2 + CS API forwarding)
npm run dev         # start the React app
```

Open [**http://localhost:3000**](http://localhost:3000/), build a design, click **Get design HTML** first, then **Get design PDF**.

### Troubleshooting

* **“Convert template to HTML first”**\
  The PDF endpoint **requires HTML**. Export HTML first (or compute it on demand).
* **401/403 from CS API**\
  Check `CS_API_TOKEN`. Ensure it’s correctly set and includes the `Bearer` prefix.
* **Orientation/size not as expected**\
  Adjust `page_size`, `page_orientation`, margins, etc., per the Export API options.

### Learn More

* Working example: [**beefree-sdk-csapi-simple-integration**](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration)
* API docs (**Export → PDF**): [**https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#pdf**](https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#pdf)

### Key Takeaway

API docs tell you what the `/pdf` endpoint does.\
This recipe shows you how it’s implemented end-to-end as a button in a real app:

* **Secure proxy** (`proxy-server.js`) with server-side LoginV2
* **Frontend dev proxy** (`vite.config.ts`)
* **Live JSON tracking** (`BeefreeEditor.tsx`)
* **“Get design PDF” button** (`App.tsx`) with HTML-first guard
* **Open PDF** link from the returned `body.url`

Clone the project, explore the files, and reuse these core concepts in your own host application so your users can export PDFs with a single click.
