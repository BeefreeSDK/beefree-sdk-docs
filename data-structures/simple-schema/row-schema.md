# Row Schema

## Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Row Schema defines how rows are structured within the email, page, and popup builders, controlling layout, styling, and responsive behavior. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and extend row configurations effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Row Schema.

* **Schema Name**: Simple Row
* **Purpose**: Defines the structure of rows in Beefree's layout system, including columns, styling, and mobile behavior.
* **Mandatory Fields**: `name`, `columns`
* **Related Schemas**:
  * `simple_column.schema.json` (nested columns)
  * `definitions.schema.json` (shared validation rules)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "simple_row.schema.json",
    "title": "Simple Row",
    "type": "object",
    "required": [
      "name",
      "columns"
    ],
    "additionalProperties": false,
    "properties": {
      "name": {
        "type": "string"
      },
      "locked": {
        "type": "boolean"
      },
      "colStackOnMobile": {
        "type": "boolean"
      },
      "rowReverseColStackOnMobile": {
        "type": "boolean"
      },
      "contentAreaBackgroundColor": {
        "type": "string"
      },
      "background-color": {
        "type": "string"
      },
      "background-image": {
        "type": "string"
      },
      "background-position": {
        "type": "string"
      },
      "background-repeat": {
        "type": "string"
      },
      "customFields": {
        "type": "object"
      },
      "border-radius": {
        "$ref": "definitions.schema.json#/definitions/borderRadius"
      },
      "border-color": {
        "type": "string"
      },
      "border-width": {
        "$ref": "definitions.schema.json#/definitions/borderWidth"
      },
      "columnsBorderRadius": {
        "$ref": "definitions.schema.json#/definitions/borderRadius"
      },
      "columnsSpacing": {
        "type": "integer",
        "minimum": 0,
        "maximum": 99
      },
      "vertical-align": {
        "type": "string",
        "enum": [
          "top",
          "middle",
          "bottom"
        ]
      },
      "display-condition": {
        "type": "object",
        "required": [
          "type"
        ],
        "properties": {
          "type": {
            "type": "string"
          },
          "label": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "before": {
            "type": "string"
          },
          "after": {
            "type": "string"
          }
        }
      },
      "metadata": {
        "type": "object"
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
      "columns": {
        "type": "array",
        "minItems": 1,
        "maxItems": 12,
        "items": {
          "$ref": "simple_column.schema.json"
        }
      }
    }
  }
```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property                     | Type    | Mandatory                                                                                                                | Description                                |
| ---------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------ |
| `name`                       | string  | ![check mark button](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/2705/path) Yes | The name of the row                        |
| `columns`                    | array   | ![check mark button](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/2705/path) Yes | The columns in the row                     |
| `locked`                     | boolean | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | Whether the row is locked                  |
| `colStackOnMobile`           | boolean | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | Whether columns stack on mobile            |
| `rowReverseColStackOnMobile` | boolean | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | Whether columns stack in reverse on mobile |
| `contentAreaBackgroundColor` | string  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The background color of the content area   |
| `background-color`           | string  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The background color of the row            |
| `background-image`           | string  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The background image of the row            |
| `background-position`        | string  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The background position of the row         |
| `background-repeat`          | string  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The background repeat property of the row  |
| `border-radius`              | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The border radius of the row (0-60)        |
| `border-color`               | string  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The border color of the row                |
| `border-width`               | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The border width of the row (0-30)         |
| `columnsBorderRadius`        | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The border radius of the columns (0-60)    |
| `columnsSpacing`             | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The spacing between columns (0-99)         |
| `vertical-align`             | enum    | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The vertical alignment of the row          |
| `display-condition`          | object  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The display condition of the row           |
| `padding-top`                | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The top padding of the row (0-60)          |
| `padding-right`              | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The right padding of the row (0-60)        |
| `padding-bottom`             | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The bottom padding of the row (0-60)       |
| `padding-left`               | integer | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | The left padding of the row (0-60)         |
| `customFields`               | object  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | Custom fields for the row                  |
| `metadata`                   | object  | ![cross mark](https://growens.atlassian.net/gateway/api/emoji/9080f9a9-4ebb-4545-9108-b217c05f14c6/274c/path) No         | Metadata for the row                       |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Row

```json
{
  "name": "Sample Row",
  "locked": false,
  "colStackOnMobile": true,
  "rowReverseColStackOnMobile": false,
  "contentAreaBackgroundColor": "#FFFFFF",
  "background-color": "#F0F0F0",
  "background-image": "<https://example.com/background.png>",
  "background-position": "center",
  "background-repeat": "no-repeat",
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  },
  "border-radius": 10,
  "border-color": "#000000",
  "border-width": 2,
  "columnsBorderRadius": 5,
  "columnsSpacing": 10,
  "vertical-align": "middle",
  "display-condition": {
    "type": "visibility",
    "label": "Show on mobile",
    "description": "Display this row on mobile devices",
    "before": "2023-01-01",
    "after": "2022-01-01"
  },
  "metadata": {
    "author": "John Doe",
    "version": "1.0"
  },
  "padding-top": 10,
  "padding-right": 10,
  "padding-bottom": 10,
  "padding-left": 10,
  "columns": [
    ...
  ]
}
```

## Additional Considerations

Consider the following when working when Simple Row Schema in Beefree SDK:

* **Extensibility**: Use `customFields` for non-standard properties.
