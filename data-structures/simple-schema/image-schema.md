# Image Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Image Schema defines how image blocks are configured and rendered within email, page, and popup builders. It manages image sources, alt text, click behavior, and styling such as padding. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and customize image blocks effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Image Schema.

* **Schema Name:** Simple Image
* **Purpose:** Defines image elements with support for alt text, links, dynamic sources, and styling.
* **Related Schemas:**
  * `definitions.schema.json` (for padding definitions)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_image.schema.json",
  "title": "Simple Image",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "image"
    },
    "alt": {
      "type": "string"
    },
    "href": {
      "type": "string"
    },
    "src": {
      "type": "string",
      "format": "urlOrMergeTags"
    },
    "dynamicSrc": {
      "type": "string"
    },
    "target": {
      "enum": ["_blank", "_self", "_top"]
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

| Property         | Type    | Mandatory                                                                                                                                       | Description                                                                                               |
| ---------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `src`            | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The source URL of the image                                                                               |
| `alt`            | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The alt text for the image                                                                                |
| `href`           | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The URL the image links to                                                                                |
| `dynamicSrc`     | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The dynamic source URL of the image                                                                       |
| `target`         | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The target for the link                                                                                   |
| `padding-top`    | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The top padding (0-60)                                                                                    |
| `padding-right`  | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The right padding (0-60)                                                                                  |
| `padding-bottom` | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The bottom padding (0-60)                                                                                 |
| `padding-left`   | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The left padding (0-60)                                                                                   |
| `customFields`   | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields                                                                                             |
| `locked`         | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | <p>Whether the module is locked.</p><p><strong>Note:</strong> Not available for Single Content AddOn.</p> |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Image

```json
{
  "src": "<https://example.com/image.png>",
  "alt": "Sample Image",
  "href": "<https://example.com>",
  "dynamicSrc": "<https://example.com/dynamic-image.png>",
  "target": "_blank",
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

Consider the following when working with the Simple Image Schema in Beefree SDK:

* **Accessibility:** Always provide meaningful `alt` text for screen readers and fallback scenarios.
* **Extensibility:** Use `customFields` for non-standard properties.
