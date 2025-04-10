# Divider Schema

## Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Divider Schema defines visual divider elements, used to create separation between blocks of content. Dividers are available **only within row addons**, including mixed and custom rows (not as standalone content blocks). This documentation breaks down the schema’s properties, configuration rules, and practical usage to help you effectively implement dividers into your layout system.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Divider Schema.

* **Schema Name:** Simple Divider
* **Purpose:** Renders a horizontal visual divider with customizable size, color, and spacing.
* **Restrictions:** Can only be used in **row addons**, **mixed rows**, or **custom rows**. Not supported as a standalone content addon.
* **Related Schemas:**
  * `definitions.schema.json` (for padding definitions)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_divider.schema.json",
  "title": "Simple Divider",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "divider"
    },
    "color": {
      "type": "string"
    },
    "height": {
      "type": "integer",
      "minimum": 1,
      "maximum": 30
    },
    "width": {
      "type": "integer",
      "minimum": 1,
      "maximum": 100
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

| Property         | Type    | Mandatory                                                                                                                                       | Description                       |
| ---------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| `color`          | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The color of the divider          |
| `height`         | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The height of the divider (1-30)  |
| `width`          | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The width of the divider (1-100)  |
| `padding-top`    | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The top padding of the divider    |
| `padding-right`  | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The right padding of the divider  |
| `padding-bottom` | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The bottom padding of the divider |
| `padding-left`   | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The left padding of the divider   |
| `locked`         | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the module is locked      |
| `customFields`   | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields for the divider     |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Divider

```json
{
  "type": "divider",
  "color": "#000000",
  "height": 10,
  "width": 50,
  "padding-top": 5,
  "padding-right": 5,
  "padding-bottom": 5,
  "padding-left": 5,
  "locked": false,
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

### Additional Considerations

Consider the following when working with the Simple Divider Schema in Beefree SDK:

* **Responsiveness:** Use percentage-based widths to ensure adaptive layout behavior across devices.
* **Design Consistency:** Apply consistent height and color to create visual rhythm in your layout.
* **Extensibility:** Use `customFields` for non-standard properties.
