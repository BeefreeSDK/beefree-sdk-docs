# Button Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple Button Schema defines how buttons are structured and styled within email, page, and popup builders. It enables customization of appearance, behavior, and interactivity — including hover effects, borders, padding, and click-through destinations. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and design button blocks effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple Button Schema.

* **Schema Name:** Simple Button
* **Purpose:** Defines clickable buttons with configurable text, links, styling, and hover states.
* **Related Schemas:**
  * `definitions.schema.json` (for padding, border-radius, border-width)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_button.schema.json",
  "title": "Simple Button",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "button"
    },
    "label": {
      "type": "string",
      "format": "noAnchorTags"
    },
    "text": {
      "type": "string",
      "format": "noAnchorTags"
    },
    "href": {
      "type": "string"
    },
    "target": {
      "enum": ["_blank", "_self", "_top"]
    },
    "size": {
      "type": "integer",
      "minimum": 1
    },
    "color": {
      "type": "string"
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
    "contentPaddingTop": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "contentPaddingRight": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "contentPaddingLeft": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "contentPaddingBottom": {
      "$ref": "definitions.schema.json#/definitions/padding"
    },
    "hoverBackgroundColor": {
      "type": "string"
    },
    "hoverColor": {
      "type": "string"
    },
    "hoverBorderColor": {
      "type": "string"
    },
    "hoverBorderWidth": {
      "$ref": "definitions.schema.json#/definitions/borderWidth"
    },
    "locked": {
      "type": "boolean"
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
    "customFields": {
      "type": "object"
    }
  }
}
```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property                        | Type    | Mandatory                                                                                                                                       | Description                                                                      |
| ------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `text`                          | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The text of the button                                                           |
| `label` deprecated (use `text`) | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The label of the button                                                          |
| `href`                          | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The hyperlink reference                                                          |
| `target`                        | enum    | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The target of the hyperlink                                                      |
| `size`                          | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The size of the button text                                                      |
| `color`                         | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The color of the button text                                                     |
| `background-color`              | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The background color of the button                                               |
| `padding-top`                   | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The top padding of the button (0-60)                                             |
| `padding-right`                 | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The right padding of the button (0-60)                                           |
| `padding-bottom`                | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The bottom padding of the button (0-60)                                          |
| `padding-left`                  | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The left padding of the button (0-60)                                            |
| `contentPaddingTop`             | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The top content padding inside the button (0-60)                                 |
| `contentPaddingRight`           | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The right content padding inside the button (0-60)                               |
| `contentPaddingLeft`            | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The left content padding inside the button (0-60)                                |
| `contentPaddingBottom`          | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The bottom content padding inside the button (0-60)                              |
| `hoverBackgroundColor`          | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The hover background color of the button                                         |
| `hoverColor`                    | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The hover color of the button text                                               |
| `hoverBorderColor`              | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The hover border color of the button                                             |
| `hoverBorderWidth`              | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The hover border width of the button (0-30)                                      |
| `locked`                        | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the button is locked                                                     |
| `border-radius`                 | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The border radius of the button (0-60)                                           |
| `border-color`                  | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The border color of the button                                                   |
| `border-width`                  | integer | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The border width of the button (0-30)                                            |
| `customFields`                  | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields                                                                    |
| `locked`                        | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | <p>Whether the module is locked</p><p>not available for single content addon</p> |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example Button

```json
{
  "text": "Click Me",
  "href": "https://example.com",
  "target": "_blank",
  "size": 12,
  "color": "#FFFFFF",
  "background-color": "#0000FF",
  "padding-top": 10,
  "padding-right": 10,
  "padding-bottom": 10,
  "padding-left": 10,
  "contentPaddingTop": 5,
  "contentPaddingRight": 5,
  "contentPaddingLeft": 5,
  "contentPaddingBottom": 5,
  "hoverBackgroundColor": "#FF0000",
  "hoverColor": "#00FF00",
  "hoverBorderColor": "#000000",
  "hoverBorderWidth": 2,
  "locked": true,
  "border-radius": 15,
  "border-color": "#CCCCCC",
  "border-width": 1,
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

### Additional Considerations

Consider the following when working with the Simple Button Schema in Beefree SDK:

* **Accessibility:** Ensure button text clearly describes its action.
* **Consistency:** Use padding and border settings to align button style with other components.
* **Interactivity:** Customize hover states to enhance user experience.
* **Extensibility:** Use `customFields` for non-standard properties.
