---
description: >-
  Learn how to enable end users export their designs as an Image by adding a
  simple button to your UI.
---

# Add a “Get design Thumbnail image” Button in Beefree SDK

## Why Export a Thumbnail Image?

Beyond HTML and plain text, a thumbnail image is super handy: you can show a visual preview in your app’s gallery, share it in approvals workflows, or attach it to tickets and briefs. In this recipe, you’ll add a button that end users click to generate a **PNG thumbnail** of the current design. It works by:

1. Converting the design's JSON to HTML as a first step. This is important, because the [/image endpoint](../../apis/content-services-api/export.md#image) requires three fields in the `POST` request and HTML is one of them.
2. Completing the remaining two fields `field_type` and `size`, and sending the POST request.
3. Returning a **PNG** end users can preview and download in their UI.

### Project Map: Where to Look in the Sample Project

This recipe is based on the working example in this GitHub repository: [**beefree-sdk-csapi-simple-integration**](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration). Clone it and explore these files:

| File                                                                                                                          | Purpose           | What You’ll Learn                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)             | Node proxy server | How to keep secrets on the server, perform LoginV2 auth, and forward export requests (including **/v1/message/image**) to the CS API. |
| [`vite.config.ts`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/vite.config.ts)               | Dev proxy setup   | How to proxy `/proxy` and `/v1` calls from the browser to your Node server (no CORS headaches).                                       |
| [`src/BeefreeEditor.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/BeefreeEditor.tsx) | Editor wrapper    | How to initialize the SDK, enable `trackChanges`, and keep live JSON in React state.                                                  |
| [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)                     | Main app logic    | How to wire the **“Get design Thumbnail image”** button, call `/v1/message/image`, and show results.                                  |
| `src``/App.tsx`                                                                                                               | Result display    | A simple pattern to preview the PNG and provide a **Download** link.                                                                  |

{% hint style="info" %}
Tip: The repo also demonstrates **HTML export**. Since the Image endpoint needs **HTML** input, you’ll either (a) click your **Get design HTML** button first, cache that HTML, then click **Get design Thumbnail image**, or (b) compute HTML on demand inside your image handler.
{% endhint %}

### Data Flow Diagram

```
+----------------+        +----------------+        +---------------------+
|                | JSON   |                | HTML   |                     |
|  Beefree SDK   |  →     |   Node Proxy   |  →     |  Content Services   |
|   (Frontend)   |        | (proxy-server) |        |   API (/image)      |
|                |        |                |        |                     |
+----------------+        +----------------+        +---------------------+
       |                           |                          |
       |                           |                          v
       |                           |                  PNG image (binary)
       |                           |                          |
       v                           v                          |
+-------------------------------------------------------------+
|                  Frontend UI (React App)                    |
|  "Get design Thumbnail image" → preview + Download link      |
+-------------------------------------------------------------+
```

**Why this flow?** Secrets ([Client Secret](../../getting-started/readme/create-an-application.md), [Client ID](../../getting-started/readme/create-an-application.md), and [Content Services API token](../../apis/content-services-api/authentication.md)) stay server-side, and the frontend focuses on UI and [displaying the image](../../apis/content-services-api/export.md#image).

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
**Important:** `.env` must be in `.gitignore` so you don’t commit secrets.
{% endhint %}

### Step 1: Clone the Project

```bash
git clone https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration.git
cd beefree-sdk-csapi-simple-integration
npm install
```

### Step 2: Proxy Server (LoginV2 + Image Forwarder)

**Reference:** [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/proxy-server.js)

* Performs **LoginV2** on the server (see the [LoginV2 docs](../../getting-started/readme/installation/authorization-process-in-detail.md)).
* Forwards the required design HTML to the [Content Services API `/image` endpoint](../../apis/content-services-api/export.md#image)
* Returns **binary** data to the browser with proper headers.

**Example code snippet**

```js
// proxy-server.js
// POST /v1/message/image → forwards to CS API /image and returns PNG bytes
app.post('/v1/message/image', async (req, res) => {
  // req.body must include: { html, file_type: 'png' | 'jpg', size: '600'|'1000'... }
  const response = await axios.post('https://api.getbee.io/v1/message/image', req.body, {
    headers: { Authorization: `Bearer ${process.env.CS_API_TOKEN}` },
    responseType: 'arraybuffer', // critical: get binary data
  });
  res.setHeader('Content-Type', 'image/png'); // inform browser it’s a PNG
  res.setHeader('Content-Disposition', 'inline');
  res.status(200).send(response.data);
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
    '/v1': { target: 'http://localhost:3001', changeOrigin: true },
    '/proxy': { target: 'http://localhost:3001', changeOrigin: true },
  },
},
```

{% hint style="info" %}
**Note:** This allows you to use `fetch('/v1/...')` in the sample project without running into CORS issues.
{% endhint %}

### Step 4: Initialize Beefree SDK and Track JSON

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
You’ll use this JSON to produce **HTML** (for image export) and for any other export flows.
{% endhint %}

### Step 5: Add the “Get design Thumbnail image” Button

**Reference:** [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx)

The Image endpoint **requires HTML**. Follow the same UX pattern as the repo:

* First, generate HTML (for example, through your **Get design HTML** button that calls `/v1/message/html`) and **cache it**.
* Then, when the user clicks **Get design Thumbnail image**, send that cached HTML to `/v1/message/image`.

**Core UI logic (guard + request + blob preview):**

```tsx
// App.tsx
const lastHtmlRef = useRef<string | undefined>(undefined);

// somewhere after HTML export completes:
/// lastHtmlRef.current = html;  // cache HTML for image export

async function onGetImage() {
  if (!lastHtmlRef.current) {
    alert('Convert template to HTML first'); // guard (same UX as repo)
    return;
  }

  const res = await fetch('/v1/message/image', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      file_type: 'png',   // or 'jpg'
      size: '1000',       // longer side in pixels (e.g., 600, 1000)
      html: lastHtmlRef.current,
    }),
  });

  if (!res.ok) return alert('Failed to create image');

  const blob = await res.blob();
  setImageUrl(URL.createObjectURL(blob)); // displayable preview URL
}
```

{% hint style="info" %}
**Note:** Prefer a two-step UX (HTML first → image), but you can also compute HTML on demand inside `onGetImage` by calling your `/v1/message/html` endpoint first.
{% endhint %}

### Step 6: Display the Image + Download Link

**Reference:** inline in [`src/App.tsx`](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration/blob/main/src/App.tsx) or a small component

```tsx
function ImageResult({ imageUrl }: { imageUrl?: string }) {
  if (!imageUrl) return <div>Export results will appear here.</div>;
  return (
    <div>
      <a href={imageUrl} download="design.png">Download image</a>
      <div style={{ marginTop: 8 }}>
        <img src={imageUrl} alt="Exported Thumbnail" style={{ maxWidth: '100%', height: 'auto' }} />
      </div>
    </div>
  );
}
```

{% hint style="info" %}
**Note:** Users can preview the thumbnail and click **Download** to save the PNG.
{% endhint %}

### Running the Sample

From the project root:

```bash
npm run dev:proxy   # start the Node proxy (LoginV2 + CS API forwarding)
npm run dev         # start the React app
```

Open [**http://localhost:3000**](http://localhost:3000/) → design something → click **Get design HTML** → then click **Get design Thumbnail image**.

### Troubleshooting

* **“Convert template to HTML first”**\
  The Image endpoint **requires HTML**. Export HTML first (or compute it on demand).
* **401/403 from CS API**\
  Check `CS_API_TOKEN`. Ensure it’s correctly set and includes the `Bearer` prefix (the repo normalizes this pattern).
* **Unexpected size/quality**\
  Adjust `size` and `file_type` in your request body per the API options.

### Learn More

* Working example: [**beefree-sdk-csapi-simple-integration**](https://github.com/BeefreeSDK/beefree-sdk-csapi-simple-integration)
* API docs (**Export → Image**): [**https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#image**](https://docs.beefree.io/beefree-sdk/apis/content-services-api/export#image)

### Key Takeaway

API docs tell you what the `/image` endpoint does.\
This recipe shows you how it’s implemented end-to-end as a button in a real app:

* **Secure proxy** (`proxy-server.js`) with LoginV2 server-side
* **Frontend dev proxy** (`vite.config.ts`)
* **Live JSON tracking** (`BeefreeEditor.tsx`)
* **“Get design Thumbnail image” button** (`App.tsx`)

Clone the project, explore the files, and bring these core concepts into your own host application so your users can generate thumbnails with a single click.
