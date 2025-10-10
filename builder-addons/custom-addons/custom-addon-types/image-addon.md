# Image AddOn

## Overview

The Image AddOn type allows you to insert image content blocks into the Beefree editor. When users interact with your Image AddOn, it inserts an image module with properties like source URL, alt text, link destination, and link target behavior.

**What Makes Image AddOns Special**

Image AddOns are ideal when you want to provide users with:

* Access to external image libraries (stock photos, brand assets, etc.)
* Dynamic image generation or selection
* Pre-configured image content from your systems

Unlike manually adding images, Image AddOns let you control the source, apply business logic, and integrate with external services.

## Prerequisites

Before implementing an Image AddOn in your code, you first need to create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/). Take the following steps to complete this:

1. Log into the [Developer Console](https://developers.beefree.io/login) and navigate to your application.
2. Create a new Custom AddOn and select **Image** as the type.
3. Configure the addon with a unique **handle** (e.g., `my-image-addon`).
4. Choose your implementation method ([Content Dialog](../build-addons-with-content-dialog.md) or [External iframe](../build-addons-with-external-iframe/)).
5. Save the addon configuration.

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

## Content Object Schema

This section discusses the Image AddOn's object schema. Understanding this schema is a core part of successfully implementing a Custom Image AddOn type.

Visit the complete [Unified Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json) to see a comprehensive reference on how to structure data for all Custom Addons.

**Required Structure**

The Image AddOn schema defines the structure for inserting images into the editor. The `src` property is the image URL that will be displayed, while `alt` provides accessibility text for screen readers and displays when images fail to load. Optional properties like `href` make the image clickable, and `dynamicSrc` enables personalization through merge tags for dynamic content at send time.

```javascript
{
  type: 'image',
  value: {
    alt: string,         // Required: Alt text for accessibility
    src: string,         // Required: Image URL
    href: string,        // Optional: Link destination
    dynamicSrc: string,  // Optional: Merge tag for dynamic src
    target: string       // Optional: '_self', '_blank', etc.
  }
}
```

**Basic Example**

This example shows a simple image insertion with only the required properties. The `src` provides the image URL, and `alt` ensures accessibility by describing the image content for users with screen readers or when the image fails to load.

```javascript
resolve({
  type: 'image',
  value: {
    alt: 'A beautiful landscape',
    src: 'https://example.com/images/landscape.jpg'
  }
});
```

**Complete Example with Link**

This comprehensive example demonstrates all commonly used image properties. The `href` makes the image clickable, `target: '_blank'` opens the link in a new tab, and the descriptive `alt` text improves accessibility. This pattern is perfect for promotional images, product photos, or any clickable visual content in email campaigns.

```javascript
resolve({
  type: 'image',
  value: {
    alt: 'Summer sale banner - Click to shop now',
    src: 'https://example.com/images/summer-sale.jpg',
    href: 'https://example.com/summer-sale',
    target: '_blank'
  }
});
```

**Dynamic Image Example**

This advanced example uses merge tags for personalization, allowing different images for each email recipient. The `src` provides a fallback image shown in the editor and testing, while `dynamicSrc` contains a merge tag that your email platform replaces with recipient-specific values at send time. This enables personalized product recommendations, user-specific content, or customized visuals based on recipient data.

```javascript
resolve({
  type: 'image',
  value: {
    alt: 'Your recommended product',
    src: 'https://example.com/images/default-product.jpg',
    dynamicSrc: '{{user_recommended_product_image}}',
    href: '{{user_recommended_product_url}}',
    target: '_blank'
  }
});
```

## Content Dialog Implementation

This section covers how to implement a Custom Image AddOn using the [Content Dialog method](../build-addons-with-content-dialog.md). It includes code snippets for three different scenarios:

* **Scenario 1:**[ Instantly insert a pre-defined image](image-addon.md#instantly-insert-a-pre-defined-image)
* **Scenario 2:** [End user selection](image-addon.md#end-user-selection)
* **Scenario 3:** [Multiple addons](image-addon.md#multiple-addons)&#x20;

### **Instantly insert a pre-defined image**

The Content Dialog method enables programmatic image insertion through a JavaScript handler function. When users drag your image addon onto the stage, this handler is called with `resolve` and `reject` callbacks. Call `resolve` with your image object to insert it immediately, or open a dialog first to let users select or configure the image. This basic pattern provides instant insertion with a predefined image.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-image-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for image insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-image-addon') {
          // Immediately insert an image
          resolve({
            type: 'image',
            value: {
              alt: 'Welcome image',
              src: 'https://example.com/images/welcome.jpg',
              href: 'https://example.com',
              target: '_blank'
            }
          });
        }
      }
    }
  }
};
```

### **End User Selection**

This pattern demonstrates opening a custom interface for image selection before insertion. The handler waits for user interaction, displaying available images or allowing uploads. Once the user selects an image, the `onSelect` callback resolves with the chosen image data. The `onCancel` callback rejects the insertion if the user abandons the selection, providing a complete user-driven workflow for image insertion.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom image selection UI
      // Replace 'yourImageSelector' with your actual UI component
      yourImageSelector.open({
        onSelect: (selectedImage) => {
          // User selected an image - resolve with image data
          resolve({
            type: 'image',
            value: {
              alt: selectedImage.description,
              src: selectedImage.imageUrl,
              href: selectedImage.linkUrl,
              target: '_blank'
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

### **Multiple AddOns**

When managing multiple image addons, this pattern shows how to handle them in a single handler using `args.contentDialogId`. This allows you to organize different image sources (stock photos, product images, brand assets) under one handler function. The switch statement routes each addon to its appropriate logic, maintaining clean code organization while supporting diverse image insertion workflows.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Handle different image addons based on their ID
      switch (args.contentDialogId) {
        case 'stock-photos-addon':
          // Immediate insertion for stock photos
          resolve({
            type: 'image',
            value: {
              alt: 'Stock photo',
              src: 'https://example.com/stock/random.jpg'
            }
          });
          break;
          
        case 'product-images-addon':
          // Open dialog for product selection
          yourProductSelector.open({
            onSelect: (product) => resolve({
              type: 'image',
              value: {
                alt: product.name,
                src: product.imageUrl,
                href: product.productPageUrl
              }
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

## Iframe Implementation

This section discusses how to implement the Custom Image AddOn using the Iframe implementation method. It includes the core concepts you need to understand to successfully implement Image AddOns using an Iframe workflow.

**Conceptual Flow**

The Iframe method provides complete UI flexibility by loading your custom web application inside the Beefree editor. Your iframe communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal for complex image selection interfaces, image editing tools, asset management systems, or any scenario where you need full control over the user interface and interaction flow.

**Required postMessage Communication**

Your iframe must implement a specific message protocol to integrate with Beefree. First, send "loaded" to notify Beefree your UI is ready and specify dialog dimensions. Listen for "init" to receive editor context like locale and state. When ready to insert an image, send "onSave" with your image object. Send "onCancel" if the user abandons the action. This bidirectional communication creates a seamless integration between your custom UI and the Beefree editor.

**1. Send "loaded" when your iframe is ready:**

```javascript
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

**2. Listen for "init" and "load" messages from Beefree:**

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Editor locale:', data.locale);
    // Initialize your image selection UI with context from Beefree
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing image
    if (data && data.value) {
      document.getElementById('imageUrl').value = data.value.src || '';
      document.getElementById('altText').value = data.value.alt || '';
      document.getElementById('linkUrl').value = data.value.href || '';
    }
  }
});
```

**3. Send "onSave" with image data:**

```javascript
// When user selects an image and clicks insert
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'image',
    value: {
      alt: 'Selected image',
      src: 'https://example.com/images/selected.jpg',
      href: 'https://example.com/link',
      target: '_blank'
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

This complete HTML example demonstrates a functional image selection interface that integrates with Beefree. It includes the full postMessage protocol implementation, simple URL input for image selection, and proper save/cancel handling. You can enhance this basic example with image galleries, file upload capabilities, search functionality, or visual preview to create a more sophisticated image selection experience.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Image Selector</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    input {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
    .preview {
      margin: 20px 0;
      max-width: 100%;
    }
    .preview img {
      max-width: 100%;
      height: auto;
    }
  </style>
</head>
<body>
  <h2>Select Image</h2>
  <input type="url" id="imageUrl" placeholder="Image URL" value="https://example.com/images/sample.jpg">
  <input type="text" id="altText" placeholder="Alt text" value="Sample image">
  <input type="url" id="linkUrl" placeholder="Link URL (optional)">
  
  <div class="preview">
    <h3>Preview:</h3>
    <img id="previewImg" src="https://example.com/images/sample.jpg" alt="Preview">
  </div>
  
  <button onclick="insertImage()">Insert Image</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Notify Beefree that iframe is loaded and ready
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

    // Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data;
      
      if (action === 'init') {
        console.log('Editor locale:', data?.locale);
      }
      
      if (action === 'load' && data?.value) {
        // Pre-populate when editing existing image
        document.getElementById('imageUrl').value = data.value.src || '';
        document.getElementById('altText').value = data.value.alt || '';
        document.getElementById('linkUrl').value = data.value.href || '';
        updatePreview();
      }
    });

    // Update preview when URL changes
    document.getElementById('imageUrl').addEventListener('input', function(e) {
      document.getElementById('previewImg').src = e.target.value;
    });

    function insertImage() {
      const src = document.getElementById('imageUrl').value;
      const alt = document.getElementById('altText').value;
      const href = document.getElementById('linkUrl').value;
      
      // Validate required fields
      if (!src || !alt) {
        alert('Please fill in Image URL and Alt Text');
        return;
      }
      
      // Build image data object
      const imageData = {
        type: 'image',
        value: { src, alt }
      };
      
      // Add optional link if provided
      if (href) {
        imageData.value.href = href;
        imageData.value.target = '_blank';
      }
      
      // Send image data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: imageData
      }, '*');
    }

    function cancel() {
      window.parent.postMessage({ action: 'onCancel' }, '*');
    }
  </script>
</body>
</html>
```
