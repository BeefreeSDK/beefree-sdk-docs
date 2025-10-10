# Build AddOns with External Iframe

## Overview

The External Iframe Method allows Custom AddOns to be hosted on different domains from the host application. This method is required for Partner AddOns or any AddOn you want to distribute to other Beefree SDK applications. Unlike the Content Dialog method which runs in your application's context, the Iframe method loads your addon as a separate web application in an iframe, communicating with Beefree through the browser's postMessage API. This architecture enables cross-domain functionality and makes your addon portable across different Beefree SDK implementations.

## Required Components

To build an iframe-based addon, you need three main components working together. Your AddOn Application is the web interface users interact with, running in an iframe inside Beefree. The JavaScript API implements postMessage communication to send and receive data between your iframe and the Beefree editor. The Server API provides a health check endpoint that Beefree uses to verify your addon is available, and optionally handles authentication if you want to control which applications can use your addon.

1. **Your AddOn Application** — Hosted on your domain (can be any web technology: React, Vue, vanilla HTML, etc.)
2. **JavaScript API** — Communication via postMessage (Details)
3. **Server API** — Health check endpoint (authentication optional)

## Quick Setup

**1. Create AddOn in Console**

Before implementing your iframe application, you must configure the addon in the Beefree SDK Developer Console. This registration tells Beefree where to load your iframe from, how to verify it's healthy, and optionally how to authenticate requests. These settings are critical—the iframe URL must be publicly accessible, the health check endpoint must respond quickly and reliably, and authentication settings (if used) must be properly configured to avoid blocking legitimate access.

Log into [developers.beefree.io](https://developers.beefree.io/):

| Field                  | Value                                                          |
| ---------------------- | -------------------------------------------------------------- |
| **Method**             | `External iframe`                                              |
| **Iframe URL**         | `https://yourdomain.com/addon`                                 |
| **Healthcheck URL**    | `https://yourdomain.com/api/health` (optional but recommended) |
| **API Key**            | `your-api-key` (optional, for authentication)                  |
| **Authentication URL** | `https://yourdomain.com/api/auth` (optional)                   |

**2. Implement JavaScript API**

Your iframe must implement a specific postMessage protocol to communicate with Beefree. This protocol defines five critical messages: `loaded` (sent when your iframe is ready), `init` (received from Beefree with context), `load` (received when editing existing content), `onSave` (sent when inserting content), and `onCancel` (sent when aborting). Understanding this message flow is essential—missing any of these messages will break the addon's functionality and leave users with non-responsive dialogs.

Your iframe must implement postMessage communication:

**Required messages:**

* Send `loaded` when ready
* Listen for `init` from Beefree
* Listen for `load` when editing existing content
* Send `onSave` with content
* Send `onCancel` on exit

**3. Implement Health Check**

The health check endpoint is a simple HTTP GET endpoint that returns a 200 status code if your addon service is operational. Beefree periodically calls this endpoint to verify your addon is available before offering it to users. This prevents frustrating experiences where users try to use an addon that's down. The health check should be lightweight—it doesn't need to validate complex logic, just confirm your service is responding. A simple "OK" response is sufficient.

Simple endpoint that returns 200:

```javascript
// Express.js example
app.get('/api/health', (req, res) => {
  // Return 200 OK to indicate the service is healthy
  res.status(200).send('OK');
});

// You can optionally include more detailed health information
app.get('/api/health', (req, res) => {
  res.status(200).json({
    status: 'healthy',
    timestamp: new Date().toISOString(),
    version: '1.0.0'
  });
});
```

## JavaScript API (Quick Reference)

**1. Send "loaded"**

The `loaded` message is the first thing your iframe must send—it tells Beefree that your application has finished loading and is ready for interaction. The `data` object in this message controls the modal's appearance: dimensions (width/height), whether it has rounded corners (`isRounded`), whether it shows a title bar with close button (`hasTitleBar`), and whether to display the addon name (`showTitle`). This configuration determines the visual presentation of your addon within the Beefree editor.

```javascript
// Send this immediately when your iframe loads
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '800px',      // Modal width
    height: '600px',     // Modal height
    isRounded: true,     // Rounded corners
    hasTitleBar: true,   // Show title bar with close button
    showTitle: true      // Display AddOn name
  }
}, '*');
```

**2. Listen for "init"**

After Beefree receives your `loaded` message, it responds with an `init` message containing context about the editor environment. The `locale` property tells you the user's language setting, allowing you to localize your interface. The `hasOpenOnDrop` boolean indicates whether the addon was triggered via Direct Open (automatic on drop). The optional `data` property can contain pass-through information you've configured. This context allows your addon to adapt its behavior based on how and where it's being used.

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Locale:', data.locale);           // e.g., 'en-US'
    console.log('Direct Open:', data.hasOpenOnDrop); // true/false
    console.log('Custom data:', data.data);         // Optional pass-through
  }
});
```

**3. Listen for "load" (Editing Mode)**

When users edit existing content that was previously inserted by your addon, Beefree sends a `load` message containing the original content data. Your iframe should use this data to pre-fill your UI, allowing users to modify their previous selections. This is critical for a good editing experience—without it, users would have to reconfigure everything from scratch each time they edit. The `data` parameter contains the exact content object you previously sent via `onSave`.

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'load') {
    // Pre-fill your UI with existing content
    // data.value contains the content object you previously sent
    if (data && data.value) {
      document.getElementById('myInput').value = data.value.someProperty || '';
      // Update all relevant UI elements with stored values
    }
  }
});
```

**4. Send "onSave"**

When the user completes their interaction with your addon and confirms they want to insert content, you send the `onSave` message containing the content object. This content object must follow Beefree's schema for your addon type—the structure with `type` and `value` properties is critical. Beefree validates this object against the schema, and if it's valid, inserts the content into the email template. If the schema is invalid, the insertion silently fails, so proper validation before sending is essential.

```javascript
// Call this when user clicks save/insert
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'html',  // Must match your addon type
    value: {
      html: '<div>Your content here</div>'
    }
  }
}, '*');
```

**5. Send "onCancel"**

If the user decides not to insert content—whether by clicking a cancel button or closing your interface—you must send the `onCancel` message to properly close the modal. This tells Beefree the operation is complete but no content should be inserted. Failing to send either `onSave` or `onCancel` leaves the modal open indefinitely, creating a poor user experience. Every user interaction path in your addon should end with one of these two messages.

```javascript
// Call this when user cancels or closes
window.parent.postMessage({
  action: 'onCancel'
}, '*');
```

See JavaScript API documentation for complete details.

## Simple Working Example

This complete HTML example demonstrates a fully functional iframe addon. It shows the entire postMessage protocol implementation: sending `loaded` on page load with proper modal configuration, listening for `init` and `load` messages, and sending `onSave` or `onCancel` based on user actions. The `load` message handler is particularly important—it pre-fills your UI when users are editing existing content, allowing them to modify what they previously inserted. This example serves as a starting point you can build upon with richer UI, validation, and features.

```html
<!DOCTYPE html>
<html>
<head>
  <title>My AddOn</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    textarea {
      width: 100%;
      height: 200px;
      padding: 10px;
      margin: 10px 0;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <h2>Add Content</h2>
  <textarea id="content" placeholder="Enter your HTML content here..."><div style="padding: 20px;"><p>Hello World!</p></div></textarea>
  <button onclick="save()">Insert Content</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Step 1: Notify Beefree that iframe has loaded
    window.parent.postMessage({
      action: 'loaded',
      data: { 
        width: '700px', 
        height: '500px',
        isRounded: true,
        hasTitleBar: true,
        showTitle: true
      }
    }, '*');

    // Step 2: Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data;
      
      if (action === 'init') {
        // Beefree is ready - editor context received
        console.log('Editor initialized with locale:', data.locale);
      }
      
      if (action === 'load') {
        // User is editing existing content - pre-fill the UI
        if (data && data.value && data.value.html) {
          document.getElementById('content').value = data.value.html;
        }
      }
    });

    // Step 3: Save function sends content to Beefree
    function save() {
      const html = document.getElementById('content').value;
      
      if (!html.trim()) {
        alert('Please enter some content');
        return;
      }
      
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'html',
          value: { html }
        }
      }, '*');
    }

    // Step 4: Cancel function closes without inserting
    function cancel() {
      window.parent.postMessage({
        action: 'onCancel'
      }, '*');
    }
  </script>
</body>
</html>
```

## Modal Customization

The modal's appearance is controlled by the `data` object in your `loaded` message. These properties determine whether users see a full-screen takeover or a smaller centered dialog, whether there are rounded corners for a modern look, and whether a title bar provides clear context about what addon they're using. Different modal configurations suit different addon types—full-screen for complex editors, smaller dialogs for simple selectors, title bars for clarity when multiple addons are available.

Customize the modal appearance in the `loaded` message:

```javascript
window.parent.postMessage({
  action: 'loaded',
  data: {
    isRounded: true,        // Rounded corners for modern look
    hasTitleBar: true,      // Show title bar with close button
    showTitle: true,        // Display AddOn name in title
    width: '800px',         // Modal width
    height: '600px'         // Modal height
  }
}, '*');
```

**Common configurations:**

```javascript
// Full-screen takeover - maximizes space for complex UIs
data: {}  // No properties = 100% viewport

// Fixed size with branding - professional appearance
data: {
  width: '700px',
  height: '500px',
  isRounded: true,
  hasTitleBar: true,
  showTitle: true
}

// Centered modal without title - clean, focused experience
data: {
  width: '900px',
  height: '700px',
  isRounded: true,
  hasTitleBar: false
}

// Compact selector - for quick choices
data: {
  width: '500px',
  height: '350px',
  isRounded: true,
  hasTitleBar: true
}
```

## Content Object Schemas

Your `onSave` message must include a valid content object that matches your addon type's schema. These schemas define the exact structure Beefree expects—missing required properties or using incorrect property names causes insertion to fail. Each addon type has different requirements: images need `src` and `alt`, HTML needs an `html` string, buttons need `label` and often `href`, and mixed content needs an array of module objects. Understanding these schemas is fundamental to iframe addon development.

Your `onSave` message must include a valid content object:

**Image**

```javascript
{
  type: 'image',
  value: {
    src: 'https://example.com/photo.jpg',
    alt: 'Photo description for accessibility',
    href: 'https://example.com',  // Optional clickable link
    target: '_blank'               // Optional link behavior
  }
}
```

**HTML**

```javascript
{
  type: 'html',
  value: {
    html: '<div style="padding: 20px; background: #f0f0f0;"><h2>Welcome!</h2><p>Custom HTML content block.</p></div>'
  }
}
```

**Button**

{% hint style="warning" %}
**Important:** Button properties like `border-radius` and all padding values must be **numbers**, not strings.
{% endhint %}

```javascript
{
  type: 'button',
  value: {
    label: 'Click Here',
    href: 'https://example.com',
    'background-color': '#0066CC',
    'border-radius': 4,        // Number, not string
    color: '#FFFFFF',
    'padding-top': 12,         // Number, not string
    'padding-right': 24,
    'padding-bottom': 12,
    'padding-left': 24
  }
}
```

**Mixed Content**

{% hint style="warning" %}
**Important:** Within Mixed Content, titles use `type: 'title'` (not `type: 'heading'`). This is different from standalone Title AddOns which use `type: 'heading'`.
{% endhint %}

```javascript
{
  type: 'mixed',
  value: [
    { 
      type: 'image', 
      value: { 
        src: 'https://example.com/banner.jpg', 
        alt: 'Banner' 
      } 
    },
    { 
      type: 'title',  // Note: 'title' not 'heading' in mixed content
      value: { 
        text: 'Feature Heading',
        align: 'center',
        size: 28
      } 
    },
    { 
      type: 'paragraph', 
      value: { 
        html: '<p>Description text</p>' 
      } 
    },
    {
      type: 'button',
      value: {
        label: 'Learn More',
        href: 'https://example.com/info',
        'background-color': '#0066CC',
        'border-radius': 4,
        'padding-top': 12,
        'padding-right': 24,
        'padding-bottom': 12,
        'padding-left': 24
      }
    }
  ]
}
```

See [AddOn Types](../custom-addon-types/) for all schemas.

## Testing Checklist

This checklist ensures your addon implements all required functionality before going live. Test each item systematically to catch issues early—missing even one of these can cause confusing user experiences or complete addon failure.

* Health check returns 200 status quickly (< 1 second)
* `loaded` message is sent immediately on iframe load with proper config
* `loaded` message includes isRounded, hasTitleBar, showTitle properties
* Modal appears with correct size and styling
* `init` message is received and processed
* `load` message handler pre-fills content correctly when editing
* `onSave` sends correct content object matching schema
* `onCancel` closes modal without inserting content
* Content inserts correctly in editor and renders properly
* Authentication (if used) succeeds for valid requests
* Authentication (if used) blocks invalid requests
* Cross-browser testing (Chrome, Firefox, Safari, Edge)
* Mobile/responsive behavior (if applicable)

## Troubleshooting

| Issue                   | Solution                                                                                                               |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Iframe not loading      | Check URL accessibility from external networks, verify CORS settings, test health endpoint manually                    |
| Authentication failing  | Verify API key in headers matches expected value, check auth endpoint logs, confirm client ID is in allowlist          |
| postMessage not working | Validate message format exactly matches specs, check browser console for errors, verify origin validation              |
| Content not inserting   | Verify content object schema matches addon type, check for missing required properties, test with minimal valid object |
| Modal sizing wrong      | Check `loaded` message data object, ensure width/height are valid CSS values                                           |
| Edit mode not working   | Implement `load` message listener, pre-fill UI with `event.data.value` contents                                        |
| Button not displaying   | Verify padding and border-radius values are **numbers**, not strings                                                   |
