# Column Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Column object defines how individual columns are structured within rows across builders for emails, pages, and popups. It manages layout weight, background styling, padding, borders, and the content modules it contains. This documentation breaks down the column’s properties, requirements, and usage examples to help you implement and customize columns effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Column object.

* **Schema Name**: Column
* **Purpose**: Defines the layout and styling of a single column within a row, including spacing, background, and the modules it contains.
* **Mandatory Fields**: (None explicitly required in schema)
* **Related Schemas**:
  * `definitions.schema.json` (for padding and border definitions)
  * `simple_row.schema.json` (defines how columns are grouped in rows)

### Structure Definition

Below is a representative structure of the Column object and a breakdown of each property.

{% hint style="danger" %}
**Important:** Ensure the sum of each column's weight is **equal to 12** for the `weight` property. It can't be a different number.
{% endhint %}

#### JSON Object

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_column.schema.json",
  "title": "Simple Column",
  "type": "object",
  "required": [
    "weight",
    "modules"
  ],
  "additionalProperties": false,
  "properties": {
    "weight": {
      "type": "integer",
      "minimum": 1,
      "maximum": 12
    },
    "background-color": {
      "type": "string"
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
    "border-color": {
      "type": "string"
    },
    "border-width": {
      "$ref": "definitions.schema.json#/definitions/borderWidth"
    },
    "modules": {
      "type": "array",
      "minItems": 0,
      "items": {
        "type": "object",
        "required": [
          "type"
        ],
        "discriminator": {
          "propertyName": "type"
        },
        "properties": {
          "type": {
            "$ref": "definitions.schema.json#/definitions/typeOfModules"
          }
        },
        "oneOf": [
          {
            "$ref": "simple_button.schema.json"
          },
          {
            "$ref": "simple_divider.schema.json"
          },
          {
            "$ref": "simple_html.schema.json"
          },
          {
            "$ref": "simple_icons.schema.json"
          },
          {
            "$ref": "simple_image.schema.json"
          },
          {
            "$ref": "simple_list.schema.json"
          },
          {
            "$ref": "simple_menu.schema.json"
          },
          {
            "$ref": "simple_paragraph.schema.json"
          },
          {
            "$ref": "simple_title.schema.json"
          }
        ]
      }
    },
    "customFields": {
      "type": "object"
    }
  }
}
```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property           | Type    | Mandatory                                                                                                                                               | Description                        |
| ------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| `weight`           | integer | ![check mark button](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/2705.png) Yes | The weight of the column (1-12)    |
| `modules`          | array   | ![check mark button](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/2705.png) Yes | The modules in the column          |
| `background-color` | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The background color of the column |
| `padding-top`      | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The top padding (0-60)             |
| `padding-right`    | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The right padding (0-60)           |
| `padding-bottom`   | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The bottom padding (0-60)          |
| `padding-left`     | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The left padding (0-60)            |
| `border-color`     | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The border color of the column     |
| `border-width`     | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | The border width (0-30)            |
| `customFields`     | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No         | Custom fields for the column       |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Column

```json
{
  "weight": 6,
  "background-color": "#FFFFFF",
  "padding-top": 10,
  "padding-right": 10,
  "padding-bottom": 10,
  "padding-left": 10,
  "border-color": "#000000",
  "border-width": 2,
  "modules": [
    {
      "type": "text",
      "text": "This is a sample column"
    }
  ],
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

## Additional Considerations

When working with Column objects in the Beefree SDK:

* **Responsive Layouts**: Use `weight` strategically to define flexible multi-column arrangements across devices.
* **Styling**: Combine background, border, and padding settings for visual structure and emphasis.
* **Extensibility**:  Use `customFields` for non-standard properties.
