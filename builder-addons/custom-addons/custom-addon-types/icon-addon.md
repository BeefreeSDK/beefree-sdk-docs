# Icon AddOn

## Overview

The Icon AddOn (type: `icons`, plural) allows you to insert icon sets with images, text labels, and links. This is perfect for social media links, feature highlights with icons, or any visual navigation elements.

## Prerequisites

Before implementing an Icon AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/):

1. Log in to the [Developer Console](https://developers.beefree.io/login) and navigate to your application.
2. Create a new Custom AddOn and select **Icon** as the type.
3. Configure the addon with a unique **handle** (for example, `my-icon-addon`).
4. Choose your implementation method ([Content Dialog](../build-addons-with-content-dialog.md) or [External iframe](../build-addons-with-external-iframe/)).
5. Save the addon configuration.

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

## Content Object Schema

This section discusses the Icon AddOn's object schema. Understanding this schema is a core part of successfully implementing a Custom Icon AddOn type.

Visit the complete [Unified Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json) to see a comprehensive reference on how to structure data for all Custom Addons.

**Required Structure**

The Icon AddOn uses a unique plural naming convention—note that the type is `'icons'` (plural) and the value contains an `icons` array. Each icon object in the array represents a separate icon element that will be displayed together as a set. This structure allows you to create cohesive icon groups like social media links or feature lists in a single insertion.

**Important:** The type is `'icons'` (plural), not `'icon'`

```javascript
{
  type: 'icons',          // Note: plural 'icons'
  value: {
    icons: [              // Required: Array of icon objects
      {
        image: string,        // Required: Icon image URL
        text: string,         // Optional: Label text
        target: string,       // Optional: '_self', '_blank', etc.
        alt: string,          // Optional: Alt text
        title: string,        // Optional: Title attribute
        href: string,         // Optional: Link URL
        width: string,        // Optional: e.g., '32px'
        height: string,       // Optional: e.g., '32px'
        textPosition: string  // Optional: 'top', 'bottom', 'left', 'right'
      }
    ]
  }
}
```

**Basic Example**

This simple example creates a set of three social media icons without any styling or advanced configuration. The properties (image, href, alt, width, height) are sufficient for basic icon display, and users can further customize the appearance using the editor's sidebar after insertion.

```javascript
resolve({
  type: 'icons',
  value: {
    icons: [
      {
        image: 'https://example.com/icons/facebook.png',
        href: 'https://facebook.com',
        alt: 'Facebook',
        width: '32px',
        height: '32px'
      },
      {
        image: 'https://example.com/icons/twitter.png',
        href: 'https://twitter.com',
        alt: 'Twitter',
        width: '32px',
        height: '32px'
      },
      {
        image: 'https://example.com/icons/instagram.png',
        href: 'https://instagram.com',
        alt: 'Instagram',
        width: '32px',
        height: '32px'
      }
    ]
  }
});
```

**Complete Example with Labels**

This comprehensive example shows all available icon properties, including text labels positioned below each icon and proper link targeting. The `textPosition: 'bottom'` places labels beneath icons, creating a polished social media bar. Using consistent sizing and proper alt text ensures accessibility and visual cohesion across all icons in the set.

```javascript
resolve({
  type: 'icons',
  value: {
    icons: [
      {
        image: 'https://example.com/icons/facebook.png',
        text: 'Facebook',
        href: 'https://facebook.com',
        target: '_blank',
        alt: 'Visit our Facebook page',
        title: 'Facebook',
        width: '32px',
        height: '32px',
        textPosition: 'bottom'
      },
      {
        image: 'https://example.com/icons/twitter.png',
        text: 'Twitter',
        href: 'https://twitter.com',
        target: '_blank',
        alt: 'Follow us on Twitter',
        title: 'Twitter',
        width: '32px',
        height: '32px',
        textPosition: 'bottom'
      },
      {
        image: 'https://example.com/icons/linkedin.png',
        text: 'LinkedIn',
        href: 'https://linkedin.com',
        target: '_blank',
        alt: 'Connect on LinkedIn',
        title: 'LinkedIn',
        width: '32px',
        height: '32px',
        textPosition: 'bottom'
      }
    ]
  }
});
```

## Content Dialog Implementation

This section covers how to implement a Custom Icon AddOn using the [Content Dialog method](../build-addons-with-content-dialog.md). It includes code snippets for three different scenarios:

* **Scenario 1:** [End user input not required](icon-addon.md#end-user-input-not-required)
* **Scenario 2:** [Dynamic Icon Generation](icon-addon.md#dynamic-icon-generation)
* **Scenario 3:** [End User Selection ](icon-addon.md#end-user-selection)

### **End user input not required**

The Content Dialog method enables programmatic icon insertion through a JavaScript handler. When users drag your icon addon onto the stage, this handler function is invoked and immediately resolves with a predefined set of icons. This pattern works perfectly for static icon sets that don't require user configuration, providing instant insertion of consistently styled icon groups.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-icon-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for icon insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-icon-addon') {
          // Immediately insert a set of icons
          resolve({
            type: 'icons',
            value: {
              icons: [
                {
                  image: 'https://example.com/icons/facebook.png',
                  href: 'https://facebook.com',
                  alt: 'Facebook',
                  width: '32px',
                  height: '32px'
                },
                {
                  image: 'https://example.com/icons/twitter.png',
                  href: 'https://twitter.com',
                  alt: 'Twitter',
                  width: '32px',
                  height: '32px'
                }
              ]
            }
          });
        }
      }
    }
  }
};
```

### **Dynamic Icon Generation**

This pattern demonstrates programmatic icon generation from a data structure, making it easy to maintain and update your icon sets. By defining your icon configurations in a structured object, you can map through them to generate the proper schema format. This approach is particularly useful when icon sets are managed in a configuration file or fetched from an API, allowing for centralized management of all icon properties.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Define icon configurations
      const socialNetworks = [
        {
          name: 'Facebook',
          iconUrl: 'https://example.com/icons/facebook.png',
          profileUrl: 'https://facebook.com'
        },
        {
          name: 'Twitter',
          iconUrl: 'https://example.com/icons/twitter.png',
          profileUrl: 'https://twitter.com'
        },
        {
          name: 'LinkedIn',
          iconUrl: 'https://example.com/icons/linkedin.png',
          profileUrl: 'https://linkedin.com'
        }
      ];
      
      // Transform data into icon schema
      const icons = socialNetworks.map(network => ({
        image: network.iconUrl,
        text: network.name,
        href: network.profileUrl,
        target: '_blank',
        alt: `Visit our ${network.name} page`,
        width: '32px',
        height: '32px',
        textPosition: 'bottom'
      }));
      
      resolve({
        type: 'icons',
        value: { icons }
      });
    }
  }
}
```

### **End User Selection**

This advanced pattern shows how to let users customize which icons to include and their URLs before insertion. By opening a custom selection interface, users can choose from available social networks and provide their specific profile URLs. The handler waits for user confirmation, validates the selections, and then generates the icon set based on user input. This provides maximum flexibility while maintaining consistency in icon styling and structure.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for icon selection
      // Replace 'yourIconSelector' with your actual UI component
      yourIconSelector.open({
        availableNetworks: ['Facebook', 'Twitter', 'Instagram', 'LinkedIn'],
        onSave: (selectedNetworks) => {
          // Filter out any without URLs and transform to icon schema
          const icons = selectedNetworks
            .filter(network => network.url)
            .map(network => ({
              image: network.iconUrl,
              text: network.name,
              href: network.url,
              target: '_blank',
              alt: `${network.name}`,
              width: '32px',
              height: '32px',
              textPosition: 'bottom'
            }));
          
          // Resolve with user-configured icons
          resolve({
            type: 'icons',
            value: { icons }
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

The Iframe method allows you to create a fully custom interface for icon configuration using any web technology. Your iframe application communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal when you need a rich UI for icon selection, URL configuration, or visual preview of icon arrangements before insertion into the email template.

**Required postMessage Communication**

Implement the standard postMessage protocol to integrate your iframe with Beefree. First, notify Beefree when your iframe is loaded and specify the dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes configuring icons, send "onSave" with your icons array. If the user cancels, send "onCancel" to close the dialog without inserting content.

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

**2. Listen for "init" message from Beefree:**

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Editor locale:', data.locale);
    // Initialize your icon configuration UI
  }
});
```

**3. Send "onSave" with icon data:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'icons',
    value: {
      icons: [
        {
          image: 'https://example.com/icons/facebook.png',
          href: 'https://facebook.com',
          alt: 'Facebook',
          width: '32px',
          height: '32px'
        }
        // ... more icons
      ]
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

This complete HTML example provides a functional icon configuration interface. It demonstrates the full postMessage protocol and includes simple inputs for configuring a social media icon set. Users can enter their social profile URLs, and the interface automatically generates properly formatted icons. You can expand this basic example with icon selection, image uploads, custom styling options, or visual preview capabilities.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Icon Configurator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    .icon-input {
      margin: 15px 0;
    }
    input {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <h2>Configure Social Icons</h2>
  <div class="icon-input">
    <label>Facebook URL:</label>
    <input type="url" id="facebookUrl" placeholder="https://facebook.com/yourpage">
  </div>
  <div class="icon-input">
    <label>Twitter URL:</label>
    <input type="url" id="twitterUrl" placeholder="https://twitter.com/yourhandle">
  </div>
  <div class="icon-input">
    <label>Instagram URL:</label>
    <input type="url" id="instagramUrl" placeholder="https://instagram.com/yourhandle">
  </div>
  <button onclick="insertIcons()">Insert Icons</button>
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

    function insertIcons() {
      const icons = [];
      
      // Facebook
      const fbUrl = document.getElementById('facebookUrl').value;
      if (fbUrl) {
        icons.push({
          image: 'https://example.com/icons/facebook.png',
          text: 'Facebook',
          href: fbUrl,
          target: '_blank',
          alt: 'Facebook',
          width: '32px',
          height: '32px',
          textPosition: 'bottom'
        });
      }
      
      // Twitter
      const twitterUrl = document.getElementById('twitterUrl').value;
      if (twitterUrl) {
        icons.push({
          image: 'https://example.com/icons/twitter.png',
          text: 'Twitter',
          href: twitterUrl,
          target: '_blank',
          alt: 'Twitter',
          width: '32px',
          height: '32px',
          textPosition: 'bottom'
        });
      }
      
      // Instagram
      const instaUrl = document.getElementById('instagramUrl').value;
      if (instaUrl) {
        icons.push({
          image: 'https://example.com/icons/instagram.png',
          text: 'Instagram',
          href: instaUrl,
          target: '_blank',
          alt: 'Instagram',
          width: '32px',
          height: '32px',
          textPosition: 'bottom'
        });
      }
      
      // Validate that at least one icon was provided
      if (icons.length === 0) {
        alert('Please enter at least one social media URL');
        return;
      }
      
      // Send icons to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'icons',
          value: { icons }
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
