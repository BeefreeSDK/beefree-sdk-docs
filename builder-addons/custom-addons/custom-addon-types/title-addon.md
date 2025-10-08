# Title AddOn

### Overview

The Title AddOn (type: `heading`) allows you to insert heading elements (H1-H6) with custom styling. This is perfect for providing pre-formatted headlines, section titles, or branded heading styles to users.

#### Prerequisites

Before implementing a Title AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/):

1. Log into the Developer Console and navigate to your application
2. Create a new Custom AddOn and select "Title" as the type
3. Configure the addon with a unique **handle** (e.g., `my-title-addon`)
4. Choose your implementation method (Content Dialog or External iframe)
5. Save the addon configuration

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match exactly with the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

#### Content Object Schema

**Required Structure**

The Title AddOn uses a unique naming convention—note that the type is `'heading'` (not `'title'`). The schema requires a `title` property specifying the heading level (`'h1'` through `'h6'`) and a `text` property containing the heading content. Optional styling properties like `align`, `size`, `bold`, and `color` allow you to pre-style headings for brand consistency while users can further customize after insertion.

**Important:** The type is `'heading'`, not `'title'`

```javascript
{
  type: 'heading',          // Note: 'heading', not 'title'
  value: {
    title: string,          // Required: 'h1', 'h2', 'h3', 'h4', 'h5', or 'h6'
    text: string,           // Required: Heading text
    align: string,          // Optional: 'left', 'center', 'right'
    size: number,           // Optional: Font size in pixels
    bold: boolean,
    color: string,          // Optional: Hex color
    linkColor: string       // Optional: Hex color for links
  }
}
```

**Basic Example**

This minimal example demonstrates the simplest heading insertion with just the required properties. The `title: 'h2'` specifies it's a level-2 heading (semantically appropriate for major section headers), while `text` contains the actual heading content. This basic structure is perfect for straightforward heading needs where styling can be applied later.

```javascript
resolve({
  type: 'heading',
  value: {
    title: 'h2',
    text: 'Hello World!'
  }
});
```

**Styled Example**

This comprehensive example shows a fully styled heading with all common properties configured. By pre-setting the heading level, alignment, size, emphasis, and color, you ensure consistent brand styling across all headings without requiring users to manually format each one. This pattern is particularly useful for maintaining visual standards and speeding up content creation in email templates.

```javascript
resolve({
  type: 'heading',
  value: {
    title: 'h1',
    text: 'Welcome to Our Newsletter',
    align: 'center',
    size: 32,
    bold: true,
    color: '#333333'
  }
});
```

#### Content Dialog Implementation

**Basic Handler**

The Content Dialog method enables programmatic heading insertion through a JavaScript handler. When users drag your title addon onto the stage, this handler is immediately invoked and resolves with a predefined heading. This pattern works perfectly for static headings or branded heading styles that don't require user input, providing instant insertion of consistently formatted headers.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-title-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for heading insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-title-addon') {
          // Check if triggered by dropping the addon (vs editing existing)
          if (args.hasOpenOnDrop) {
            // Immediately insert a heading
            resolve({
              type: 'heading',
              value: {
                title: 'h2',
                text: 'Hello World!',
                align: 'center',
                color: '#333333',
                size: 28,
                bold: true
              }
            });
          } else {
            // Handle editing existing content or open dialog
          }
        }
      }
    }
  }
};
```

**Pattern: Heading Level Selector**

This pattern demonstrates creating a heading library with size-appropriate styling for each heading level. By mapping heading levels to appropriate font sizes, you maintain proper visual hierarchy (H1 largest, H6 smallest) while providing users with semantic heading options. This approach is ideal for template systems where consistent typographic hierarchy is important for both design and accessibility.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Define heading sizes for consistent hierarchy
      const headingSizes = {
        h1: 36,
        h2: 28,
        h3: 24,
        h4: 20,
        h5: 18,
        h6: 16
      };
      
      // For this example, we'll insert an H2
      // You could open a dialog to let users choose the level
      const level = 'h2';
      
      resolve({
        type: 'heading',
        value: {
          title: level,
          text: 'Section Heading',
          align: 'left',
          size: headingSizes[level],
          bold: true,
          color: '#333333'
        }
      });
    }
  }
}
```

**Pattern: With User Input**

This advanced pattern shows how to let users provide heading text and select formatting options before insertion. By opening a custom interface, users can type their heading, choose the semantic level, set alignment, and configure other properties. The handler waits for user confirmation, then resolves with the customized heading. This provides maximum flexibility while maintaining proper heading structure and semantic HTML.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for heading configuration
      // Replace 'yourHeadingEditor' with your actual UI component
      yourHeadingEditor.open({
        onSave: (headingConfig) => {
          // Map heading levels to appropriate sizes
          const sizes = {
            h1: 36, h2: 28, h3: 24,
            h4: 20, h5: 18, h6: 16
          };
          
          // User confirmed - resolve with configured heading
          resolve({
            type: 'heading',
            value: {
              title: headingConfig.level,
              text: headingConfig.text,
              align: headingConfig.alignment,
              size: sizes[headingConfig.level],
              bold: headingConfig.bold,
              color: headingConfig.color || '#333333'
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

#### Iframe Implementation

**Conceptual Flow**

The Iframe method provides complete UI flexibility by loading your custom web application inside the Beefree editor. Your iframe communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal for rich heading configuration interfaces, heading template libraries, or any scenario where you need full control over how users create and format heading content before inserting it into the email.

**Required postMessage Communication**

Your iframe must implement the standard postMessage protocol to integrate with Beefree. First, notify Beefree when your iframe is loaded and specify dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes configuring their heading, send "onSave" with your heading object. If the user cancels, send "onCancel" to close without inserting. This bidirectional communication ensures seamless integration between your custom heading editor and Beefree.

**1. Send "loaded" when your iframe is ready:**

```javascript
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '600px',
    height: '400px',
    isRounded: true,
    hasTitleBar: true,
    showTitle: true
  }
}, '*');
```

**2. Listen for "init" message from Beefree:**

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Editor locale:', data.locale);
    // Initialize your heading editor UI
  }
  
  if (action === 'load') {
    // Pre-fill form when editing existing title
    if (data && data.value) {
      document.getElementById('headingText').value = data.value.text || '';
      document.getElementById('headingAlign').value = data.value.align || 'center';
      if (data.value.title) {
        document.getElementById('headingLevel').value = data.value.title;
      }
      updatePreview();
    }
  }
});
```

**3. Send "onSave" with heading data:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'heading',
    value: {
      title: 'h2',
      text: 'My Heading',
      align: 'center',
      size: 28,
      bold: true,
      color: '#333333'
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

This complete HTML example demonstrates a functional heading configuration interface. It includes the full postMessage protocol implementation, inputs for heading text and level selection, alignment options, and proper save/cancel handling. The interface automatically adjusts preview text size based on the selected heading level. You can expand this basic example with live preview, font selection, color pickers, or heading template galleries for more sophisticated heading creation.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Heading Editor</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    .field {
      margin: 15px 0;
    }
    label {
      display: block;
      font-weight: bold;
      margin-bottom: 5px;
    }
    input, select {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
    .preview {
      margin: 20px 0;
      padding: 15px;
      background-color: #f5f5f5;
      border-radius: 4px;
    }
    #previewText {
      margin: 0;
      text-align: center;
    }
  </style>
</head>
<body>
  <h2>Configure Heading</h2>
  
  <div class="field">
    <label>Heading Text:</label>
    <input type="text" id="headingText" placeholder="Enter heading text" value="Hello World!" oninput="updatePreview()">
  </div>
  
  <div class="field">
    <label>Heading Level:</label>
    <select id="headingLevel" onchange="updatePreview()">
      <option value="h1">H1 - Main Title</option>
      <option value="h2" selected>H2 - Section Heading</option>
      <option value="h3">H3 - Subsection</option>
      <option value="h4">H4 - Minor Heading</option>
      <option value="h5">H5 - Small Heading</option>
      <option value="h6">H6 - Smallest Heading</option>
    </select>
  </div>
  
  <div class="field">
    <label>Alignment:</label>
    <select id="alignment">
      <option value="left">Left</option>
      <option value="center" selected>Center</option>
      <option value="right">Right</option>
    </select>
  </div>
  
  <div class="preview">
    <strong>Preview:</strong>
    <h2 id="previewText">Hello World!</h2>
  </div>
  
  <button onclick="insertHeading()">Insert Heading</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Heading size mappings
    const headingSizes = {
      h1: 36, h2: 28, h3: 24,
      h4: 20, h5: 18, h6: 16
    };

    // Wait for DOM and send loaded message
    window.addEventListener('DOMContentLoaded', function() {
      setTimeout(function() {
        // Notify Beefree that iframe is loaded and ready
        window.parent.postMessage({
          action: 'loaded',
          data: { 
            width: '600px', 
            height: '400px',
            isRounded: true,
            hasTitleBar: true,
            showTitle: true
          }
        }, '*');
      }, 300);
    });

    // Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data || {};
      
      if (action === 'init') {
        console.log('Editor locale:', data?.locale);
      }
      
      if (action === 'load') {
        // Pre-fill form when editing existing title
        if (data && data.value) {
          document.getElementById('headingText').value = data.value.text || '';
          document.getElementById('alignment').value = data.value.align || 'center';
          if (data.value.title) {
            document.getElementById('headingLevel').value = data.value.title;
          }
          updatePreview();
        }
      }
    });

    function updatePreview() {
      const text = document.getElementById('headingText').value;
      const level = document.getElementById('headingLevel').value;
      const preview = document.getElementById('previewText');
      
      preview.textContent = text;
      preview.style.fontSize = headingSizes[level] + 'px';
    }

    function insertHeading() {
      const text = document.getElementById('headingText').value;
      
      // Validation: ensure text is entered
      if (!text.trim()) {
        alert('Please enter heading text');
        return;
      }
      
      const level = document.getElementById('headingLevel').value;
      const align = document.getElementById('alignment').value;
      
      // Send heading data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'heading',
          value: {
            title: level,
            text: text,
            align: align,
            size: headingSizes[level],
            bold: true,
            color: '#333333'
          }
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

#### Heading Levels

Choose the appropriate semantic level:

* **H1** - Main page/email title (use sparingly, typically once)
* **H2** - Major section headings
* **H3** - Subsection headings
* **H4-H6** - Further nested headings

Proper heading hierarchy improves accessibility and SEO.
