# Build AddOns with Content Dialog

## Overview

The **Content Dialog Method** is the simplest way to build Custom AddOns when your AddOn logic and UI are hosted within the same application as the Beefree SDK editor. This method allows you to use JavaScript handler functions that run in your application's context, giving you direct access to your app's data, services, and UI components without the complexity of iframe communication.

## Quick Setup

**1. Create AddOn in Console**

Before writing any code, you must first create the addon configuration in the Beefree SDK Developer Console. This establishes the addon's identity and settings that your code will reference.

Log into [developers.beefree.io](https://developers.beefree.io/):

* Navigate to your app → **AddOns** → **Create a custom AddOn**
* Fill out the form (Name, Type, Handle, etc.)
* **Method**: Select `Content Dialog`
* **Handle**: Remember this! You'll need it in code

**2. Configure beeConfig**

The `beeConfig` object is where you define how Beefree SDK behaves, including your addon handlers. The `contentDialog.addOn.handler` function is called whenever users interact with your addon, and it receives three parameters: `resolve` (to insert content), `reject` (to cancel), and `args` (context information). This handler function is the heart of the Content Dialog method—it's where you determine what content gets inserted based on your business logic.

Add your handler to `beeConfig`:

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-addon-handle') {
          // Your addon logic goes here
          // Call resolve() with a content object to insert content
          // Call reject() to cancel the operation
          
          resolve({
            type: 'html',
            value: {
              html: '<div>Hello World!</div>'
            }
          });
        }
      }
    }
  }
};
```

**3. Initialize Beefree SDK**

Once your `beeConfig` is defined with the handler, you initialize the Beefree SDK with your authentication token and configuration. The `bee.start()` method loads the editor with an optional template parameter, which can be a saved email template JSON or undefined for a blank canvas. This initialization connects your handler function to the Beefree editor, making your addon functional.

```javascript
const bee = new BeePlugin(token, beeConfig);
bee.start(template);
```

## Handler Function

The handler is called when users interact with your AddOn. Understanding the handler function signature is crucial—it follows a promise-like pattern where you either `resolve` with content to insert or `reject` to abort. The `args` parameter provides valuable context like which specific addon was triggered and whether it was opened automatically via Direct Open, allowing you to create sophisticated conditional logic.

```javascript
handler: (resolve, reject, args) => {
  // Three parameters:
  // - resolve: function to call with content object
  // - reject: function to call on cancel/error
  // - args: context information
}
```

**Handler Arguments**

The `args` object contains contextual information about how and why your handler was invoked. The `contentDialogId` matches the handle you created in the Developer Console, allowing a single handler to manage multiple addons. The `hasOpenOnDrop` boolean indicates if the addon was triggered via Direct Open (automatic on drop) versus manual opening. The `metadata` property contains any previously saved custom data if the user is editing existing content, enabling stateful addons that remember their configuration.

```javascript
handler: (resolve, reject, args) => {
  console.log(args.contentDialogId);  // Your AddOn handle from Console
  console.log(args.hasOpenOnDrop);    // true if Direct Open triggered
  console.log(args.metadata);         // Previously saved data (if editing)
}
```

## Implementation Patterns

**Pattern 1: Immediate Resolution**

This pattern resolves instantly without user interaction, perfect for addons that generate or fetch content programmatically. When the handler is called, it immediately creates a content object and resolves, inserting the content into the editor. This is ideal for auto-generated content like timestamps, random images, pre-formatted text blocks, or any content that doesn't require user configuration.

Insert content immediately without user interaction:

```javascript
handler: (resolve, reject, args) => {
  // Check which addon triggered this handler
  if (args.contentDialogId === 'my-quick-html-addon') {
    // Immediately insert content when addon is triggered
    // This example creates a simple HTML block with contextual information
    resolve({
      type: 'html',
      value: {
        html: '<div style="padding: 20px; background-color: #f0f0f0;"><p>Hello World! This content was inserted automatically.</p></div>'
      }
    });
  }
}
```

**Use when:** Content doesn't require user input (e.g., auto-generated content, default blocks, timestamps).

**Pattern 2: With Modal Dialog**

This pattern shows a custom UI for user input before inserting content. Your handler opens a modal or dialog (using your application's UI framework), waits for the user to make selections or provide input, then resolves with the configured content when they confirm. If they cancel, you call `reject()` to abort the insertion. This gives users full control over what content is inserted while maintaining a guided workflow.

Show a dialog for user input, then resolve:

```javascript
handler: (resolve, reject, args) => {
  // Check which addon triggered this handler
  if (args.contentDialogId === 'my-text-editor-addon') {
    // Open your custom modal/dialog system
    // Replace 'yourModalSystem' with your actual UI implementation
    yourModalSystem.open({
      title: 'Configure Content',
      content: 'Enter your content settings',
      
      // User confirmed - insert their configured content
      onConfirm: (userInput) => {
        resolve({
          type: 'paragraph',
          value: {
            html: `<p>${userInput.text}</p>`,
            color: userInput.color || '#333333'
          }
        });
      },
      
      // User canceled - abort without inserting anything
      onCancel: () => reject()
    });
  }
}
```

**Use when:** Users need to make selections or provide input (e.g., text editors, image selectors, configuration dialogs).

**Pattern 3: Multiple AddOns**

When you have multiple custom addons registered in the Developer Console, you can handle them all in a single handler function by checking `args.contentDialogId`. The switch statement routes each addon to its appropriate logic, keeping your code organized while supporting diverse addon types. This pattern is particularly useful when different addons share common functionality or data sources—you can reuse helper functions and maintain all addon logic in one place.

Handle different AddOns with a switch statement:

```javascript
handler: (resolve, reject, args) => {
  // Wrap in try-catch for error handling
  try {
    // Route to different logic based on which addon was triggered
    switch (args.contentDialogId) {
      case 'simple-text-addon':
        // Immediate insertion for simple addon
        resolve({
          type: 'paragraph',
          value: {
            html: '<p>Simple text block inserted!</p>'
          }
        });
        break;
        
      case 'image-selector-addon':
        // Open image picker for complex addon
        yourImageSelector.open({
          onSelect: (selectedImage) => resolve({
            type: 'image',
            value: { 
              src: selectedImage.url, 
              alt: selectedImage.description 
            }
          }),
          onCancel: () => reject()
        });
        break;
        
      case 'content-library-addon':
        // Open content library browser
        yourContentLibrary.open({
          onSelect: (content) => resolve(content),
          onCancel: () => reject()
        });
        break;
        
      default:
        // Unknown addon - log error and reject
        console.error('Unknown addon ID:', args.contentDialogId);
        reject(new Error('Unknown AddOn'));
    }
  } catch (error) {
    console.error('AddOn error:', error);
    reject(error);
  }
}
```

**Use when:** Managing multiple Custom AddOns in one handler.

**Pattern 4: Conditional Logic with Direct Open**

The Direct Open feature allows addons to insert content automatically when dragged onto the stage, without requiring the user to manually open a dialog. This pattern detects whether the addon was triggered via Direct Open (`args.hasOpenOnDrop === true`) and provides different behavior: automatic insertion with default content for drag-and-drop, or opening a full configuration dialog when manually triggered. This creates an efficient workflow where users can quickly insert default content but still have access to full customization when needed.

Different behavior based on how AddOn was triggered:

```javascript
handler: (resolve, reject, args) => {
  if (args.contentDialogId === 'my-button-addon') {
    if (args.hasOpenOnDrop) {
      // User dragged addon onto stage - insert default content immediately
      // This provides a fast workflow for common use cases
      resolve({
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
      });
    } else {
      // User manually opened addon - show full customization dialog
      // This allows advanced configuration when needed
      yourCustomDialog.open({
        onConfirm: (config) => resolve({
          type: 'button',
          value: {
            label: config.buttonText,
            href: config.url,
            'background-color': config.color,
            color: '#FFFFFF',
            'border-radius': 4,
            'padding-top': 12,
            'padding-right': 24,
            'padding-bottom': 12,
            'padding-left': 24
          }
        }),
        onCancel: () => reject()
      });
    }
  }
}
```

**Use when:** Combining Direct Open with manual triggering for flexible user workflows.

## Content Object Structure

Every call to `resolve()` must include a properly formatted content object that matches Beefree's schema for the addon type. The `type` property specifies what kind of content you're inserting (image, html, button, etc.), the `value` object contains the type-specific properties and configuration, and the optional `mergeTags` array defines personalization fields for dynamic content. Understanding these schemas is critical—incorrect structures will cause insertion to fail silently or produce unexpected results.

Every `resolve()` call requires a properly formatted content object:

```javascript
{
  type: string,        // AddOn type: 'image', 'html', 'mixed', etc.
  value: object,       // Type-specific properties
  mergeTags: array     // Optional: for personalization
}
```

**Examples by Type**

Each addon type has its own specific schema requirements. Below are examples showing the minimal required properties for common addon types—these are the building blocks you'll use in your handler's `resolve()` calls.

**Image:**

```javascript
resolve({
  type: 'image',
  value: {
    src: 'https://example.com/welcome.jpg',
    alt: 'Welcome image description'
  }
});
```

**HTML:**

```javascript
resolve({
  type: 'html',
  value: {
    html: '<div style="padding: 20px;"><h2>Custom HTML Block</h2><p>This is a custom HTML content block.</p></div>'
  }
});
```

**Button:**

{% hint style="warning" %}
**Important:** Button properties like `border-radius` and all padding values must be **numbers**, not strings.
{% endhint %}

```javascript
resolve({
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
});
```

**Paragraph:**

```javascript
resolve({
  type: 'paragraph',
  value: {
    html: '<p>This is a paragraph of text that will be inserted into the email.</p>',
    color: '#333333'
  }
});
```

**Mixed Content:**

{% hint style="warning" %}
**Important:** Within Mixed Content, titles use `type: 'title'` (not `type: 'heading'`). This is different from standalone Title AddOns which use `type: 'heading'`.
{% endhint %}

```javascript
resolve({
  type: 'mixed',
  value: [
    { 
      type: 'image', 
      value: { 
        src: 'https://example.com/feature.jpg', 
        alt: 'Feature image' 
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
        html: '<p>Feature description text</p>' 
      } 
    },
    {
      type: 'button',
      value: {
        label: 'Learn More',
        href: 'https://example.com/features',
        'background-color': '#0066CC',
        'border-radius': 4,
        'padding-top': 12,
        'padding-right': 24,
        'padding-bottom': 12,
        'padding-left': 24
      }
    }
  ]
});
```

See [AddOn Types](custom-addon-types/) for complete schemas.

## Complete Example

This comprehensive example demonstrates a working implementation with multiple addons, Direct Open support, conditional logic, and error handling. It shows how to structure your `beeConfig` with the `addOns` array for Direct Open configuration and a unified handler that manages different addon types with appropriate workflows. This pattern represents real-world addon development—multiple addons with different behaviors, user interaction patterns, and error handling all working together in one cohesive system.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable Direct Open for specific addons (optional)
  addOns: [
    { id: 'quick-text-addon', openOnDrop: true },
    { id: 'image-library-addon', openOnDrop: false }
  ],
  
  // Configure unified handler for all addons
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Log context for debugging
        console.log('AddOn triggered:', args);
        console.log('contentDialogId:', args.contentDialogId);
        console.log('hasOpenOnDrop:', args.hasOpenOnDrop);
        
        // Wrap in try-catch for error handling
        try {
          // Route based on addon ID
          switch (args.contentDialogId) {
            case 'quick-text-addon':
              // Simple addon with Direct Open support
              if (args.hasOpenOnDrop) {
                // Auto-insert default text on drop
                resolve({
                  type: 'paragraph',
                  value: { 
                    html: '<p>Quick text inserted automatically!</p>' 
                  }
                });
              } else {
                // Show editor for manual customization
                yourTextEditor.open({
                  onSave: (text) => resolve({ 
                    type: 'paragraph', 
                    value: { html: `<p>${text}</p>` } 
                  }),
                  onCancel: () => reject()
                });
              }
              break;
              
            case 'image-library-addon':
              // Complex addon with image selection
              yourImagePicker.open({
                onSelect: (img) => resolve({
                  type: 'image',
                  value: { src: img.url, alt: img.description }
                }),
                onCancel: () => reject()
              });
              break;
              
            case 'content-block-addon':
              // Mixed content addon
              yourContentBlockBuilder.open({
                onSave: (config) => resolve({
                  type: 'mixed',
                  value: [
                    { 
                      type: 'image', 
                      value: { src: config.imageUrl, alt: config.imageAlt } 
                    },
                    { 
                      type: 'title',  // Note: 'title' not 'heading' in mixed content
                      value: { 
                        text: config.headingText,
                        align: 'center',
                        size: 28
                      } 
                    },
                    { 
                      type: 'paragraph', 
                      value: { html: config.text } 
                    },
                    { 
                      type: 'button', 
                      value: { 
                        label: config.buttonText, 
                        href: config.buttonUrl,
                        'background-color': '#0066CC',
                        'border-radius': 4,
                        'padding-top': 12,
                        'padding-right': 24,
                        'padding-bottom': 12,
                        'padding-left': 24
                      } 
                    }
                  ]
                }),
                onCancel: () => reject()
              });
              break;
              
            default:
              console.error('Unknown addon ID:', args.contentDialogId);
              reject(new Error('Unknown addon'));
          }
        } catch (error) {
          console.error('AddOn error:', error);
          reject(error);
        }
      }
    }
  }
};

// Initialize Beefree SDK with configuration
const bee = new BeePlugin(token, beeConfig);
bee.start(template);
```

## Error Handling

Proper error handling is essential for production addons—it prevents silent failures, provides useful debugging information, and gives users clear feedback when something goes wrong. Always wrap async operations in try-catch blocks, validate that your content objects have the required properties before resolving, and provide meaningful error messages. Calling `reject()` with an error ensures Beefree knows the operation failed and can respond appropriately.

Always handle errors properly:

```javascript
handler: async (resolve, reject, args) => {
  try {
    // Perform async operation (API call, data fetch, etc.)
    const result = await yourAsyncOperation();
    
    // Validate the result before resolving
    if (!result || !result.type || !result.value) {
      throw new Error('Invalid content object - missing required properties');
    }
    
    // Everything is valid - insert the content
    resolve(result);
    
  } catch (error) {
    // Log error for debugging
    console.error('AddOn error:', error);
    
    // Show user-friendly error message
    alert(`Failed to insert content: ${error.message}`);
    
    // Reject to notify Beefree of the failure
    reject(error);
  }
}
```

## Using Custom Metadata

Custom metadata allows you to store additional information with your content that persists when users save and reopen their emails. This is incredibly powerful for creating stateful addons that remember their configuration, track content sources, or maintain relationships with external systems. When a user edits content that was inserted by your addon, Beefree provides the original metadata in `args.metadata`, allowing you to reconstruct the addon's state and pre-fill your UI with the previous configuration.

Store custom data with your content:

```javascript
resolve({
  type: 'html',
  value: {
    html: '<div>Generated content block</div>',
    customFields: {
      sourceId: '12345',
      contentType: 'auto-generated',
      createdAt: new Date().toISOString(),
      version: '1.0'
    }
  }
});
```

## Troubleshooting

| Issue                  | Solution                                                                                      |
| ---------------------- | --------------------------------------------------------------------------------------------- |
| AddOn not appearing    | Verify plan level supports custom addons, check that handle matches Developer Console exactly |
| Dialog not opening     | Check browser console for errors, verify handler function is defined in beeConfig             |
| Content not inserting  | Validate content object schema matches addon type, check for missing required properties      |
| Multiple clicks needed | Ensure resolve() or reject() is always called exactly once in all code paths                  |
| Button not displaying  | Verify padding and border-radius values are **numbers**, not strings                          |
