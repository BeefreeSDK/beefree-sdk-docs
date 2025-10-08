# JavaScript API for Iframe AddOns

### Overview

The JavaScript API enables communication between your external iframe AddOn and the Beefree editor using the browser's `postMessage` API. This bidirectional messaging system is the foundation of all iframe-based addons—it's how your addon tells Beefree it's ready, receives context about the editor environment, sends content to be inserted, and signals when operations are complete or canceled. Understanding this API is essential for building functional iframe addons.

**You do not need this if:**

* You're using the Content Dialog Method

#### Communication Protocol

**Message Structure**

All messages follow a consistent JSON structure with an `action` property identifying the message type and an optional `data` property containing the payload. This standardization makes the API predictable and easy to implement—every message you send or receive follows this same pattern, reducing cognitive overhead and making debugging straightforward. The `action` field is always a string, and the `data` field can contain any JSON-serializable data appropriate for that action.

All messages use this format:

```javascript
{
  action: string,  // Action type: 'loaded', 'init', 'onSave', etc.
  data: any        // Optional payload specific to the action
}
```

**Communication Flow**

Understanding the message flow sequence is critical for proper addon implementation. Your iframe must send `loaded` first to signal readiness, then wait for Beefree to respond with `init` containing context. If the user is editing existing content, Beefree also sends `load` with the current content. Finally, your addon sends either `onSave` (to insert content) or `onCancel` (to abort) based on user actions. Missing any step in this flow causes the addon to malfunction.

```
Your Iframe                          Beefree Editor
──────────────────────────────────────────────────
1. Send 'loaded' ──────────────────→
                  ←──────────────── 2. Send 'init'
                  ←──────────────── 3. Send 'load' (if editing)
[User interacts with your UI]
4. Send 'onSave' ──────────────────→
   OR
   Send 'onCancel' ─────────────────→
```

#### Messages Your AddOn Sends

**1. `loaded` — Iframe is Ready**

The `loaded` message is your addon's first communication with Beefree—it signals that your iframe has finished loading, initialized its UI, and is ready to receive messages. This is a critical handshake; without it, Beefree doesn't know your addon is ready and won't send the `init` message or display your interface. Always send this message as early as possible in your application's lifecycle, typically in a DOMContentLoaded or useEffect hook.

**When:** Immediately after your iframe loads\
**Purpose:** Tells Beefree the AddOn is ready to communicate

```javascript
// Send this as soon as your iframe is ready
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '800px',
    height: '600px',
    isRounded: true,
    hasTitleBar: true,
    showTitle: true
  }
}, '*');
```

**With Modal Configuration**

The `data` object in the `loaded` message controls the visual presentation of your addon within Beefree. Setting appropriate dimensions ensures your UI displays optimally. The `isRounded` property adds modern rounded corners, `hasTitleBar` provides a close button and context, and `showTitle` displays your addon's name. These visual options let you match Beefree's design language while maintaining your addon's identity.

**Options:**

| Property      | Type    | Default  | Description                                 |
| ------------- | ------- | -------- | ------------------------------------------- |
| `isRounded`   | Boolean | `false`  | Rounded modal corners                       |
| `hasTitleBar` | Boolean | `false`  | Show title bar with close button            |
| `showTitle`   | Boolean | `false`  | Display AddOn name in title                 |
| `width`       | String  | `'100%'` | Modal width (`'600px'`, `'80%'`, `'80vw'`)  |
| `height`      | String  | `'100%'` | Modal height (`'400px'`, `'90%'`, `'90vh'`) |

**2. `onSave` — Send Content to Editor**

The `onSave` message is how your addon delivers content to be inserted into the email template. The `data` object must contain a valid content object matching your addon type's schema—this is where all your addon's work culminates in structured data that Beefree can process. The schema validation is strict: missing required properties, incorrect property names, or wrong data types cause silent failures. Always validate your content object before sending to avoid frustrating debugging sessions.

**When:** User clicks save/submit button\
**Purpose:** Insert content into the editor

```javascript
// Send this when user confirms they want to insert content
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'html',  // Must match your addon type from Console
    value: {       // Type-specific content structure
      html: '<div>Your content here</div>'
    }
  }
}, '*');
```

**Examples by Type**

Each addon type has its own schema requirements. These examples show the minimal valid structure for common types—understanding these patterns is essential for successful content insertion. Note the subtle differences: images need `src` and `alt`, buttons need `label`, mixed content needs an array. Learning these schemas thoroughly prevents the frustration of silently failing insertions.

**Image:**

```javascript
{
  action: 'onSave',
  data: {
    type: 'image',
    value: {
      src: 'https://example.com/photo.jpg',
      alt: 'Descriptive alt text for accessibility',
      href: 'https://example.com',  // Optional: makes image clickable
      target: '_blank'               // Optional: link behavior
    }
  }
}
```

**Button:**

{% hint style="warning" %}
**Important:** Button properties like `border-radius` and all padding values must be **numbers**, not strings.
{% endhint %}

```javascript
{
  action: 'onSave',
  data: {
    type: 'button',
    value: {
      label: 'Get Started',
      href: 'https://example.com/signup',
      'background-color': '#0066CC',
      'border-radius': 4,        // Number, not string
      color: '#FFFFFF',
      'padding-top': 12,         // Number, not string
      'padding-right': 24,
      'padding-bottom': 12,
      'padding-left': 24
    }
  }
}
```

**Paragraph:**

```javascript
{
  action: 'onSave',
  data: {
    type: 'paragraph',
    value: {
      html: '<p>This is a paragraph of text.</p>',
      color: '#333333',
      bold: false
    }
  }
}
```

**Mixed Content:**

{% hint style="warning" %}
**Important:** Within Mixed Content, titles use `type: 'title'` (not `type: 'heading'`). This is different from standalone Title AddOns which use `type: 'heading'`.
{% endhint %}

```javascript
{
  action: 'onSave',
  data: {
    type: 'mixed',
    value: [
      { 
        type: 'image', 
        value: { 
          src: 'https://example.com/img.jpg', 
          alt: 'Image' 
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
          href: 'https://example.com',
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
}
```

**3. `onCancel` — User Canceled**

The `onCancel` message tells Beefree to close your addon's modal without inserting any content. This is essential for the user experience, every interaction path must end with either `onSave` or `onCancel`. Users might cancel by clicking a cancel button, closing the dialog, or hitting escape.

**When:** User clicks cancel or closes modal\
**Purpose:** Close modal without inserting content

```javascript
// Send this when user decides not to insert content
window.parent.postMessage({
  action: 'onCancel'
}, '*');
```

#### Messages Your AddOn Receives

**1. `init` — Editor Context**

After Beefree receives your `loaded` message, it responds with `init` containing context about the editor environment. This context lets your addon adapt its behavior: the `locale` property enables internationalization, showing your UI in the user's language. The `hasOpenOnDrop` boolean indicates whether Direct Open triggered the addon (automatic on drop), allowing different workflows for quick inserts versus detailed configuration. The optional `data` property can pass through custom information configured in the host application.

**When:** After Beefree receives your `loaded` message\
**Contains:** Editor locale, Direct Open status, and optional custom data

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Locale:', data.locale);             // e.g., 'en-US', 'es-ES'
    console.log('Direct Open:', data.hasOpenOnDrop); // true/false
    console.log('Custom Data:', data.data);          // Optional pass-through
    
    // Use locale to show translated UI
    loadTranslations(data.locale);
    
    // Adapt behavior based on Direct Open
    if (data.hasOpenOnDrop) {
      // Show quick-select UI for fast insertion
      showQuickSelect();
    } else {
      // Show full configuration UI
      showFullEditor();
    }
  }
});
```

**Structure:**

```javascript
{
  action: 'init',
  data: {
    locale: 'en-US',          // Editor language setting
    hasOpenOnDrop: false,     // Was addon triggered via Direct Open?
    data: {}                  // Optional pass-through data from host app
  }
}
```

**2. `load` — Edit Existing Content**

When users click to edit content they previously inserted with your addon, Beefree sends the `load` message containing the existing content object. This enables stateful addons where users can modify their previous choices rather than starting from scratch each time. Your addon should use this data to pre-fill its UI, showing the current configuration. Users see what they created before and can make targeted changes.

**When:** User is editing previously inserted content\
**Contains:** The existing content object that was originally inserted

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'load') {
    console.log('Editing existing content:', data);
    
    // Pre-fill your UI with existing values
    if (data && data.value) {
      if (data.type === 'html' && data.value.html) {
        document.getElementById('htmlInput').value = data.value.html;
      }
      
      if (data.type === 'image') {
        document.getElementById('imageUrl').value = data.value.src;
        document.getElementById('altText').value = data.value.alt;
      }
      
      if (data.type === 'button') {
        document.getElementById('btnLabel').value = data.value.label;
        document.getElementById('btnUrl').value = data.value.href;
      }
      
      // Show any custom metadata you stored
      if (data.value.customFields) {
        restoreCustomSettings(data.value.customFields);
      }
    }
  }
});
```

**Structure:**

```javascript
{
  action: 'load',
  data: {
    type: 'html',       // The addon type
    value: {
      html: '<div>Existing content</div>',
      // Any other properties you included when inserting
      customFields: { /* your custom data */ }
    }
  }
}
```

#### Complete Implementation

This complete example demonstrates a production-ready iframe addon with proper message handling, user input validation, edit mode support, and comprehensive comments. It shows the full lifecycle: initialization, message listening, content creation, and cleanup. Use this as a template for your own addons, replacing the HTML/textarea with your actual UI components. The pattern shows immediate `loaded`, centralized message listener, validation before sending

```html
<!DOCTYPE html>
<html>
<head>
  <title>My AddOn</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      margin: 0;
    }
    h2 {
      margin-top: 0;
    }
    textarea {
      width: 100%;
      height: 250px;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-family: monospace;
      font-size: 14px;
    }
    .button-group {
      margin-top: 15px;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 14px;
    }
    .save-btn {
      background-color: #0066CC;
      color: white;
    }
    .cancel-btn {
      background-color: #6c757d;
      color: white;
    }
  </style>
</head>
<body>
  <h2>Add Content</h2>
  <p>Enter your HTML content below:</p>
  <textarea id="content" placeholder="<div>&#10;  <h1>Hello World!</h1>&#10;  <p>Your content here</p>&#10;</div>"><div style="padding: 20px; background-color: #f0f0f0;">
  <h2>Hello World!</h2>
  <p>This is sample HTML content.</p>
</div></textarea>
  
  <div class="button-group">
    <button class="save-btn" onclick="save()">Insert Content</button>
    <button class="cancel-btn" onclick="cancel()">Cancel</button>
  </div>

  <script>
    // Step 1: Send 'loaded' message immediately
    window.parent.postMessage({
      action: 'loaded',
      data: {
        width: '700px',
        height: '550px',
        isRounded: true,
        hasTitleBar: true,
        showTitle: true
      }
    }, '*');

    // Step 2: Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data || {};

      // Handle 'init' message - editor is ready
      if (action === 'init') {
        console.log('Editor initialized');
        console.log('Locale:', data.locale);
        console.log('Direct Open:', data.hasOpenOnDrop);
        
        // You can adapt your UI based on locale or Direct Open
        // e.g., loadTranslations(data.locale);
      }

      // Handle 'load' message - user is editing existing content
      if (action === 'load') {
        console.log('Loading existing content for editing');
        
        // Pre-fill the textarea with existing HTML
        if (data && data.value && data.value.html) {
          document.getElementById('content').value = data.value.html;
        }
        
        // If you stored custom metadata, restore it
        if (data && data.value && data.value.customFields) {
          console.log('Custom fields:', data.value.customFields);
          // Restore any custom settings from metadata
        }
      }
    });

    // Step 3: Save handler - validates and sends content
    function save() {
      const html = document.getElementById('content').value;
      
      // Validate user input
      if (!html.trim()) {
        alert('Please enter some content');
        return;
      }
      
      // Optional: Add custom metadata for tracking
      const contentObject = {
        type: 'html',
        value: { 
          html: html,
          // Optional: Store custom data that persists with the content
          customFields: {
            createdAt: new Date().toISOString(),
            version: '1.0'
          }
        }
      };
      
      // Send content to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: contentObject
      }, '*');
      
      console.log('Content sent to editor');
    }

    // Step 4: Cancel handler - closes without inserting
    function cancel() {
      console.log('User canceled');
      
      // Notify Beefree to close the modal
      window.parent.postMessage({
        action: 'onCancel'
      }, '*');
    }
    
    // Optional: Handle escape key to cancel
    document.addEventListener('keydown', (event) => {
      if (event.key === 'Escape') {
        cancel();
      }
    });
  </script>
</body>
</html>
```

#### Troubleshooting

| Issue                       | Solution                                                                                                                                      |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Messages not received       | Check browser console for errors, verify postMessage syntax is exact, ensure listener is added before messages arrive                         |
| Modal not appearing         | Ensure `loaded` message is sent immediately on page load, check modal config properties are valid, verify health check endpoint is responding |
| Content not inserting       | Validate content object schema matches addon type exactly, check for missing required properties, test with minimal valid object first        |
| Can't edit existing content | Implement `load` message listener, pre-fill UI with `event.data.value` contents, handle case where value might be undefined                   |
| Cross-browser issues        | Test in all major browsers (Chrome, Firefox, Safari, Edge), check for browser-specific postMessage quirks, use polyfills if needed            |
| Button not displaying       | Verify padding and border-radius values are **numbers**, not strings                                                                          |
