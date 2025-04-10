# Menu Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Menu Schema defines how navigation menus are configured and rendered within email, page, and popup builders. It supports lists of items with links, customizable paddings, and metadata. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and customize menu blocks effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Menu Schema.

* **Schema Name:** Simple Menu
* **Purpose:** Defines navigational menu structures made of multiple text-and-link items with styling support.
* **Related Schemas:**
  * `definitions.schema.json` (for padding values)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_menu.schema.json",
  "title": "Simple Menu",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "menu"
    },
    "items": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "type": {
            "const": "menu-item"
          },
          "text": {
            "type": "string"
          },
          "link": {
            "type": "object",
            "additionalProperties": false,
            "properties": {
              "title": {
                "type": "string"
              },
              "href": {
                "type": "string",
                "format": "urlOrMergeTags"
              },
              "target": {
                "enum": ["_blank", "_self", "_top"]
              }
            }
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

**Level 1: `simple_menu.schema.json` Properties**

| Property         | Type    | Mandatory                                                                                                                                       | Description                                                                                             |
| ---------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `items`          | array   | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The menu items                                                                                          |
| `padding-top`    | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The top padding (0-60)                                                                                  |
| `padding-right`  | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The right padding (0-60)                                                                                |
| `padding-bottom` | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The bottom padding (0-60)                                                                               |
| `padding-left`   | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The left padding (0-60)                                                                                 |
| `locked`         | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the menu is locked                                                                              |
| `customFields`   | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields for the menu                                                                              |
| `locked`         | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | <p>Whether the module is locked <strong>Note:</strong></p><p>Not available for single content addon</p> |

**Level 2: `items` Array Properties**

| Property | Type   | Mandatory                                                                                                                                       | Description                       |
| -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| `text`   | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text of the menu item         |
| `link`   | object | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The link object for the menu item |

**Level 3: `link` Object Properties**

| Property | Type   | Mandatory                                                                                                                                       | Description            |
| -------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `title`  | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The title of the link  |
| `href`   | string | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The URL of the link    |
| `target` | enum   | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The target of the link |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Menu

```json
{
  "items": [
    {
      "text": "Home",
      "link": {
        "title": "Home",
        "href": "<https://example.com>",
        "target": "_self"
      }
    },
    {
      "text": "About",
      "link": {
        "title": "About",
        "href": "<https://example.com/about>",
        "target": "_self"
      }
    }
  ],
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

Consider the following when working with the Simple Menu Schema in Beefree SDK:

* **Accessibility:** Use the `title` field in `link` to improve accessibility for screen readers.
* **Responsive Design:** Menu alignment and padding should be tested across devices for layout consistency.
* **Extensibility:** Use `customFields` for non-standard properties.
