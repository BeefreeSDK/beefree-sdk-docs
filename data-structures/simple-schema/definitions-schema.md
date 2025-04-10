# Definitions Schema

## Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the **Definitions Schema** acts as a shared helper resource, providing reusable validation rules and enums across other content schemas such as rows, buttons, titles, and more. It does not represent a standalone content block but supports consistency and maintainability across the schema ecosystem.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Definitions Schema.

* **Schema Name:** Definitions
* **Purpose:** Provides shared schema definitions used by other blocks for common properties like padding, border radius, border width, and module type.
* **Usage Context:** Referenced via `$ref` in other schemas to enforce value ranges and consistency.
* **Related Schemas:**
  * All content and layout schemas that use padding, border, or type enums (e.g., `simple_row`, `simple_button`, `simple_title`, etc.)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "definitions.schema.json",
  "title": "Definitions",
  "definitions": {
    "padding": {
      "type": "integer",
      "minimum": 0,
      "maximum": 60
    },
    "borderRadius": {
      "type": "integer",
      "minimum": 0,
      "maximum": 60
    },
    "borderWidth": {
      "type": "integer",
      "minimum": 0,
      "maximum": 30
    },
    "typeOfModules": {
      "enum": [
        "button",
        "divider",
        "heading",
        "html",
        "icons",
        "image",
        "list",
        "menu",
        "paragraph",
        "title"
      ]
    }
  }
}
```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Definition Name | Type    | Description                                                                                                                                                   |
| --------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `padding`       | integer | Standard padding value used across modules. Must be between 0 and 60.                                                                                         |
| `borderRadius`  | integer | Controls the roundness of corners. Must be between 0 and 60.                                                                                                  |
| `borderWidth`   | integer | Defines the width of borders. Must be between 0 and 30.                                                                                                       |
| `typeOfModules` | enum    | Enum representing supported module types: `"button"`, `"divider"`, `"heading"`, `"html"`, `"icons"`, `"image"`, `"list"`, `"menu"`, `"paragraph"`, `"title"`. |

## Additional Considerations

Consider the following when working with the Definitions Schema in Beefree SDK:

* **Reusability:** Always reference shared properties from this schema instead of redefining them.
* **Consistency:** Helps maintain uniform styling, validation, and developer experience across multiple content modules.
* **Extensibility:** New shared values (e.g., `fontWeight`, `alignmentOptions`, etc.) can be added here as the design system evolves.
