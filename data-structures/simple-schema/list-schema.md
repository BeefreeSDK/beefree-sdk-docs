# List Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple List Schema defines how list elements (ordered and unordered) are rendered within email, page, and popup builders. It allows developers to customize list appearance using text formatting, alignment, spacing, and HTML tags. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and style list blocks effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple List Schema.

* **Schema Name:** Simple List
* **Purpose:** Defines list blocks (`<ul>` or `<ol>`) with rich formatting and styling options.
* **Related Schemas:**
  * `definitions.schema.json` (for padding definitions)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_list.schema.json",
  "title": "Simple List",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "list"
    },
    "underline": {
      "type": "boolean"
    },
    "italic": {
      "type": "boolean"
    },
    "bold": {
      "type": "boolean"
    },
    "html": {
      "type": "string"
    },
    "text": {
      "type": "string"
    },
    "align": {
      "enum": ["left", "center", "right"]
    },
    "tag": {
      "enum": ["ol", "ul"]
    },
    "size": {
      "type": "integer",
      "minimum": 1
    },
    "color": {
      "type": "string"
    },
    "linkColor": {
      "type": "string"
    },
    "letter-spacing": {
      "type": "integer",
      "minimum": -99,
      "maximum": 99
    },
    "line-height": {
      "type": "number",
      "minimum": 0.5,
      "maximum": 3,
      "multipleOf": 0.00001
    },
    "padding-top": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "padding-right": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "padding-bottom": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "padding-left": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "locked": {
      "type": "boolean"
    },
    "direction": {
      "enum": ["ltr", "rtl"]
    },
    "customFields": {
      "type": "object"
    }
  }
}
```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property                      | Type    | Mandatory                                                                                                                                       | Description                                                                                             |
| ----------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `text`                        | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text content                                                                                        |
| `html`deprecated (use `text`) | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text content                                                                                        |
| `underline`                   | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the text is underlined                                                                          |
| `italic`                      | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the text is italicized                                                                          |
| `bold`                        | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the text is bold                                                                                |
| `align`                       | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The alignment of the text                                                                               |
| `tag`                         | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The HTML tag for the list                                                                               |
| `size`                        | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The size of the text                                                                                    |
| `color`                       | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The color of the text                                                                                   |
| `linkColor`                   | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The color of the links                                                                                  |
| `customFields`                | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields for the list                                                                              |
| `locked`                      | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | <p>Whether the module is locked</p><p><strong>Note:</strong> Not available for Single Content AddOn</p> |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example List

```json
{
  "text": "<ul><li>Item 1</li><li>Item 2</li></ul>",
  "underline": false,
  "italic": false,
  "bold": true,
  "align": "left",
  "tag": "ul",
  "size": 14,
  "color": "#000000",
  "linkColor": "#0000FF",
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

### Additional Considerations

Consider the following when working with the Simple List Schema in Beefree SDK:

* **Accessibility:** Lists help structure content semantically for assistive technologies.
* **Rich Formatting:** Use bold, italic, and alignment settings to control appearance.
* **Multilingual Support:** Use the `direction` field for RTL language compatibility.
* **Extensibility:** Use `customFields` for non-standard properties.
