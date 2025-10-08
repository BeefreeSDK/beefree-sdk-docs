# HTML AddOn

### Overview

The HTML AddOn type allows you to insert custom HTML content blocks into the Beefree SDK editor. This is ideal for embedding custom widgets, specialized markup, or any HTML content that requires flexibility beyond standard content blocks.

#### Prerequisites

Before implementing an HTML AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/):

1. Log into the Developer Console and navigate to your application
2. Create a new Custom AddOn and select "HTML" as the type
3. Configure the addon with a unique **handle** (e.g., `my-html-addon`)
4. Choose your implementation method (Content Dialog or External iframe)
5. Save the addon configuration

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match exactly with the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

#### Content Object Schema

**Required Structure**

The HTML AddOn uses a simple schema with a single `html` property containing your markup as a string. This structure tells Beefree to treat the content as raw HTML, preserving your markup exactly as provided while rendering it within the editor.

```javascript
{
  type: 'html',
  value: {
    html: string  // Your HTML markup as a string
  }
}
```

**Basic Example**

This minimal example shows the simplest HTML addon implementation—a single div with text content. Any valid HTML can be inserted this way, from simple text containers to complex nested structures with multiple elements and inline styles.

```javascript
resolve({
  type: 'html',
  value: {
    html: '<div style="padding: 20px; text-align: center;">Hello World!</div>'
  }
});
```

**Styled Example**

This example demonstrates a more styled HTML block with proper email-safe formatting. Note the use of inline styles (required for email compatibility), table-based structure (for better email client support), and semantic paragraph tags for proper text rendering across different email environments.

```javascript
resolve({
  type: 'html',
  value: {
    html: `
      <table role="presentation" width="100%" cellpadding="0" cellspacing="0">
        <tr>
          <td style="padding: 20px; background-color: #f5f5f5;">
            <p style="margin: 0; font-size: 16px; color: #333333;">
              This is a custom HTML content block with email-safe formatting.
            </p>
          </td>
        </tr>
      </table>
    `
  }
});
```

#### Content Dialog Implementation

**Basic Handler**

The Content Dialog method lets you insert HTML content programmatically when users drag your addon onto the stage. The handler function receives `resolve` and `reject` callbacks—call `resolve` with your HTML object to insert content, or `reject` to cancel the operation. This immediate resolution pattern is perfect for addons that don't require user input before insertion.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-html-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for HTML insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-html-addon') {
          // Check if triggered by dropping the addon (vs editing existing)
          if (args.hasOpenOnDrop) {
            // Immediately insert HTML content
            resolve({
              type: 'html',
              value: {
                html: '<div style="padding: 20px; text-align: center;"><h2>Hello World!</h2><p>This is a custom HTML block.</p></div>'
              }
            });
          } else {
            // Handle editing existing content
            // Open your dialog/modal here
          }
        }
      }
    }
  }
};
```

**Pattern: With User Input**

This pattern demonstrates how to collect user input before inserting HTML content. By opening a custom dialog or modal, you can let users provide content, configuration, or selections that determine what HTML gets generated. The handler waits for the user's confirmation before resolving, giving you full control over the insertion process and allowing for validation or transformation of user input.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for HTML configuration
      // Replace 'yourHtmlEditor' with your actual UI component
      yourHtmlEditor.open({
        onConfirm: (userHtmlContent) => {
          // User confirmed - resolve with their HTML
          resolve({
            type: 'html',
            value: { 
              html: userHtmlContent 
            }
          });
        },
        onCancel: () => {
          // User canceled - reject to abort insertion
          reject();
        }
      });
    }
  }
}
```

**Pattern: Multiple AddOns**

When you have multiple HTML addons registered in the console, you can handle them all in a single handler by checking the `args.contentDialogId` property. This allows you to organize different HTML content types under one handler function, making your code more maintainable while supporting various HTML insertion use cases from simple static content to complex user-driven dialogs.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Handle different HTML addons based on their ID
      switch (args.contentDialogId) {
        case 'simple-html-addon':
          // Immediate insertion for simple addon
          resolve({
            type: 'html',
            value: { 
              html: '<div style="padding: 10px;">Simple HTML Block</div>' 
            }
          });
          break;
          
        case 'custom-widget-addon':
          // Open dialog for complex addon
          yourWidgetSelector.open({
            onConfirm: (widgetHtml) => resolve({ 
              type: 'html', 
              value: { html: widgetHtml } 
            }),
            onCancel: () => reject()
          });
          break;
          
        default:
          reject();
      }
    }
  }
}
```

#### Iframe Implementation

**Conceptual Flow**

The Iframe method provides complete UI flexibility by loading your custom web application inside the Beefree editor. Your iframe communicates with Beefree using the `postMessage` API, following a specific protocol: first notify Beefree when loaded, then receive initialization data, and finally send your HTML content when the user confirms. This approach is ideal when you need a rich, complex interface for HTML generation or configuration.

**Required postMessage Communication**

Your iframe must implement a specific message protocol to integrate properly with Beefree. The "loaded" message tells Beefree your UI is ready and specifies the dialog dimensions. The "init" message from Beefree provides context like locale and editor state. When ready to insert content, send "onSave" with your HTML object, or send "onCancel" if the user abandons the action. This bidirectional communication enables seamless integration between your custom UI and the Beefree editor.

**1. Send "loaded" when your iframe is ready:**

```javascript
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
```

**2. Listen for "init" and "load" messages from Beefree:**

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Editor locale:', data.locale);
    // Initialize your UI with context from Beefree
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing HTML
    if (data && data.value && data.value.html) {
      document.getElementById('htmlContent').value = data.value.html;
    }
  }
});
```

**3. Send "onSave" with HTML content:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'html',
    value: {
      html: '<div style="padding: 20px;">Your HTML content here</div>'
    }
  }
}, '*');
```

**4. Send "onCancel" if user cancels:**

```javascript
// When user clicks cancel or closes dialog
window.parent.postMessage({
  action: 'onCancel'
}, '*');
```

**Simple Iframe Example**

This complete HTML example demonstrates a functional HTML editor interface that integrates with Beefree. It includes the full postMessage protocol implementation, a simple textarea for HTML input, and proper save/cancel handling. You can enhance this basic example with syntax highlighting, live preview, validation, or pre-built HTML templates to create a more sophisticated user experience.

```html
<!DOCTYPE html>
<html>
<head>
  <title>HTML Editor</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    textarea {
      width: 100%;
      height: 300px;
      padding: 10px;
      font-family: monospace;
      margin: 10px 0;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <h2>Edit HTML Content</h2>
  <textarea id="htmlContent" placeholder="Enter your HTML here..."><div style="padding: 20px; text-align: center;"><h2>Hello World!</h2><p>Edit this HTML content.</p></div></textarea>
  <button onclick="insertHtml()">Insert HTML</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Notify Beefree that iframe is loaded and ready
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
    
    // Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data;
      
      if (action === 'init') {
        console.log('Editor locale:', data?.locale);
      }
      
      if (action === 'load' && data?.value?.html) {
        // Pre-populate when editing existing content
        document.getElementById('htmlContent').value = data.value.html;
      }
    });

    function insertHtml() {
      const html = document.getElementById('htmlContent').value;
      
      // Send HTML content to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'html',
          value: { html: html }
        }
      }, '*');
    }

    function cancel() {
      window.parent.postMessage({ action: 'onCancel' }, '*');
    }
  </script>
</body>
</html>
```
