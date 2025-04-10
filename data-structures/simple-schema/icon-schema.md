# Icon Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Icons Schema defines a block used to display one or more icons alongside optional labels, titles, and links. It allows layout control over icon size, positioning, and interaction behavior. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and customize icon blocks effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Icons Schema.

* **Schema Name:** Simple Icons
* **Purpose:** Defines icon-based elements with configurable image, text, positioning, and linking.
* **Mandatory Fields:** `image`, `width`, `height`, `textPosition` (per icon)
* **Related Schemas:**
  * `definitions.schema.json` (for padding definitions)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_icons.schema.json",
  "title": "Simple Icons",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "icons"
    },
    "icons": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "required": ["image", "textPosition", "width", "height"],
        "properties": {
          "alt": {
            "type": "string"
          },
          "text": {
            "type": "string"
          },
          "title": {
            "type": "string"
          },
          "image": {
            "type": "string",
            "format": "urlOrMergeTags"
          },
          "href": {
            "type": "string",
            "format": "urlOrMergeTags"
          },
          "height": {
            "type": "string"
          },
          "width": {
            "type": "string"
          },
          "target": {
            "enum": ["_blank", "_self", "_top"]
          },
          "textPosition": {
            "enum": ["left", "right", "top", "bottom"]
          }
        }
      }
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

The following tables list the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

**Level 1: `simple_icons.schema.json` Properties**

| Property       | Type    | Mandatory                                                                                                                                       | Description                                                                                             |
| -------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `icons`        | array   | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The icons array                                                                                         |
| `customFields` | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields for the icons                                                                             |
| `locked`       | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | <p>Whether the module is locked</p><p><strong>Note:</strong> Not available for Single Content AddOn</p> |

**Level 2: `icons` Array Properties**

| Property       | Type   | Mandatory                                                                                                                                               | Description               |
| -------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `image`        | string | ![check mark button](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/2705.png) Yes | The URL of the icon image |
| `width`        | string | ![check mark button](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/2705.png) Yes | The width of the icon     |
| `height`       | string | ![check mark button](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/2705.png) Yes | The height of the icon    |
| `textPosition` | enum   | ![check mark button](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/2705.png) Yes | The position of the text  |
| `alt`          | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The alt text for the icon |
| `text`         | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The text for the icon     |
| `title`        | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The title of the icon     |
| `href`         | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The URL the icon links to |
| `target`       | enum   | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The target of the link    |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Icons

```json
{
  "icons": [
    {
      "alt": "Icon 1",
      "text": "Icon Text 1",
      "title": "Icon Title 1",
      "image": "<https://example.com/icon1.png>",
      "href": "<https://example.com>",
      "height": "24px",
      "width": "24px",
      "target": "_self",
      "textPosition": "left"
    },
    {
      "alt": "Icon 2",
      "text": "Icon Text 2",
      "title": "Icon Title 2",
      "image": "<https://example.com/icon2.png>",
      "href": "<https://example.com>",
      "height": "24px",
      "width": "24px",
      "target": "_self",
      "textPosition": "right"
    }
  ],
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

### Additional Considerations

Consider the following when working with the Simple Icons Schema in Beefree SDK:

* **Accessibility:** Use `alt` and `title` fields to improve usability and accessibility.
* **Responsiveness:** Icons and labels should adapt well in mobile layouts using `textPosition`.
* **Consistency:** Ensure icon dimensions (`height`, `width`) are aligned for visual harmony.
* **Extensibility:** Use `customFields` for non-standard properties.
