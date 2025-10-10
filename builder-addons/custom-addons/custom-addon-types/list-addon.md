# List AddOn

## Overview

The List AddOn type allows you to insert ordered (numbered) or unordered (bulleted) lists with custom formatting. This is perfect for feature lists, step-by-step instructions, or any content that benefits from a list structure.

## Prerequisites

Before implementing a List AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/). Take the following steps to complete this:

1. Log into the [Developer Console](https://developers.beefree.io/login) and navigate to your application.
2. Create a new Custom AddOn and select **List** as the type.
3. Configure the addon with a unique **handle** (e.g., `my-list-addon`).
4. Choose your implementation method (Content Dialog or External iframe).
5. Save the addon configuration.

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

## Content Object Schema

This section discusses the List AddOn's object schema. Understanding this schema is a core part of successfully implementing a Custom List AddOn type.

Visit the complete [Unified Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json) to see a comprehensive reference on how to structure data for all Custom Addons.

**Required Structure**

The List AddOn schema requires two critical properties: `tag` (which specifies `'ul'` for unordered/bulleted lists or `'ol'` for ordered/numbered lists) and `html` (which contains the actual list markup). Optional styling properties like `color`, `size`, and text formatting allow you to pre-style lists for brand consistency, while users can further customize after insertion.

```javascript
{
  type: 'list',
  value: {
    tag: string,            // Required: 'ul' (bullets) or 'ol' (numbers)
    html: string,           // Required: List HTML
    align: string,          // Optional: 'left', 'center', 'right'
    size: number,           // Optional: Font size in pixels
    underline: boolean,
    italic: boolean,
    bold: boolean,
    color: string,          // Optional: Hex color
    linkColor: string       // Optional: Hex color for links
  }
}
```

**Unordered List (Bullets)**

This example demonstrates an unordered list with bullet points, perfect for presenting features, benefits, or options where order doesn't matter. The `tag: 'ul'` specifies bullet formatting, while the `html` property contains standard list markup that will render with bullet points in the email.

```javascript
resolve({
  type: 'list',
  value: {
    tag: 'ul',
    html: '<ul><li>Feature one</li><li>Feature two</li><li>Feature three</li></ul>',
    align: 'left',
    color: '#333333'
  }
});
```

**Ordered List (Numbers)**

This example shows an ordered list with sequential numbering, ideal for step-by-step instructions, procedures, or any content where order matters. The `tag: 'ol'` tells Beefree to render the list with numbers, and the `bold: true` property emphasizes the text for greater visual impact in the email.

```javascript
resolve({
  type: 'list',
  value: {
    tag: 'ol',
    html: '<ol><li>First step</li><li>Second step</li><li>Third step</li></ol>',
    bold: true,
    color: '#333333'
  }
});
```

**Styled List Example**

This comprehensive example demonstrates all available styling options for lists. By pre-configuring properties like font size, text formatting, colors, and alignment, you can ensure brand consistency while still allowing users to edit the list content after insertion. This pattern is particularly useful for maintaining visual standards across email campaigns.

```javascript
resolve({
  type: 'list',
  value: {
    tag: 'ul',
    html: '<ul><li>Free shipping on orders over $50</li><li>30-day money-back guarantee</li><li>24/7 customer support</li></ul>',
    size: 16,
    bold: false,
    italic: false,
    underline: false,
    color: '#333333',
    linkColor: '#0066CC',
    align: 'left'
  }
});
```

## Content Dialog Implementation

This section covers how to implement a Custom List AddOn using the [Content Dialog method](../build-addons-with-content-dialog.md). It includes code snippets for three different scenarios:

* **Scenario 1:** [End user input not required](list-addon.md#end-user-input-not-required)
* **Scenario 2:** [Dynamic list generation](list-addon.md#dynamic-list-generation)
* **Scenario 3:** [User-defined list](list-addon.md#user-defined-list)&#x20;

### **End user input not required**

The Content Dialog method allows programmatic list insertion through a JavaScript handler. When users drag your list addon onto the stage, this handler is immediately invoked and resolves with a predefined list. This pattern works perfectly for static list content that doesn't require user configuration, providing instant insertion of consistently formatted lists.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-list-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for list insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-list-addon') {
          // Check if triggered by dropping the addon (vs editing existing)
          if (args.hasOpenOnDrop) {
            // Immediately insert a list
            resolve({
              type: 'list',
              value: {
                tag: 'ul',
                html: '<ul><li>Item one</li><li>Item two</li><li>Item three</li></ul>',
                color: '#333333',
                size: 16
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

### **Dynamic List Generation**

This pattern demonstrates programmatic list generation from an array of data, making it easy to create lists from dynamic sources like APIs, databases, or configuration files. By mapping through your data array, you can transform structured information into properly formatted list HTML, enabling dynamic content insertion while maintaining consistent markup structure.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Define list items (could come from an API, database, etc.)
      const features = [
        'Easy to use interface',
        'Fast performance',
        'Secure data handling',
        'Cross-platform compatibility'
      ];
      
      const listType = 'ul';  // or 'ol' for numbered list
      
      // Build HTML from array
      const listItems = features.map(feature => `<li>${feature}</li>`).join('');
      const listHtml = `<${listType}>${listItems}</${listType}>`;
      
      // Resolve with generated list
      resolve({
        type: 'list',
        value: {
          tag: listType,
          html: listHtml,
          color: '#333333',
          size: 16
        }
      });
    }
  }
}
```

### **User-Defined List**

This advanced pattern shows how to let users create custom lists through an interface before insertion. By opening a dialog where users can add, edit, or remove list items and choose between ordered or unordered formatting, you provide maximum flexibility while maintaining proper list structure. The handler filters out empty items and validates input before resolving, ensuring clean list insertion.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for list creation
      // Replace 'yourListEditor' with your actual UI component
      yourListEditor.open({
        onSave: (items, listType) => {
          // Filter out empty items and build list HTML
          const validItems = items
            .filter(item => item.trim())
            .map(item => `<li>${item}</li>`)
            .join('');
          
          const html = `<${listType}>${validItems}</${listType}>`;
          
          // Resolve with user-configured list
          resolve({
            type: 'list',
            value: {
              tag: listType,
              html: html,
              align: 'left',
              color: '#333333',
              size: 16
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

## Iframe Implementation

This section discusses how to implement the Custom List AddOn using the Iframe implementation method. It includes the core concepts you need to understand to successfully implement List AddOns using an Iframe workflow.

**Conceptual Flow**

The Iframe method allows you to create a fully custom interface for list creation using any web technology. Your iframe application communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal when you need a rich UI for list management, including features like drag-and-drop reordering, formatting options, or template selection before inserting the list into the email template.

**Required postMessage Communication**

Implement the standard postMessage protocol to integrate your iframe with Beefree. First, notify Beefree when your iframe is loaded and specify the dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes creating their list, send "onSave" with your list object. If the user cancels, send "onCancel" to close the dialog without inserting content.

**1. Send "loaded" when your iframe is ready:**

```javascript
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '600px',
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
    // Initialize your list creation UI
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing list
    if (data && data.value) {
      document.getElementById('listType').value = data.value.tag || 'ul';
      // Parse existing list HTML to extract items
      const tempDiv = document.createElement('div');
      tempDiv.innerHTML = data.value.html || '';
      const listItems = Array.from(tempDiv.querySelectorAll('li'))
        .map(li => li.textContent)
        .join('\n');
      document.getElementById('listItems').value = listItems;
    }
  }
});
```

**3. Send "onSave" with list data:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'list',
    value: {
      tag: 'ul',
      html: '<ul><li>Item 1</li><li>Item 2</li></ul>',
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

### **Simple Iframe Example**

This complete HTML example provides a functional list creation interface. It demonstrates the full postMessage protocol and includes a dynamic item input system where users can add multiple list items and choose between ordered or unordered formatting. The interface builds proper list HTML and sends it to Beefree. You can expand this basic example with rich text editing, item reordering, or pre-built list templates.

```html
<!DOCTYPE html>
<html>
<head>
  <title>List Creator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    .list-item {
      margin: 10px 0;
    }
    input[type="text"] {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
    }
    select {
      padding: 8px;
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <h2>Create List</h2>
  
  <label for="listType">List Type:</label>
  <select id="listType">
    <option value="ul">Bulleted List (ul)</option>
    <option value="ol">Numbered List (ol)</option>
  </select>
  
  <div id="listItems">
    <div class="list-item">
      <input type="text" placeholder="List item 1" value="First item">
    </div>
    <div class="list-item">
      <input type="text" placeholder="List item 2" value="Second item">
    </div>
    <div class="list-item">
      <input type="text" placeholder="List item 3" value="Third item">
    </div>
  </div>
  
  <button onclick="addItem()">Add Item</button><br>
  <button onclick="insertList()">Insert List</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Notify Beefree that iframe is loaded and ready
    window.parent.postMessage({
      action: 'loaded',
      data: { 
        width: '600px', 
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
      
      if (action === 'load' && data?.value) {
        // Pre-populate when editing existing list
        document.getElementById('listType').value = data.value.tag || 'ul';
        const tempDiv = document.createElement('div');
        tempDiv.innerHTML = data.value.html || '';
        const listItems = Array.from(tempDiv.querySelectorAll('li'))
          .map(li => li.textContent)
          .join('\n');
        document.getElementById('listItems').value = listItems;
      }
    });

    function addItem() {
      const container = document.getElementById('listItems');
      const itemCount = container.children.length + 1;
      const div = document.createElement('div');
      div.className = 'list-item';
      div.innerHTML = `<input type="text" placeholder="List item ${itemCount}">`;
      container.appendChild(div);
    }

    function insertList() {
      const listType = document.getElementById('listType').value;
      const inputs = document.querySelectorAll('#listItems input');
      
      // Build list HTML from inputs
      let listHtml = `<${listType}>`;
      inputs.forEach(input => {
        if (input.value.trim()) {
          listHtml += `<li>${input.value}</li>`;
        }
      });
      listHtml += `</${listType}>`;
      
      // Validate that at least one item exists
      if (!listHtml.includes('<li>')) {
        alert('Please enter at least one list item');
        return;
      }
      
      // Send list data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'list',
          value: {
            tag: listType,
            html: listHtml,
            color: '#333333',
            size: 16
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
