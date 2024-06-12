# Generating Custom Rows from existing content

Custom Rows allows you to easily generate draggable rows from your application content, or other application content, without any design process or complex user interaction.

To make it possible, we built a **Simplified Row Schema**, a JSON that describes each row and its contents with the minimum number of elements, to easily transform existing content into a destination format compliant by the Beefree SDK system.

While the [Saved Rows](../saved-rows/) feature provides the complex and continuously evolving object used in the message page, the **Simplified Row Schema** makes it easy to build an API that feeds the editor with contents from different origins like e-commerce stores, blogs, or digital asset management systems.

## Simplified Row Schema <a href="#simplified-row-schema" id="simplified-row-schema"></a>

### **General row schema**

The following is an example of four different row objects:

* **First:** A row with a single column and 2 text modules (a title and a paragraph) inside.
* **Second:** A row with 2 equal columns and 2 text modules (a title and a paragraph) inside each one. These columns will not stack when the message is open on mobile devices.
* **Third:** A row with a background image on it.
* **Four:** A row with a display condition.

```json

[{
    "name": "First item", // Identifies the row
    "columns": [{ // The columns inside the row
        "weight": 12, // This weight identifies a single column row
        "modules": [{ // This describes the content modules inside the column
            "type": "title", // Every module is identified by a type parameter
            "text": "How am I supposed to fight?"
        },
        {
            "type": "paragraph",
            "text": "Look, I can take you as far as Anchorhead. You can get a transport there to Mos Eisley or wherever you're going."
        }]
    }]
},
{
    "name": "Second item",
    "colStackOnMobile": false,
    "columns": [{
        "weight": 6,
        "modules": [{
            "type": "title",
            "text": "You're going to do his laundry?"
        },
        {
            "type": "paragraph",
            "text": "Oh Leela! You're the only person I could turn to; you're the only person who ever loved me."
        }]
    },
    {
        "weight": 6,
        "modules": [{
            "type": "title",
            "text": "Well how'd you become king then?"
        },
        {
            "type": "paragraph",
            "text": "The Lady of the Lake, her arm clad in the purest shimmering samite held aloft Excalibur from the bosom of the water, signifying by divine providence that I, Arthur, was to carry Excalibur. THAT is why I am your king."
        },
        {
            "type": "paragraph",
            "text": "Listen, strange women lyin\' in ponds distributin\' swords is no basis for a system of government. Supreme executive power derives from a mandate from the masses, not from some farcical aquatic ceremony."
        }]
    }]
},
{
    "background-image": "https://yourdomain/yourpath/background.png",
    "background-repeat": "repeat",
    "background-position": "top center",
    "background-color": "#fff",
    "name": "Text on background pattern",
    "columns": [{
        "weight": 12,
        "modules": [{
            "type": "paragraph",
            "text": "Behind the word mountains, far from the countries Vokalia and Consonantia."
          }]
      }]
 },
{
    "name": "Developer joke",
    "display-condition": {
        "type": "Jokes",
        "label": "developers",
        "description": "Only developers will see this content",
        "before": "{% raw %}
{% if recipient.role == \'Developer\' %}",
        "after": "{% endif %}
{% endraw %}"
    },
    "columns": [{
        "weight": 12,
        "modules": [{
            "type": "paragraph",
            "text": "Chuck Norris writes code that optimizes itself"
          }]
      }]
 }]

```

## Simplified Row JSON Schema <a href="#general-row-parameters" id="general-row-parameters"></a>

The updated Beefree SDK simplified row schema provides more flexibility for creating Custom Addons and Rows, enhancing control over permissions to ensure critical content remains unchanged by end users. Synchronization of data between the row's content and metadata and your application allows dynamic responses to user changes, eliminating the need to restart when reopening [content dialogs](../advanced-options/content-dialog.md). Visit the [Row Simplified Schema section](../addons/custom-addons/addon-development.md#row-simplified-schema) of the [AddOn Development page](../addons/custom-addons/addon-development.md) to learn more about the benefits of this feature and how to use them.&#x20;

The following code sample provides an example of this simplified row schema.

{% code overflow="wrap" %}
```javascript
{
  $schema: 'http://json-schema.org/draft-07/schema',
  $id: 'BEE-simplified-row',
  type: 'object',
  required: [
    'name',
    'columns',
  ],
  definitions: {
    padding: {
      type: 'integer',
      minimum: 0,
      maximum: 60,
    },
  },
  properties: {
    name: {
      type: 'string',
    },
    colStackOnMobile: {
      type: 'boolean',
    },
    rowReverseColStackOnMobile: {
      type: 'boolean',
    },
    contentAreaBackgroundColor: {
      type: 'string',
    },
    'background-color': {
      type: 'string',
    },
    'background-image': {
      type: 'string',
    },
    'background-position': {
      type: 'string',
    },
    'background-repeat': {
      type: 'string',
    },
    customFields: {
      type: 'object',
    },
    'display-condition': {
      type: 'object',
      properties: {
        type: {
          type: 'string',
        },
        label: {
          type: 'string',
        },
        description: {
          type: 'string',
        },
        before: {
          type: 'string',
        },
        after: {
          type: 'string',
        },
      },
    },
    metadata: {
      type: 'object',
    },
    columns: {
      type: 'array',
      minItems: 1,
      items: {
        type: 'object',
        required: [
          'weight',
          'modules',
        ],
        additionalProperties: false,
        properties: {
          weight: {
            type: 'integer',
            minimum: 1,
            maximum: 12,
          },
          'background-color': {
            type: 'string',
          },
          'padding-top': {
            $ref: '#/definitions/padding',
          },
          'padding-right': {
            $ref: '#/definitions/padding',
          },
          'padding-bottom': {
            $ref: '#/definitions/padding',
          },
          'padding-left': {
            $ref: '#/definitions/padding',
          },
          modules: {
            type: 'array',
            items: {
              type: 'object',
              discriminator: {
                propertyName: 'type',
              },
              required: [
                'type',
              ],
              properties: {
                type: {
                  enum: [
                    'button',
                    'divider',
                    'heading',
                    'html',
                    'icons',
                    'image',
                    'list',
                    'menu',
                    'paragraph',
                    'title',
                  ],
                },
              },
              oneOf: [
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-button',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'button',
                    },
                    label: {
                      type: 'string',
                      format: 'noAnchorTags',
                    },
                    text: {
                      type: 'string',
                      format: 'noAnchorTags',
                    },
                    href: {
                      type: 'string',
                      format: 'urlOrMergeTags',
                    },
                    target: {
                      enum: [
                        '_blank',
                        '_self',
                        '_top',
                      ],
                    },
                    color: {
                      type: 'string',
                    },
                    'background-color': {
                      type: 'string',
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-divider',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'divider',
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-icons',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'icons',
                    },
                    icons: {
                      type: 'array',
                      items: {
                        type: 'object',
                        additionalProperties: false,
                        required: [
                          'image',
                          'textPosition',
                          'width',
                          'height',
                        ],
                        properties: {
                          alt: {
                            type: 'string',
                          },
                          text: {
                            type: 'string',
                          },
                          title: {
                            type: 'string',
                          },
                          image: {
                            type: 'string',
                            format: 'urlOrMergeTags',
                          },
                          href: {
                            type: 'string',
                            format: 'urlOrMergeTags',
                          },
                          height: {
                            type: 'string',
                          },
                          width: {
                            type: 'string',
                          },
                          target: {
                            enum: [
                              '_blank',
                              '_self',
                              '_top',
                            ],
                          },
                          textPosition: {
                            enum: [
                              'left',
                              'right',
                              'top',
                              'bottom',
                            ],
                          },
                        },
                      },
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-image',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'image',
                    },
                    alt: {
                      type: 'string',
                    },
                    href: {
                      type: 'string',
                      format: 'urlOrMergeTags',
                    },
                    src: {
                      type: 'string',
                      format: 'urlOrMergeTags',
                    },
                    dynamicSrc: {
                      type: 'string',
                    },
                    target: {
                      enum: [
                        '_blank',
                        '_self',
                        '_top',
                      ],
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-html',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'html',
                    },
                    html: {
                      type: 'string',
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-list',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'list',
                    },
                    underline: {
                      type: 'boolean',
                    },
                    italic: {
                      type: 'boolean',
                    },
                    bold: {
                      type: 'boolean',
                    },
                    html: {
                      type: 'string',
                    },
                    text: {
                      type: 'string',
                    },
                    align: {
                      enum: [
                        'left',
                        'center',
                        'right',
                      ],
                    },
                    tag: {
                      enum: [
                        'ol',
                        'ul',
                      ],
                    },
                    size: {
                      type: 'integer',
                    },
                    color: {
                      type: 'string',
                    },
                    linkColor: {
                      type: 'string',
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-menu',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'menu',
                    },
                    items: {
                      type: 'array',
                      items: {
                        type: 'object',
                        additionalProperties: false,
                        properties: {
                          type: {
                            const: 'menu-item',
                          },
                          text: {
                            type: 'string',
                          },
                          link: {
                            type: 'object',
                            additionalProperties: false,
                            properties: {
                              title: {
                                type: 'string',
                              },
                              href: {
                                type: 'string',
                                format: 'urlOrMergeTags',
                              },
                              target: {
                                type: 'string',
                                enum: [
                                  '_blank',
                                  '_self',
                                  '_top',
                                ],
                              },
                            },
                          },
                        },
                      },
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-paragraph',
                  type: 'object',
                  properties: {
                    type: {
                      const: 'paragraph',
                    },
                    underline: {
                      type: 'boolean',
                    },
                    italic: {
                      type: 'boolean',
                    },
                    bold: {
                      type: 'boolean',
                    },
                    html: {
                      type: 'string',
                    },
                    text: {
                      type: 'string',
                    },
                    align: {
                      enum: [
                        'left',
                        'center',
                        'right',
                      ],
                    },
                    size: {
                      type: 'integer',
                    },
                    color: {
                      type: 'string',
                    },
                    linkColor: {
                      type: 'string',
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
                {
                  $schema: 'http://json-schema.org/draft-07/schema',
                  $id: 'BEE-simplified-title',
                  type: 'object',
                  properties: {
                    type: {
                      enum: ['title', 'heading'],
                    },
                    underline: {
                      type: 'boolean',
                    },
                    italic: {
                      type: 'boolean',
                    },
                    bold: {
                      type: 'boolean',
                    },
                    html: {
                      type: 'string',
                    },
                    text: {
                      type: 'string',
                    },
                    align: {
                      enum: [
                        'left',
                        'center',
                        'right',
                      ],
                    },
                    title: {
                      enum: [
                        'h1',
                        'h2',
                        'h3',
                      ],
                    },
                    size: {
                      type: 'integer',
                    },
                    color: {
                      type: 'string',
                    },
                    linkColor: {
                      type: 'string',
                    },
                    customFields: {
                      type: 'object',
                    },
                  },
                },
              ],
            },
          },
          customFields: {
            type: 'object',
          },
        },
      },
    },
  },
}
```
{% endcode %}

## General row parameters <a href="#general-row-parameters" id="general-row-parameters"></a>

### **name**

The row’s name:

* A string of plain text that identifies the row.
* Displayed in the row card when the row is shown in the _Rows_ panel.
* Included in the textual content used in searches

### **background image**

Set a row background image.

Properties:

* background-image: valid image url
* background-repeat: repeat | no-repeat
* background-position: top | bottom + left | center | right
* background-color: #c2c2c2 // CSS value

### **display conditions**

Set a row display condition.\
Check the [display conditions documentation](../advanced-options/display-conditions.md) for further details.

Properties:

* display-condition
  * type
  * label
  * description
  * before
  * after

### **mobile**

Disable stacking on mobile.  Set the value to “false” to disable stacking on mobile.  If the value is “true”, or not provided, the columns will stack on mobile.

* colStackOnMobile: true | false

### **columns**

List of the row columns. Each column type is identified with a weight parameter to indicate how much horizontal space they fill.\
We use a 12-column grid with the following values as available combinations:

* 12
* 9, 3
* 8, 4
* 6, 6
* 6, 3, 3
* 4, 8
* 4, 4, 4
* 3, 9
* 3, 3, 6
* 3, 6, 3
* 3, 3, 3, 3

All the columns weight inside a row must sum 12 as the total value.

See the example above in _General Row Schema_.

### **modules**

List of content modules inside a column

### **type**

Every module is identified by a type parameter. Available types are:

* _title_
* _paragraph_
* _image_
* _button_
* _divider_
* _HTML_

Each module type has a set of available options. If none is included, the editor will use the default values.

## Content types scheme and parameters <a href="#content-types-scheme-and-parameters" id="content-types-scheme-and-parameters"></a>

### **Text**

```javascript

{
  "type": "title",
  "text": "I'm a headline."
}, {
  "type": "paragraph",
  "text": "I can be a long paragraph, a short sentence, or a simple word."
}

```

**title** adds the text with the following attributes:

* Font-size: 18px
* Font-weight: Bold
* Text-align: left

**paragraph** will use the following formatting:

* Font-size: 14px
* Text-align: left

**text** contains the string that will be displayed as content:

* Must be a plain text string
* Quotation marks must be escaped to be compliant with the JSON format
* If not included, a default “Loren Ipsum” text string will be used

## **Additional text parameters**

```javascript

"align": "center" "left" "right"
"size": integer // value in px
"bold": boolean
"italic": boolean
"underline": boolean
"color": "#CFCFCF"
"linkColor": "#CFCFCF"

```

### **Image**

```javascript

{
    "type": "image",
    "src": "https://static.pexels.com/photos/248280/pexels-photo-248280.jpeg",
    "href": "https://www.beefree.io", //optional 
    "alt": "This is a sample image", //optional 
    "dynamicSrc": "http://srcto/dynamic/src" //optional 
}

```

**src** image public URL

**href** Image action URL (link)

**alt** alternate text

**dynamicSrc** when added, the content applies the dynamic image behavior and uses the value as dynamic URL

### **Button**

```javascript

{
  "type": "button",
  "text": "Read more",
  "href": "https://lipsum.com"
},{
  "module": "button",
  "text": "Keep in touch",
  "href": "mailto:growth@beefree.io?subject=Custom content test&body=Sent from a custom button"
}

```

**text** text string that will be displayed as the button content. Must be a plain text string.

If not included, a default text string will be used

**href** button action URL (link)

### **Additional button parameters**

```javascript

"color": "#CFCFCF"
"background-color": "#C2C2C2"

```

### **Divider**

```javascript

{"type":"divider"}

```

Currently there are no additional parameters.

### **HTML**

```json

{"type":"html","html":"<div class=\'our-class\'>This is custom HTML.<\/div>"}

```
