# HTML Schema

### Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In Beefree SDK, the Simple HTML Schema enables the inclusion of raw HTML code blocks within email, page, and popup builders. This provides full flexibility for embedding custom markup, third-party widgets, or advanced layouts not covered by predefined content blocks. This documentation breaks down the schema's properties, requirements, and usage examples to help you implement and manage custom HTML inserts effectively.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

### Schema Overview

This section summarizes the purpose and key characteristics of the Simple HTML Schema.

* **Schema Name:** Simple HTML
* **Purpose:** Allows insertion of raw HTML content for full flexibility in layout and functionality.
* **Mandatory Fields:** `html`

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_html.schema.json",
  "title": "Simple Html",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "const": "html"
    },
    "html": {
      "type": "string"
    },
    "customFields": {
      "type": "object"
    },
    "locked": {
      "type": "boolean"
    }
  }
}
```

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property       | Type    | Mandatory                                                                                                                                       | Description                                                                   |
| -------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `html`         | string  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | The HTML content                                                              |
| `customFields` | object  | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Custom fields for the HTML                                                    |
| `locked`       | boolean | ![cross mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/ef8b0642-7523-4e13-9fd3-01b65648acf6/32x32/274c.png) No | Whether the module is locked **Note:** Not available for Single Content AddOn |

### Usage Examples

Reference an example of the schema in the following code snippet.

#### Example HTML

```json
{
  "html": "<div>Sample HTML</div>",
  "customFields": {
    "custom1": "value1",
    "custom2": "value2"
  }
}
```

### Additional Considerations

Consider the following when working with the Simple HTML Schema in Beefree SDK:

* **Use Responsibly:** This block is powerful, but bypasses visual editor constraints. Use it for advanced or dynamic scenarios.
* **Extensibility:** Use `customFields` for non-standard properties.
