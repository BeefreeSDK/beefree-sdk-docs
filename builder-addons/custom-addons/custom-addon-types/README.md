# Custom AddOn Types

### What Are Custom AddOn Types?

Custom AddOn Types define what kind of content your AddOn will insert into the Beefree email builder when users interact with it. Each type corresponds to a specific content module in the Beefree editor, such as images, buttons, paragraphs, or HTML blocks.

Think of AddOn Types as the "shape" of the content your AddOn produces. When you create a Custom AddOn in the Beefree SDK Developer Console, you must select a type that determines:

* **What content structure** is inserted on the stage
* **Which sidebar properties** appear when the module is selected
* **What schema** your AddOn must use when resolving content
* **How users can edit** the inserted content

#### How AddOn Types Work

**1. Type Selection in Console**

When creating a Custom AddOn in the [Beefree SDK Developer Console](https://developers.beefree.io/), you select a **Type** from a dropdown menu. This type is permanently associated with your AddOn.

```
Create Custom AddOn Form:
├── Name: "My Custom AddOn"
├── Type: [Image ▼]  ← You select the type here
│         - Image
│         - HTML
│         - Mixed
│         - Row
│         - Paragraph
│         - Button
│         - Title
│         - List
│         - Menu
│         - Icon
├── Handle: "my-custom-addon"
└── ...
```

{% hint style="info" %}
**Note:** The Console displays "Title" in the dropdown, but your code must use `type: 'heading'` when resolving content.
{% endhint %}

**2. Content Object Schema**

Each type requires a specific **content object structure** that your AddOn must return. This object is passed to the `resolve()` function in your handler.

**Example: Image Type**

```javascript
resolve({
  type: 'image',  // Must match your AddOn type
  value: {
    src: 'https://example.com/image.jpg',  // Type-specific properties
    alt: 'Description'
  }
});
```

**Example: Button Type**

```javascript
resolve({
  type: 'button',  // Must match your AddOn type
  value: {
    label: 'Click Me',  // Type-specific properties
    href: 'https://example.com',
    'background-color': '#7747FF',
    color: '#FFFFFF',
    'border-radius': 4,
    'padding-top': 12,
    'padding-right': 24,
    'padding-bottom': 12,
    'padding-left': 24
  }
});
```

**3. Editor Integration**

When a user drops your AddOn tile onto the stage:

1. **Content Dialog Opens** (if using Content Dialog method) or **Iframe Loads** (if using Iframe method)
2. **User Interacts** with your custom UI to create/select content
3. **Your Handler Resolves** with a properly formatted content object
4. **Module Is Inserted** on the editor stage
5. **Sidebar Updates** to show properties specific to that type

```
User Action          Your Code                    Editor Result
───────────────────────────────────────────────────────────────
Drop AddOn tile  →   handler() called        →   Dialog opens
                                             
User clicks save →   resolve({               →   Module appears
                       type: 'image',             on stage
                       value: {...}               
                     })                      →   Sidebar shows
                                                 image properties
```

**4. Sidebar Properties**

Each type displays different properties in the editor's sidebar when the module is selected:

| Type              | Sidebar Shows                                           |
| ----------------- | ------------------------------------------------------- |
| **Image**         | Image source, alt text, link, dimensions, alignment     |
| **HTML**          | HTML content (read-only via AddOn), padding, background |
| **Button**        | Button text, link, colors, borders, padding, alignment  |
| **Paragraph**     | Text editor, font, colors, alignment, spacing           |
| **Title/Heading** | Heading level, text, font, size, alignment              |
| **List**          | List type, items, font, colors, alignment               |
| **Menu**          | Menu items, links, layout, spacing                      |
| **Icon**          | Icon images, links, sizes, alignment                    |
| **Mixed**         | Varies based on included modules                        |
| **Row**           | Column structure, background, padding, alignment        |

#### Available Custom AddOn Types

Beefree SDK currently supports **10 Custom AddOn Types**. Each type serves different use cases and content needs.

**Content Module Types**

These types insert individual content modules:

**Image AddOn**

Inserts an image module with a source URL, alt text, and optional link.

**Resolve Structure:**

```javascript
{
  type: 'image',
  value: {
    src: string,
    alt: string,
    href: string,      // Optional
    target: string     // Optional: '_blank', '_self'
  }
}
```

***

**HTML AddOn**

Inserts custom HTML markup. Content is only editable by reopening the AddOn.

**Resolve Structure:**

```javascript
{
  type: 'html',
  value: {
    html: string
  }
}
```

***

**Paragraph AddOn**

Inserts text paragraphs with formatting and support for merge tags.

**Resolve Structure:**

```javascript
{
  type: 'paragraph',
  value: {
    html: string,
    color: string,      // Optional
    bold: boolean,      // Optional
    italic: boolean,    // Optional
    underline: boolean  // Optional
  },
  mergeTags: [...]      // Optional
}
```

***

**Button AddOn**

Inserts pre-styled call-to-action buttons.

**Resolve Structure:**

```javascript
{
  type: 'button',
  value: {
    label: string,
    href: string,
    'background-color': string,
    color: string,
    'border-radius': number,    // Pixels (e.g., 4)
    'padding-top': number,      // Optional, pixels
    'padding-right': number,    // Optional, pixels
    'padding-bottom': number,   // Optional, pixels
    'padding-left': number      // Optional, pixels
  }
}
```

***

**Title/Heading AddOn**

Inserts heading elements (H1-H3) with custom styling.

**Resolve Structure:**

```javascript
{
  type: 'heading',
  value: {
    title: string,      // 'h1', 'h2', or 'h3'
    text: string,       // The heading content
    align: string,      // 'left', 'center', 'right', 'justify'
    size: number,       // Font size in pixels
    color: string,      // Hex color
    bold: boolean,      // Optional
    italic: boolean,    // Optional
    underline: boolean, // Optional
    linkColor: string,  // Optional, hex color
    'letter-spacing': number,  // Optional, -99 to 99
    'line-height': number,     // Optional, 0.5 to 3
    direction: string   // Optional, 'ltr' or 'rtl'
  }
}
```

{% hint style="warning" %}
**Important:** Use `type: 'heading'` in your code, not `type: 'title'`. The Console may display "Title" but the content object type must be `'heading'`.
{% endhint %}

***

**List AddOn**

Inserts ordered or unordered lists with formatting.

**Resolve Structure:**

```javascript
{
  type: 'list',
  value: {
    tag: string,     // 'ul' or 'ol'
    html: string,    // The list HTML
    color: string,   // Optional, hex color
    align: string,   // Optional, 'left', 'center', 'right'
    size: number     // Optional, font size in pixels
  }
}
```

***

**Menu AddOn**

Inserts navigation menus with multiple linked items.

**Resolve Structure:**

```javascript
{
  type: 'menu',
  value: {
    items: [
      {
        text: string,
        link: {
          href: string,
          target: string,  // '_blank', '_self'
          title: string    // Optional
        }
      }
    ]
  }
}
```

***

**Icon AddOn**

Inserts icon sets with images, labels, and links.

**Resolve Structure:**

```javascript
{
  type: 'icons',
  value: {
    icons: [
      {
        image: string,        // Icon image URL
        text: string,         // Icon label
        href: string,         // Link URL
        target: string,       // '_blank', '_self'
        alt: string,          // Alt text
        width: string,        // e.g., '32px'
        height: string,       // e.g., '32px'
        textPosition: string  // 'top', 'bottom', 'left', 'right'
      }
    ]
  }
}
```

***

**Advanced Structure Types**

These types insert more complex structures:

**Mixed Content AddOn**

Inserts multiple content modules at once in a single drop action.

**Resolve Structure:**

```javascript
{
  type: 'mixed',
  value: [
    { type: 'image', value: {...} },
    { type: 'heading', value: {...} },
    { type: 'paragraph', value: {...} },
    { type: 'button', value: {...} }
  ]
}
```

***

**Row AddOn**

Inserts a pre-built row structure with columns and multiple modules.

**Resolve Structure:**

```javascript
{
  type: 'rowAddon',
  value: {
    name: string,
    columns: [
      {
        weight: number,  // Column width (1-12)
        modules: [
          { type: 'image', value: {...} },
          { type: 'heading', value: {...} }
        ]
      }
    ],
    metadata: {}  // Optional
  }
}
```

***

#### Validation and Errors

Each type has a specific schema that must be followed. If your `resolve()` function returns an invalid content object:

* The module will **not be inserted** on the stage
* An error will be logged to the browser console
* The `onError` callback in `beeConfig` will be triggered

**Always validate your content objects match the expected schema for your type.**

#### Type-Specific Documentation

For detailed information about each type, including:

* Complete schema definitions
* Working code examples
* Implementation guides for both Content Dialog and Iframe methods
* Advanced use cases
* Best practices

Refer to the individual type pages:

* [Image AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/image-addon)
* [HTML AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/html-addon)
* [Mixed Content AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/mixed-content-addon)
* [Row AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/row-addon)
* [Paragraph AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/paragraph-addon)
* [Button AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/data-structures/simple-schema/button-schema)
* [Title AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/data-structures/simple-schema/title-schema)
* [List AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/list-addon)
* [Menu AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/menu-addon)
* [Icon AddOn](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/icon-addon)

#### Schema Resources

All Custom AddOn Types follow schemas defined in the Beefree SDK Simple Schema:

* **GitHub Repository:** [BeefreeSDK/beefree-sdk-simple-schema](https://github.com/BeefreeSDK/beefree-sdk-simple-schema)
* **Official Documentation:** [Beefree SDK Data Structures](https://docs.beefree.io/beefree-sdk/data-structures/simple-schema)

Each type has a corresponding JSON schema file in the repository that defines all valid properties and requirements.

#### Quick Start Example

Here's a minimal example showing how types work:

```javascript
// In Beefree SDK Console:
// - Name: "Quick Image AddOn"
// - Type: Image  ← Select this
// - Handle: "quick-image"

// In your code:
const beeConfig = {
  contentDialog: {
    addOn: {
      handle: 'quick-image',  // Must match Console
      handler: (resolve, reject, args) => {
        // Your AddOn must return type: 'image'
        resolve({
          type: 'image',  // Must match Console type
          value: {
            src: 'https://example.com/image.jpg',
            alt: 'Example Image'
          }
        });
      }
    }
  }
};
```
