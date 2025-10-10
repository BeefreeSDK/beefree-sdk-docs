# Mixed Content AddOn

## Overview

The Mixed Content AddOn type allows you to insert multiple content modules at once in a single drop action. Instead of inserting just one type of content (like an image or a paragraph), Mixed Content AddOns can insert a combination of different modules together—such as an image followed by a title, description, and button.

**What Makes Mixed Content AddOns Powerful**

Mixed Content AddOns solve a common problem: **repetitive multi-step content creation**. Instead of users manually dragging individual modules and configuring each separately, they can drop a single Mixed Content AddOn that inserts all elements at once, pre-configured and ready to use. This dramatically speeds up content creation while maintaining consistency.

## Prerequisites

Before implementing a Mixed Content AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/). Take the following steps to complete this:

1. Log into the [Developer Console](https://developers.beefree.io/login) and navigate to your application.
2. Create a new Custom AddOn and select **Mixed** as the type.
3. Configure the addon with a unique **handle** (for example, `my-mixed-addon`).
4. Choose your implementation method ([Content Dialog](../build-addons-with-content-dialog.md) or [External iframe](../build-addons-with-external-iframe/)).
5. Save the addon configuration.

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

## Content Object Schema

This section discusses the Mixed AddOn's object schema. Understanding this schema is a core part of successfully implementing a Custom Mixed AddOn type.

Visit the complete [Unified Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json) to see a comprehensive reference on how to structure data for all Custom Addons.

**Required Structure**

The Mixed Content AddOn uses a unique structure where the `value` property is an array of content module objects rather than a single object. Each module in the array follows its own type's schema (image, paragraph, button, etc.), and they'll be inserted sequentially on the stage. The optional `mergeTags` array allows you to define personalization tags that work across all modules in the set.

{% hint style="warning" %}
**Important:** Within Mixed Content, titles use `type: 'title'` (not `type: 'heading'`). This is different from standalone Title AddOns which use `type: 'heading'`.
{% endhint %}

```javascript
{
  type: 'mixed',
  value: [
    // Array of content module objects
    { type: 'image', value: {...} },
    { type: 'paragraph', value: {...} },
    { type: 'button', value: {...} }
  ],
  mergeTags: [  // Optional
    { name: 'Field Name', value: '@tag', previewValue: 'Preview' }
  ]
}
```

**Simple Example**

This basic example demonstrates inserting two modules together—an image followed by descriptive text. When dropped on the stage, both modules appear sequentially, creating a simple content block. This pattern is perfect for basic content combinations that users would otherwise need to create manually by dragging two separate modules.

```javascript
resolve({
  type: 'mixed',
  value: [
    {
      type: 'image',
      value: {
        src: 'https://example.com/welcome.jpg',
        alt: 'Welcome image'
      }
    },
    {
      type: 'paragraph',
      value: {
        html: '<p>Welcome to our newsletter! We\'re excited to share our latest updates with you.</p>'
      }
    }
  ]
});
```

**Complete Example**

This comprehensive example shows a full content block combining four different module types in a logical flow: an image to capture attention, a title for the heading, descriptive text, and a call-to-action button. Each module maintains its own schema and properties, but they're inserted together as a cohesive unit. This pattern is ideal for promotional blocks, product features, or any structured content that benefits from consistent layout.

{% hint style="warning" %}
Note: Button properties like `border-radius` and padding values must be **numbers** (representing pixels), not strings.
{% endhint %}

```javascript
resolve({
  type: 'mixed',
  value: [
    {
      type: 'image',
      value: {
        alt: 'Featured product',
        src: 'https://example.com/images/product.jpg',
        href: 'https://example.com/product'
      }
    },
    {
      type: 'title',  // Note: 'title' not 'heading' in mixed content
      value: {
        text: 'Introducing Our New Product',
        align: 'center',
        size: 28,
        color: '#333333'
      }
    },
    {
      type: 'paragraph',
      value: {
        html: '<p>Discover the amazing features of our latest product designed to make your life easier.</p>',
        color: '#666666'
      }
    },
    {
      type: 'button',
      value: {
        label: 'Learn More',
        href: 'https://example.com/product',
        'background-color': '#0066CC',
        color: '#FFFFFF',
        'border-radius': 4,         // Number, not string
        'padding-top': 12,          // Number, not string
        'padding-right': 24,        // Number, not string
        'padding-bottom': 12,       // Number, not string
        'padding-left': 24          // Number, not string
      }
    }
  ]
});
```

## Content Dialog Implementation

This section covers how to implement a Custom Mixed AddOn using the [Content Dialog method](../build-addons-with-content-dialog.md). It includes code snippets for three different scenarios:

* **Scenario 1:** [Pre-defined mixed content](mixed-content-addon.md#pre-defined-mixed-content)
* **Scenario 2:** [Building from data](mixed-content-addon.md#building-from-data)
* **Scenario 3:** [With user selection](mixed-content-addon.md#with-user-selection)

### **Pre-defined mixed content**

The Content Dialog method allows programmatic insertion of multiple modules through a JavaScript handler. When users drag your mixed content addon onto the stage, this handler is invoked and immediately resolves with an array of module objects. This pattern works perfectly for predefined content blocks that don't require user input, providing instant insertion of complete, multi-module content structures.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-mixed-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for mixed content insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-mixed-addon') {
          // Check if triggered by dropping the addon (vs editing existing)
          if (args.hasOpenOnDrop) {
            // Immediately insert multiple modules together
            resolve({
              type: 'mixed',
              value: [
                {
                  type: 'image',
                  value: {
                    alt: 'Content image',
                    src: 'https://example.com/image.jpg'
                  }
                },
                {
                  type: 'title',  // Note: 'title' not 'heading'
                  value: {
                    text: 'Welcome!',
                    align: 'center',
                    size: 28
                  }
                },
                {
                  type: 'paragraph',
                  value: {
                    html: '<p>This is descriptive text that follows the image.</p>'
                  }
                },
                {
                  type: 'button',
                  value: {
                    label: 'Click Here',
                    href: 'https://example.com',
                    'background-color': '#0066CC',
                    color: '#FFFFFF',
                    'border-radius': 4,
                    'padding-top': 12,
                    'padding-right': 24,
                    'padding-bottom': 12,
                    'padding-left': 24
                  }
                }
              ]
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

### **Building from Data**

This pattern demonstrates constructing mixed content from structured data, making it easy to create content blocks from dynamic sources like APIs, databases, or user selections. By transforming your data into the proper module array format, you can generate consistent content blocks while maintaining flexibility in the source data structure. This approach is particularly valuable when integrating with external content management systems or product catalogs.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Example data (could come from API, database, etc.)
      const contentData = {
        title: 'Summer Sale',
        description: 'Save up to 50% on select items this weekend only!',
        imageUrl: 'https://example.com/sale-banner.jpg',
        buttonText: 'Shop Now',
        buttonUrl: 'https://example.com/sale'
      };
      
      // Build mixed content from data
      resolve({
        type: 'mixed',
        value: [
          {
            type: 'image',
            value: {
              src: contentData.imageUrl,
              alt: contentData.title,
              href: contentData.buttonUrl
            }
          },
          {
            type: 'title',  // Note: 'title' not 'heading' in mixed content
            value: {
              text: contentData.title,
              align: 'center',
              size: 28
            }
          },
          {
            type: 'paragraph',
            value: {
              html: `<p>${contentData.description}</p>`
            }
          },
          {
            type: 'button',
            value: {
              label: contentData.buttonText,
              href: contentData.buttonUrl,
              'background-color': '#0066CC',
              color: '#FFFFFF',
              'border-radius': 4,
              'padding-top': 12,
              'padding-right': 24,
              'padding-bottom': 12,
              'padding-left': 24
            }
          }
        ]
      });
    }
  }
}
```

### **With User Selection**

This advanced pattern shows how to let users select or configure content before insertion. By opening a custom interface, users can choose which content to include or provide specific details like text, images, and links. The handler waits for user confirmation, then builds the mixed content array based on their selections. This provides maximum flexibility while maintaining the efficiency of multi-module insertion.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for content configuration
      // Replace 'yourContentSelector' with your actual UI component
      yourContentSelector.open({
        onSelect: (selectedContent) => {
          // User confirmed - build mixed content from selections
          const modules = [];
          
          // Add image if provided
          if (selectedContent.imageUrl) {
            modules.push({
              type: 'image',
              value: {
                src: selectedContent.imageUrl,
                alt: selectedContent.title
              }
            });
          }
          
          // Add title if provided
          if (selectedContent.title) {
            modules.push({
              type: 'title',  // Note: 'title' not 'heading' in mixed content
              value: {
                text: selectedContent.title,
                align: 'center',
                size: 28
              }
            });
          }
          
          // Add description if provided
          if (selectedContent.description) {
            modules.push({
              type: 'paragraph',
              value: {
                html: `<p>${selectedContent.description}</p>`
              }
            });
          }
          
          // Add button if URL provided
          if (selectedContent.buttonUrl) {
            modules.push({
              type: 'button',
              value: {
                label: selectedContent.buttonText || 'Learn More',
                href: selectedContent.buttonUrl,
                'background-color': '#0066CC',
                color: '#FFFFFF',
                'border-radius': 4,
                'padding-top': 12,
                'padding-right': 24,
                'padding-bottom': 12,
                'padding-left': 24
              }
            });
          }
          
          // Resolve with user-configured content
          resolve({
            type: 'mixed',
            value: modules
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

This section discusses how to implement the Custom Mixed AddOn using the Iframe implementation method. It includes the core concepts you need to understand to successfully implement Mixed AddOns using an Iframe workflow.

**Conceptual Flow**

The Iframe method provides complete UI flexibility by loading your custom web application inside the Beefree editor. Your iframe communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal for complex content builders, template selectors, or rich configuration interfaces where you need full control over how users create and configure multi-module content blocks before insertion.

**Required postMessage Communication**

Your iframe must implement the standard postMessage protocol to integrate with Beefree. First, notify Beefree when your iframe is loaded and specify dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes configuring their content, send "onSave" with your mixed content array. If the user cancels, send "onCancel" to close without inserting. This communication pattern ensures seamless integration between your custom UI and the Beefree editor.

**1. Send "loaded" when your iframe is ready:**

```javascript
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '800px',
    height: '700px',
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
    // Initialize your content builder UI
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing mixed content
    if (data && data.value && Array.isArray(data.value)) {
      data.value.forEach(item => {
        if (item.type === 'image') {
          document.getElementById('imageUrl').value = item.value?.src || '';
        } else if (item.type === 'title') {
          document.getElementById('title').value = item.value?.text || '';
        } else if (item.type === 'paragraph') {
          const tempDiv = document.createElement('div');
          tempDiv.innerHTML = item.value?.html || '';
          document.getElementById('description').value = tempDiv.textContent || '';
        } else if (item.type === 'button') {
          document.getElementById('buttonText').value = item.value?.label || '';
          document.getElementById('buttonUrl').value = item.value?.href || '';
        }
      });
    }
  }
});
```

**3. Send "onSave" with mixed content:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'mixed',
    value: [
      {
        type: 'image',
        value: {
          src: 'https://example.com/image.jpg',
          alt: 'Content image'
        }
      },
      {
        type: 'title',  // Note: 'title' not 'heading' in mixed content
        value: {
          text: 'Welcome!',
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
          label: 'Click Here',
          href: 'https://example.com',
          'background-color': '#0066CC',
          color: '#FFFFFF',
          'border-radius': 4,
          'padding-top': 12,
          'padding-right': 24,
          'padding-bottom': 12,
          'padding-left': 24
        }
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

This complete HTML example demonstrates a functional content block builder interface. It includes the full postMessage protocol implementation and provides simple inputs for creating a mixed content block with an image, title, description, and button. Users can configure each component, and the interface builds the proper mixed content structure for Beefree. You can expand this basic example with preview capabilities, template selection, advanced styling options, or integration with external content sources.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Content Block Builder</title>
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
    input, textarea {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
    }
    textarea {
      height: 80px;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <h2>Create Content Block</h2>
  
  <div class="field">
    <label>Image URL:</label>
    <input type="url" id="imageUrl" placeholder="https://example.com/image.jpg" value="https://example.com/featured.jpg">
  </div>
  
  <div class="field">
    <label>Title:</label>
    <input type="text" id="title" placeholder="Content title" value="Welcome!">
  </div>
  
  <div class="field">
    <label>Description:</label>
    <textarea id="description" placeholder="Content description">This is a sample content block with an image, title, description, and call-to-action button.</textarea>
  </div>
  
  <div class="field">
    <label>Button Text:</label>
    <input type="text" id="buttonText" placeholder="Button text" value="Learn More">
  </div>
  
  <div class="field">
    <label>Button URL:</label>
    <input type="url" id="buttonUrl" placeholder="https://example.com" value="https://example.com">
  </div>
  
  <button onclick="insertContent()">Insert Content Block</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Notify Beefree that iframe is loaded and ready
    window.parent.postMessage({
      action: 'loaded',
      data: { 
        width: '800px', 
        height: '700px',
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
      
      if (action === 'load' && data?.value && Array.isArray(data.value)) {
        // Pre-populate when editing existing mixed content
        data.value.forEach(item => {
          if (item.type === 'image') {
            document.getElementById('imageUrl').value = item.value?.src || '';
          } else if (item.type === 'title') {
            document.getElementById('title').value = item.value?.text || '';
          } else if (item.type === 'paragraph') {
            const tempDiv = document.createElement('div');
            tempDiv.innerHTML = item.value?.html || '';
            document.getElementById('description').value = tempDiv.textContent || '';
          } else if (item.type === 'button') {
            document.getElementById('buttonText').value = item.value?.label || '';
            document.getElementById('buttonUrl').value = item.value?.href || '';
          }
        });
      }
    });

    function insertContent() {
      const imageUrl = document.getElementById('imageUrl').value;
      const title = document.getElementById('title').value;
      const description = document.getElementById('description').value;
      const buttonText = document.getElementById('buttonText').value;
      const buttonUrl = document.getElementById('buttonUrl').value;
      
      // Validate required fields
      if (!imageUrl || !title || !description) {
        alert('Please fill in all required fields');
        return;
      }
      
      // Build mixed content array
      const modules = [];
      
      if (imageUrl) {
        modules.push({
          type: 'image',
          value: {
            src: imageUrl,
            alt: title || 'Content image'
          }
        });
      }
      
      if (title) {
        modules.push({
          type: 'title',  // Note: 'title' not 'heading' in mixed content
          value: {
            text: title,
            align: 'center',
            size: 28,
            color: '#333333'
          }
        });
      }
      
      if (description) {
        modules.push({
          type: 'paragraph',
          value: {
            html: `<p>${description}</p>`
          }
        });
      }
      
      if (buttonText && buttonUrl) {
        modules.push({
          type: 'button',
          value: {
            label: buttonText,
            href: buttonUrl,
            'background-color': '#0066CC',
            color: '#FFFFFF',
            'border-radius': 4,
            'padding-top': 12,
            'padding-right': 24,
            'padding-bottom': 12,
            'padding-left': 24
          }
        });
      }
      
      // Send mixed content to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'mixed',
          value: modules
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

#### Available Module Types

You can combine any of these module types in a Mixed Content AddOn:

* **image** - Images with links
* **paragraph** - Text content with HTML
* **button** - Call-to-action buttons
* **title** - Titles/headings (use `type: 'title'` in mixed content, not `'heading'`)
* **list** - Ordered or unordered lists
* **menu** - Navigation menus
* **icons** - Icon sets with links
* **html** - Custom HTML markup

**Note:** You cannot nest Mixed Content AddOns or Row AddOns inside another Mixed Content AddOn.
