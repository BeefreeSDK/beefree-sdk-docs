# Paragraph AddOn

## Overview

The Paragraph AddOn type allows you to insert text paragraphs with formatting and merge tags. This is ideal for providing dynamic, personalized text content or pre-formatted text blocks to users.

## Prerequisites

Before implementing a Paragraph AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/). Take the following steps to complete this:

1. Log into the [Developer Console](https://developers.beefree.io/login) and navigate to your application.
2. Create a new Custom AddOn and select **Paragraph** as the type.
3. Configure the addon with a unique **handle** (for example, `my-paragraph-addon`).
4. Choose your implementation method ([Content Dialog ](../build-addons-with-content-dialog.md)or [External iframe](../build-addons-with-external-iframe/)).
5. Save the addon configuration.

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

## Content Object Schema

This section discusses the Paragraph AddOn's object schema. Understanding this schema is a core part of successfully implementing a Custom Paragraph AddOn type.

Visit the complete [Unified Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json) to see a comprehensive reference on how to structure data for all Custom Addons

**Required Structure**

The Paragraph AddOn schema centers on the `html` property which contains your text content with HTML markup. Optional styling properties like `color`, `bold`, `italic`, and padding allow you to pre-style text for brand consistency. The optional `mergeTags` array enables personalization by defining placeholders that get replaced with recipient-specific data at send time.

```javascript
{
  type: 'paragraph',
  value: {
    html: string,              // Required: HTML content
    underline: boolean,
    italic: boolean,
    bold: boolean,
    color: string,             // Hex color
    linkColor: string,         // Hex color for links
    'padding-top': string,
    'padding-right': string,
    'padding-bottom': string,
    'padding-left': string
  },
  mergeTags: [                 // Optional
    {
      name: string,
      value: string,
      previewValue: string
    }
  ]
}
```

**Basic Example**

This minimal example demonstrates the simplest paragraph insertion with just HTML content. The `html` property contains standard paragraph markup that will render in the email. Users can further style and edit the text after insertion using the editor's sidebar controls.

```javascript
resolve({
  type: 'paragraph',
  value: {
    html: '<p>Welcome! This is a simple paragraph of text that provides information to the reader.</p>'
  }
});
```

**With Styling**

This example shows a styled paragraph with pre-configured text formatting and colors. By setting properties like `bold`, `color`, and padding, you ensure consistent brand styling across paragraphs without requiring users to manually apply formatting. This pattern is particularly useful for maintaining visual standards in email templates.

```javascript
resolve({
  type: 'paragraph',
  value: {
    html: '<p>This is an important announcement that requires your attention.</p>',
    bold: true,
    italic: false,
    underline: false,
    color: '#333333',
    linkColor: '#0066CC',
    'padding-top': '10px',
    'padding-bottom': '10px'
  }
});
```

**With Merge Tags**

This advanced example demonstrates personalization through merge tags, which are placeholders in your text that get replaced with recipient-specific data when emails are sent. The `html` contains merge tags (like `@first_name`), and the `mergeTags` array defines what these represent and their preview values. The preview values show in the editor, while actual values are substituted by your email sending platform at send time.

```javascript
resolve({
  type: 'paragraph',
  value: {
    html: '<p>Hello @first_name, thank you for joining @company_name! We\'re excited to have you on board.</p>',
    color: '#333333'
  },
  mergeTags: [
    {
      name: 'First Name',
      value: '@first_name',
      previewValue: 'John'
    },
    {
      name: 'Company Name',
      value: '@company_name',
      previewValue: 'Example Corp'
    }
  ]
});
```

## Content Dialog Implementation

This section covers how to implement a Custom Paragraph AddOn using the [Content Dialog method](../build-addons-with-content-dialog.md). It includes code snippets for three different scenarios:

* **Scenario 1:** [Pre-defined text content](paragraph-addon.md#pre-defined-text-content)
* **Scenario 2:**[ With personalization](paragraph-addon.md#with-personalization)
* **Scenario 3:** [With user input](paragraph-addon.md#with-user-input)&#x20;

### **Pre-defined text content**

The Content Dialog method enables programmatic paragraph insertion through a JavaScript handler. When users drag your paragraph addon onto the stage, this handler is immediately invoked and resolves with predefined text content. This pattern works perfectly for static text blocks that don't require user input, providing instant insertion of formatted paragraphs with consistent styling.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-paragraph-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for paragraph insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-paragraph-addon') {
          // Check if triggered by dropping the addon (vs editing existing)
          if (args.hasOpenOnDrop) {
            // Immediately insert a paragraph
            resolve({
              type: 'paragraph',
              value: {
                html: '<p>Hello World! This is a sample paragraph that demonstrates text content insertion.</p>',
                color: '#333333',
                bold: false
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

### **With Personalization**

This pattern demonstrates how to create personalized text content using merge tags. By defining a set of merge fields, you enable dynamic content that changes for each email recipient. This is particularly powerful for creating personalized greetings, account-specific information, or custom messaging based on recipient data. The handler immediately resolves with the text and merge tag definitions, which your email platform will process at send time.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Define available merge fields
      const mergeFields = [
        { name: 'First Name', value: '@first_name', previewValue: 'John' },
        { name: 'Last Name', value: '@last_name', previewValue: 'Doe' },
        { name: 'Email', value: '@email', previewValue: 'john@example.com' }
      ];
      
      // Resolve with personalized content
      resolve({
        type: 'paragraph',
        value: {
          html: '<p>Hello @first_name @last_name, your email is @email.</p>',
          color: '#333333'
        },
        mergeTags: mergeFields
      });
    }
  }
}
```

### **With User Input**

This advanced pattern shows how to let users create or edit text content before insertion. By opening a custom text editor interface, users can compose their message, potentially select from available merge tags, and configure styling. The handler waits for user confirmation before resolving, providing a flexible workflow that combines user control with automated formatting and merge tag support.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for text editing
      // Replace 'yourTextEditor' with your actual UI component
      yourTextEditor.open({
        availableMergeTags: [
          { name: 'First Name', value: '@first_name', previewValue: 'John' }
        ],
        onSave: (textContent, selectedMergeTags) => {
          // User confirmed - resolve with their content
          resolve({
            type: 'paragraph',
            value: {
              html: `<p>${textContent}</p>`,
              color: '#333333',
              bold: false
            },
            mergeTags: selectedMergeTags
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

## Iframe Implementation

This section discusses how to implement the Custom Paragraph AddOn using the Iframe implementation method. It includes the core concepts you need to understand to successfully implement Paragraph AddOns using an Iframe workflow.

**Conceptual Flow**

The Iframe method provides complete UI flexibility by loading your custom web application inside the Beefree editor. Your iframe communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal for rich text editors, template selectors, or sophisticated interfaces where you need full control over text composition, formatting, and merge tag insertion before adding the paragraph to the email.

**Required postMessage Communication**

Your iframe must implement the standard postMessage protocol to integrate with Beefree. First, notify Beefree when your iframe is loaded and specify dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes creating their paragraph, send "onSave" with your paragraph object including any merge tags. If the user cancels, send "onCancel" to close without inserting. This bidirectional communication ensures seamless integration.

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
    // Initialize your text editor UI
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing paragraph
    if (data && data.value) {
      const htmlContent = data.value.html || '';
      // Extract text from HTML for textarea
      const tempDiv = document.createElement('div');
      tempDiv.innerHTML = htmlContent;
      document.getElementById('textContent').value = tempDiv.textContent || '';
      
      // Pre-populate formatting options
      document.getElementById('boldCheckbox').checked = data.value.bold || false;
      document.getElementById('italicCheckbox').checked = data.value.italic || false;
      document.getElementById('underlineCheckbox').checked = data.value.underline || false;
    }
  }
});
```

**3. Send "onSave" with paragraph data:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'paragraph',
    value: {
      html: '<p>Your text content here</p>',
      color: '#333333'
    },
    mergeTags: [
      {
        name: 'First Name',
        value: '@first_name',
        previewValue: 'John'
      }
    ]
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

### **Simple Iframe Example**

This complete HTML example demonstrates a functional text editor interface that integrates with Beefree. It includes the full postMessage protocol implementation, a simple textarea for text input, merge tag insertion capability, and proper save/cancel handling. Users can compose text and optionally insert personalization merge tags. You can expand this basic example with rich text editing, formatting toolbar, or template selection for more sophisticated text creation.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Text Editor</title>
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
      font-family: inherit;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
    }
    .merge-tags {
      margin: 10px 0;
    }
    .merge-tag-btn {
      padding: 5px 10px;
      margin: 2px;
      background-color: #e0e0e0;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h2>Edit Text Content</h2>
  
  <div class="merge-tags">
    <strong>Insert Merge Tag:</strong><br>
    <button class="merge-tag-btn" onclick="insertMergeTag('@first_name')">First Name</button>
    <button class="merge-tag-btn" onclick="insertMergeTag('@last_name')">Last Name</button>
    <button class="merge-tag-btn" onclick="insertMergeTag('@email')">Email</button>
  </div>
  
  <textarea id="textContent" placeholder="Enter your text here...">Hello @first_name! Welcome to our newsletter.</textarea>
  
  <button onclick="insertParagraph()">Insert Paragraph</button>
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
      const { action, data } = event.data || {};
      
      if (action === 'init') {
        console.log('Initialized with locale:', data?.locale);
      }
      
      if (action === 'load' && data?.value) {
        // Pre-populate when editing existing paragraph
        const htmlContent = data.value.html || '';
        const tempDiv = document.createElement('div');
        tempDiv.innerHTML = htmlContent;
        document.getElementById('textContent').value = tempDiv.textContent || '';
      }
    });

    function insertMergeTag(tag) {
      const textarea = document.getElementById('textContent');
      const start = textarea.selectionStart;
      const end = textarea.selectionEnd;
      const text = textarea.value;
      textarea.value = text.substring(0, start) + tag + text.substring(end);
      textarea.focus();
    }

    function insertParagraph() {
      const text = document.getElementById('textContent').value;
      
      // Validate text content
      if (!text.trim()) {
        alert('Please enter paragraph text');
        return;
      }
      
      // Define merge tags that might be in the text
      const mergeTags = [
        {
          name: 'First Name',
          value: '@first_name',
          previewValue: 'John'
        },
        {
          name: 'Last Name',
          value: '@last_name',
          previewValue: 'Doe'
        },
        {
          name: 'Email',
          value: '@email',
          previewValue: 'john@example.com'
        }
      ];
      
      // Send paragraph data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'paragraph',
          value: {
            html: `<p>${text}</p>`,
            color: '#333333'
          },
          mergeTags: mergeTags
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

#### Understanding Merge Tags

Merge tags allow personalization by acting as placeholders in your text:

```javascript
// In the editor, user sees the preview:
"Hello John, welcome to Example Corp!"

// In the JSON/template:
html: '<p>Hello @first_name, welcome to @company!</p>'

// At send time, your email platform replaces:
@first_name → actual recipient first name
@company → actual recipient company
```

The `previewValue` is what displays in the editor preview, while the actual values are substituted by your email sending platform when emails are sent.
