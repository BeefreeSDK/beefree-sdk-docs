# Row AddOn

### Overview

The Row AddOn type allows you to insert pre-built row structures with columns and multiple content modules. Unlike Mixed Content AddOns that insert modules sequentially, Row AddOns create structured layouts with side-by-side columns—perfect for multi-column designs like product grids, feature comparisons, or content layouts that require horizontal organization.

#### What Makes Row AddOns Unique

Row AddOns provide layout structure in addition to content:

* Define the number of columns using a 12-column grid system
* Control column widths using weight values (1-12)
* Include multiple modules within each column
* Create complex, multi-column layouts in one drop

This is ideal when you need consistent, reusable layout patterns that go beyond simple vertical stacking.

#### Prerequisites

Before implementing a Row AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/):

1. Log into the Developer Console and navigate to your application
2. Create a new Custom AddOn and select "Row" as the type
3. Configure the addon with a unique **handle** (e.g., `my-row-addon`)
4. Choose your implementation method (Content Dialog or External iframe)
5. Save the addon configuration

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match exactly with the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

#### Content Object Schema

**Required Structure**

The Row AddOn schema uses `type: 'rowAddon'` with a value containing a `name` identifier and a `columns` array. Each column has a `weight` (1-12, defining its width in the 12-column grid) and a `modules` array containing the content for that column. The optional `metadata` object lets you store custom information about the row. This structure creates complete layout systems in a single insertion.

{% hint style="warning" %}
**Important:** Within Row AddOns, titles use `type: 'title'` (not `type: 'heading'`). This is similar to Mixed Content AddOns.
{% endhint %}

```javascript
{
  type: 'rowAddon',
  value: {
    name: string,           // Required: Row identifier
    columns: [              // Required: Array of column objects
      {
        weight: number,     // Required: Column width (1-12)
        modules: [          // Required: Array of modules in this column
          { type: 'image', ... },
          { type: 'paragraph', ... }
        ]
      }
    ],
    metadata: {}            // Optional: Custom data
  }
}
```

**Understanding Column Weights**

Columns use a **12-column grid system** where weights must add up to 12 for proper layout:

* **Single column (full width)**: `weight: 12`
* **Two equal columns (50/50)**: `weight: 6` each
* **Three equal columns (33/33/33)**: `weight: 4` each
* **Two-thirds + one-third (67/33)**: `weight: 8` and `weight: 4`

This flexible system allows you to create any column configuration that matches your design needs.

**Simple Two-Column Example**

This basic example demonstrates a two-column layout with equal width columns (50/50 split). Each column contains a simple content structure with an image and text. This pattern is perfect for side-by-side content presentation like before/after comparisons, feature highlights, or product showcases where visual balance matters.

```javascript
resolve({
  type: 'rowAddon',
  value: {
    name: 'Two Column Layout',
    columns: [
      {
        weight: 6,  // 50% width
        modules: [
          {
            type: 'image',
            value: {
              src: 'https://example.com/image-left.jpg',
              alt: 'Left image'
            }
          },
          {
            type: 'paragraph',
            value: {
              html: '<p>Content for left column</p>'
            }
          }
        ]
      },
      {
        weight: 6,  // 50% width
        modules: [
          {
            type: 'image',
            value: {
              src: 'https://example.com/image-right.jpg',
              alt: 'Right image'
            }
          },
          {
            type: 'paragraph',
            value: {
              html: '<p>Content for right column</p>'
            }
          }
        ]
      }
    ]
  }
});
```

**Three-Column Example**

This example shows a three-column layout with equal widths (33/33/33 split), ideal for displaying multiple items in a grid format like product features, team members, or service offerings. Each column contains an image and title, creating a balanced, professional layout that presents information in an organized, scannable format perfect for email marketing.

```javascript
resolve({
  type: 'rowAddon',
  value: {
    name: 'Three Column Grid',
    columns: [
      {
        weight: 4,  // 33% width
        modules: [
          {
            type: 'image',
            value: {
              src: 'https://example.com/feature-1.jpg',
              alt: 'Feature 1'
            }
          },
          {
            type: 'title',  // Note: 'title' not 'heading' in rows
            value: {
              text: 'Feature One',
              size: 20
            }
          }
        ]
      },
      {
        weight: 4,  // 33% width
        modules: [
          {
            type: 'image',
            value: {
              src: 'https://example.com/feature-2.jpg',
              alt: 'Feature 2'
            }
          },
          {
            type: 'title',  // Note: 'title' not 'heading' in rows
            value: {
              text: 'Feature Two',
              size: 20
            }
          }
        ]
      },
      {
        weight: 4,  // 33% width
        modules: [
          {
            type: 'image',
            value: {
              src: 'https://example.com/feature-3.jpg',
              alt: 'Feature 3'
            }
          },
          {
            type: 'title',  // Note: 'title' not 'heading' in rows
            value: {
              text: 'Feature Three',
              size: 20
            }
          }
        ]
      }
    ]
  }
});
```

#### Content Dialog Implementation

**Basic Handler**

The Content Dialog method enables programmatic row insertion through a JavaScript handler. When users drag your row addon onto the stage, this handler is immediately invoked and resolves with a complete row structure including columns and their content. This pattern works perfectly for predefined layouts that don't require user configuration, providing instant insertion of complex, multi-column structures with consistent formatting.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-row-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for row insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-row-addon') {
          // Check if triggered by dropping the addon (vs editing existing)
          if (args.hasOpenOnDrop) {
            // Immediately insert a two-column row
            resolve({
              type: 'rowAddon',
              value: {
                name: 'Simple Row',
                columns: [
                  {
                    weight: 6,
                    modules: [
                      {
                        type: 'image',
                        value: {
                          src: 'https://example.com/left.jpg',
                          alt: 'Left content'
                        }
                      }
                    ]
                  },
                  {
                    weight: 6,
                    modules: [
                      {
                        type: 'image',
                        value: {
                          src: 'https://example.com/right.jpg',
                          alt: 'Right content'
                        }
                      }
                    ]
                  }
                ]
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

**Pattern: Dynamic Column Generation**

This pattern demonstrates programmatically building row structures from data arrays, making it easy to create layouts from dynamic sources like product catalogs, API responses, or database queries. By calculating column weights and mapping through your data, you can generate properly structured rows with any number of columns while maintaining consistent module structure. This is particularly powerful for content that changes frequently or needs to scale based on available items.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Example data (could come from API, database, etc.)
      const items = [
        { name: 'Product A', image: 'https://example.com/product-a.jpg' },
        { name: 'Product B', image: 'https://example.com/product-b.jpg' },
        { name: 'Product C', image: 'https://example.com/product-c.jpg' }
      ];
      
      // Calculate column weight (12 ÷ number of items)
      const columnWeight = Math.floor(12 / items.length);
      
      // Build columns from data
      const columns = items.map(item => ({
        weight: columnWeight,
        modules: [
          {
            type: 'image',
            value: {
              src: item.image,
              alt: item.name
            }
          },
          {
            type: 'title',  // Note: 'title' not 'heading' in rows
            value: {
              text: item.name,
              size: 20
            }
          }
        ]
      }));
      
      // Resolve with generated row
      resolve({
        type: 'rowAddon',
        value: {
          name: 'Product Grid',
          columns,
          metadata: {
            productCount: items.length,
            generated: new Date().toISOString()
          }
        }
      });
    }
  }
}
```

**Pattern: User-Configured Rows**

This advanced pattern shows how to let users configure row layout and content before insertion. By opening a custom interface, users can select the number of columns, choose content for each column, and configure the layout structure. The handler waits for user confirmation, then builds the row based on their selections. This provides maximum flexibility while automating the complex task of creating properly structured multi-column layouts.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for row configuration
      // Replace 'yourLayoutSelector' with your actual UI component
      yourLayoutSelector.open({
        onSelect: (layoutConfig) => {
          // layoutConfig contains user selections
          const { columnCount, items } = layoutConfig;
          const columnWeight = Math.floor(12 / columnCount);
          
          // Build columns from user selections
          const columns = items.map(item => ({
            weight: columnWeight,
            modules: [
              {
                type: 'image',
                value: {
                  src: item.imageUrl,
                  alt: item.name
                }
              },
              {
                type: 'paragraph',
                value: {
                  html: `<p>${item.description}</p>`
                }
              }
            ]
          }));
          
          // Resolve with user-configured row
          resolve({
            type: 'rowAddon',
            value: {
              name: 'Custom Row',
              columns,
              metadata: {
                userConfigured: true,
                columnCount
              }
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

The Iframe method provides complete UI flexibility by loading your custom web application inside the Beefree editor. Your iframe communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal for visual layout builders, template galleries, or sophisticated interfaces where you need full control over how users design and configure multi-column row structures before inserting them into the email.

**Required postMessage Communication**

Your iframe must implement the standard postMessage protocol to integrate with Beefree. First, notify Beefree when your iframe is loaded and specify dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes configuring their row layout, send "onSave" with your complete row object. If the user cancels, send "onCancel" to close without inserting. This bidirectional communication enables seamless integration between your custom layout builder and the Beefree editor.

**1. Send "loaded" when your iframe is ready:**

```javascript
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '900px',
    height: '700px',
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
    // Initialize your row builder UI
  }
});
```

**3. Send "onSave" with row structure:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'rowAddon',
    value: {
      name: 'My Row',
      columns: [
        {
          weight: 6,
          modules: [
            {
              type: 'image',
              value: {
                src: 'https://example.com/image.jpg',
                alt: 'Image'
              }
            }
          ]
        },
        {
          weight: 6,
          modules: [
            {
              type: 'paragraph',
              value: {
                html: '<p>Text content</p>'
              }
            }
          ]
        }
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

**Simple Iframe Example**

This complete HTML example demonstrates a functional row layout builder interface. It includes the full postMessage protocol implementation and provides options for column count selection with simple content inputs for each column. Users can choose between 1-4 columns and provide image URLs for each. The interface automatically calculates column weights and builds the proper row structure. You can expand this basic example with drag-and-drop layout builders, visual column previews, advanced module configuration, or layout template galleries.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Row Layout Builder</title>
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
    select, input {
      padding: 8px;
      margin: 5px 0;
      width: 100%;
    }
    button {
      padding: 10px 20px;
      margin-right: 10px;
    }
    .columns-config {
      margin: 20px 0;
      padding: 15px;
      background-color: #f5f5f5;
      border-radius: 4px;
    }
    .column-input {
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <h2>Create Row Layout</h2>
  
  <div class="field">
    <label>Number of Columns:</label>
    <select id="columnCount" onchange="updateColumnInputs()">
      <option value="1">1 Column</option>
      <option value="2" selected>2 Columns</option>
      <option value="3">3 Columns</option>
      <option value="4">4 Columns</option>
    </select>
  </div>
  
  <div class="columns-config" id="columnsConfig">
    <!-- Column inputs will be generated here -->
  </div>
  
  <button onclick="insertRow()">Insert Row</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Notify Beefree that iframe is loaded and ready
    window.parent.postMessage({
      action: 'loaded',
      data: { 
        width: '900px', 
        height: '700px',
        isRounded: true,
        hasTitleBar: true,
        showTitle: true
      }
    }, '*');

    // Initialize with 2 columns
    updateColumnInputs();

    function updateColumnInputs() {
      const count = parseInt(document.getElementById('columnCount').value);
      const container = document.getElementById('columnsConfig');
      container.innerHTML = '';
      
      for (let i = 1; i <= count; i++) {
        container.innerHTML += `
          <div class="column-input">
            <label>Column ${i} Image URL:</label>
            <input type="url" id="col${i}Image" placeholder="https://example.com/image-${i}.jpg" value="https://example.com/image-${i}.jpg">
            <label>Column ${i} Text:</label>
            <input type="text" id="col${i}Text" placeholder="Column ${i} content" value="Column ${i} content">
          </div>
        `;
      }
    }

    function insertRow() {
      const columnCount = parseInt(document.getElementById('columnCount').value);
      const columnWeight = Math.floor(12 / columnCount);
      const columns = [];
      
      // Build columns from inputs
      for (let i = 1; i <= columnCount; i++) {
        const imageUrl = document.getElementById(`col${i}Image`).value;
        const text = document.getElementById(`col${i}Text`).value;
        
        columns.push({
          weight: columnWeight,
          modules: [
            {
              type: 'image',
              value: {
                src: imageUrl,
                alt: `Column ${i} image`
              }
            },
            {
              type: 'title',  // Note: 'title' not 'heading' in rows
              value: {
                text: text,
                size: 20,
                align: 'center'
              }
            }
          ]
        });
      }
      
      // Send row data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'rowAddon',
          value: {
            name: `${columnCount} Column Row`,
            columns,
            metadata: {
              columnCount,
              created: new Date().toISOString()
            }
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

#### Available Module Types

You can use any of these module types within row columns:

* **title** - Titles/headings (use `type: 'title'` in rows, not `'heading'`)
* **paragraph** - Text content
* **image** - Images
* **button** - Call-to-action buttons
* **list** - Ordered or unordered lists
* **icons** - Icon sets
* **menu** - Navigation menus
* **html** - Custom HTML

**Note:** You cannot nest Row AddOns or Mixed Content AddOns inside a Row AddOn.

#### Column Weight Examples

**Common Layouts**

```javascript
// Full width (1 column)
columns: [{ weight: 12, modules: [...] }]

// 50/50 (2 columns)
columns: [
  { weight: 6, modules: [...] },
  { weight: 6, modules: [...] }
]

// 33/33/33 (3 columns)
columns: [
  { weight: 4, modules: [...] },
  { weight: 4, modules: [...] },
  { weight: 4, modules: [...] }
]

// 67/33 (2 columns, unequal)
columns: [
  { weight: 8, modules: [...] },
  { weight: 4, modules: [...] }
]
```

#### Using Metadata

Store custom information with your row for tracking or later reference:

```javascript
resolve({
  type: 'rowAddon',
  value: {
    name: 'Product Row',
    columns: [...],
    metadata: {
      source: 'product-catalog',
      category: 'featured',
      productIds: [123, 456, 789],
      createdAt: new Date().toISOString()
    }
  }
});
```
