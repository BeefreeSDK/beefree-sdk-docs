# Button AddOn

## Overview

The Button AddOn type allows you to insert pre-styled call-to-action buttons into the Beefree editor. This is perfect for providing users with brand-compliant button styles, reducing design work and ensuring consistency across emails.

## Prerequisites

Before implementing a Button AddOn in your code, you first need to create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/). Take the following steps to complete this:

1. Log in to the [Developer Console](https://developers.beefree.io/login) and navigate to your application.
2. Create a new Custom AddOn and select **Button** as the type.
3. Configure the addon with a unique **handle** (for example, `my-button-addon`).
4. Choose your implementation method ([Content Dialog](../build-addons-with-content-dialog.md) or [External iframe](../build-addons-with-external-iframe/)).
5. Save the addon configuration.

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

## Content Object Schema

This section discusses the Button AddOn's object schema. Understanding this schema is a core part of successfully implementing a Custom Button AddOn type.

Visit the complete [Unified Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json) to see a comprehensive reference on how to structure data for all Custom Addons. &#x20;

**Required Structure**

The Button AddOn requires a specific data structure to properly insert button content into the editor. The schema defines how the button will appear and behave when added to the email template.

{% hint style="warning" %}
**Important:** Padding and border-radius values must be **numbers** (representing pixels), not strings. For example, use `'border-radius': 4` not `'border-radius': '4px'`.
{% endhint %}

```javascript
{
  type: 'button',
  value: {
    label: string,              // Required: Button text
    href: string,               // Optional: Link URL
    'font-family': string,
    'font-size': string,
    'background-color': string,
    'border-radius': number,    // Pixels as number (e.g., 4)
    color: string,              // Text color
    'padding-top': number,      // Pixels as number (e.g., 12)
    'padding-right': number,    // Pixels as number (e.g., 24)
    'padding-bottom': number,   // Pixels as number (e.g., 12)
    'padding-left': number,     // Pixels as number (e.g., 24)
    width: string,
    direction: string           // 'ltr' or 'rtl'
  }
}
```

**Basic Example**

The following example show a basic button implementation, containing only the required `type` and `label` properties. This button will use the editor's default styling and can be customized by the user after insertion.

```javascript
resolve({
  type: 'button',
  value: {
    label: 'Click Here',
    href: 'https://example.com'
  }
});
```

**Styled Example**

This example shows a fully customized button with branded colors, sizing, and padding. By pre-configuring these properties, you ensure consistent brand styling across all buttons without requiring users to manually style each one.

```javascript
resolve({
  type: 'button',
  value: {
    label: 'Get Started',
    href: 'https://example.com/signup',
    'font-size': '16px',
    'background-color': '#0066CC',
    'border-radius': 4,         // Number, not string
    color: '#FFFFFF',
    'padding-top': 12,          // Number, not string
    'padding-right': 24,        // Number, not string
    'padding-bottom': 12,       // Number, not string
    'padding-left': 24          // Number, not string
  }
});
```

## Content Dialog Implementation

This section covers how to implement a Custom Button AddOn using the [Content Dialog method](../build-addons-with-content-dialog.md). It includes code snippets for three different scenarios:

* **Scenario 1:** [End user input not required](button-addon.md#end-user-input-not-required)
* **Scenario 2:** [End user input required](button-addon.md#end-user-input-required)

### **End user input not required**

The Content Dialog method allows you to programmatically insert button content using a JavaScript handler function. When users drag and drop your button addon onto the stage, the handler is immediately invoked with `resolve` and `reject` functions that control the insertion flow. This basic pattern immediately resolves with a pre-defined button, making it perfect for simple use cases where no user interaction is needed.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'simple-button-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for button insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'simple-button-addon') {
          // Immediately insert a button with predefined values
          resolve({
            type: 'button',
            value: {
              label: 'Hello World!',
              href: 'https://example.com',
              'background-color': '#0066CC',
              color: '#FFFFFF',
              'border-radius': 4,         // Number, not string
              'padding-top': 12,          // Number, not string
              'padding-right': 24,        // Number, not string
              'padding-bottom': 12,       // Number, not string
              'padding-left': 24          // Number, not string
            }
          });
        }
      }
    }
  }
};
```

### **End user input required**

This advanced pattern demonstrates how to create a library of pre-defined button styles for users to choose from. By opening a custom UI selector, users can pick between different button variants (primary, secondary, etc.) while maintaining brand consistency. The handler waits for user selection before resolving, giving you full control over the insertion flow.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Define multiple button style presets
      const buttonStyles = {
        primary: {
          'background-color': '#0066CC',
          'color': '#FFFFFF',
          'border-radius': 4,           // Number, not string
          'padding-top': 12,            // Number, not string
          'padding-right': 24,          // Number, not string
          'padding-bottom': 12,         // Number, not string
          'padding-left': 24            // Number, not string
        },
        secondary: {
          'background-color': '#6C757D',
          'color': '#FFFFFF',
          'border-radius': 4,           // Number, not string
          'padding-top': 12,            // Number, not string
          'padding-right': 24,          // Number, not string
          'padding-bottom': 12,         // Number, not string
          'padding-left': 24            // Number, not string
        }
      };
      
      // Open your custom UI for style selection
      // Replace 'yourButtonSelector' with your actual UI component
      yourButtonSelector.open({
        styles: buttonStyles,
        onSelect: (styleKey, buttonText, buttonUrl) => {
          // User confirmed - resolve with selected style
          resolve({
            type: 'button',
            value: {
              label: buttonText,
              href: buttonUrl,
              ...buttonStyles[styleKey]
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

This section discusses how to implement the Custom Button AddOn using the Iframe implementation method. It includes the core concepts you need to understand to successfully implement Button AddOns using an Iframe workflow.

**Conceptual Flow**

The Iframe method allows you to build a completely custom UI for your button addon using any web technology. Your iframe application is loaded inside the Beefree editor and communicates using `postMessage` events. This approach gives you complete control over the user experience, letting you create rich interfaces for button customization, validation, and preview before insertion.

**Required postMessage Communication**

When using the Iframe method, your application must follow a specific message protocol to communicate with the Beefree editor. First, send a "loaded" message to indicate your iframe is ready. Then, listen for the "init" message from Beefree which provides context about the editor state. Finally, send "onSave" with your button data when ready to insert, or "onCancel" if the user abandons the action.

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

**2. Listen for "init" and "load" messages from Beefree:**

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Editor locale:', data.locale);
    // Initialize your UI with context from Beefree
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing button
    if (data && data.value) {
      document.getElementById('buttonText').value = data.value.label || '';
      document.getElementById('buttonUrl').value = data.value.href || '';
    }
  }
});
```

**3. Send "onSave" with button data:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'button',
    value: {
      label: 'Click Me',
      href: 'https://example.com',
      'background-color': '#0066CC',
      color: '#FFFFFF',
      'border-radius': 4,         // Number, not string
      'padding-top': 12,          // Number, not string
      'padding-right': 24,        // Number, not string
      'padding-bottom': 12,       // Number, not string
      'padding-left': 24          // Number, not string
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

This complete HTML example shows a simple but functional button configuration interface. It demonstrates the full communication protocol with Beefree, including the loaded notification, button configuration inputs, and save/cancel actions. You can use this as a starting point and enhance it with your own styling, validation, and additional configuration options.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Button Configurator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    input, button {
      margin: 10px 0;
      padding: 8px;
      width: 100%;
    }
  </style>
</head>
<body>
  <h2>Configure Button</h2>
  <input type="text" id="buttonText" placeholder="Button text" value="Hello World!">
  <input type="url" id="buttonUrl" placeholder="Link URL" value="https://example.com">
  <input type="color" id="buttonColor" value="#0066CC">
  <button onclick="insertButton()">Insert Button</button>
  <button onclick="cancel()">Cancel</button>

  <script>
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
    
    // Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data;
      
      if (action === 'init') {
        console.log('Initialized with locale:', data.locale);
      }
      
      if (action === 'load' && data?.value) {
        // Pre-populate when editing existing button
        document.getElementById('buttonText').value = data.value.label || '';
        document.getElementById('buttonUrl').value = data.value.href || '';
      }
    });

    function insertButton() {
      const text = document.getElementById('buttonText').value;
      const url = document.getElementById('buttonUrl').value;
      const color = document.getElementById('buttonColor').value;
      
      // Send button data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'button',
          value: {
            label: text,
            href: url,
            'background-color': color,
            color: '#FFFFFF',
            'border-radius': 4,         // Number, not string
            'padding-top': 12,          // Number, not string
            'padding-right': 24,        // Number, not string
            'padding-bottom': 12,       // Number, not string
            'padding-left': 24          // Number, not string
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
