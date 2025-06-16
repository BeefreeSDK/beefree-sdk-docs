# Title Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Title Schema defines how titles (headings) are represented within builders for emails, pages, and popups. It manages styling, typography, alignment, and responsive behavior. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and extend title blocks effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Title Schema.

* **Schema Name:** Simple Title
* **Purpose:** Defines title elements (e.g., headings) with formatting options like bold, underline, alignment, and spacing.
* **Related Schemas:**
  * `definitions.schema.json` (for padding definitions)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_title.schema.json",
  "title": "Simple Title",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "enum": [
        "title",
        "heading"
      ]
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
      "enum": [
        "left",
        "center",
        "right",
        "justify"
      ]
    },
    "title": {
      "enum": [
        "h1",
        "h2",
        "h3"
      ]
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
    "direction": {
      "enum": [
        "ltr",
        "rtl"
      ]
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
    "customFields": {
      "type": "object"
    }
  }
}

```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property                     | Type    | Mandatory                                                                                                                                       | Description                                                                             |
| ---------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `text`                       | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text content of the title                                                           |
| `html` deprecated (use text) | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text content of the title                                                           |
| `underline`                  | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the text is underlined                                                          |
| `italic`                     | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the text is italicized                                                          |
| `bold`                       | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the text is bold                                                                |
| `align`                      | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The alignment of the text                                                               |
| `title`                      | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The title level (h1, h2, h3)                                                            |
| `size`                       | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The size of the text (minimum 1)                                                        |
| `color`                      | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The color of the text                                                                   |
| `linkColor`                  | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The color of the links                                                                  |
| `letter-spacing`             | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The letter spacing (-99 to 99)                                                          |
| `line-height`                | number  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The line height (0.5 to 3)                                                              |
| `direction`                  | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text direction (ltr, rtl)                                                           |
| `padding-top`                | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The top padding (0-60)                                                                  |
| `padding-right`              | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The right padding (0-60)                                                                |
| `padding-bottom`             | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The bottom padding (0-60)                                                               |
| `padding-left`               | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The left padding (0-60)                                                                 |
| `customFields`               | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields                                                                           |
| `locked`                     | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the module is locked. **Note:** This is not available for Single Content AddOn. |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Title

```json
{
  "underline": true,
  "italic": false,
  "bold": true,
  "text": "Welcome",
  "align": "center",
  "title": "h1",
  "size": 24,
  "color": "#000000",
  "linkColor": "#FF0000",
  "letter-spacing": 1,
  "line-height": 1.5,
  "direction": "ltr",
  "padding-top": 10,
  "padding-right": 10,
  "padding-bottom": 10,
  "padding-left": 10,
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

### Additional Considerations

Consider the following when working with the Simple Title Schema in Beefree SDK:

* **Extensibility:** Use `customFields` for non-standard properties.
* **Responsiveness:** Text alignment and direction settings help support responsive, multilingual layouts.
