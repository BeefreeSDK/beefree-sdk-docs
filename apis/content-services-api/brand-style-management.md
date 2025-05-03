---
description: >-
  This page lists and describes the Brand Style category of endpoints within the
  Content Services API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Brand Style

### Overview <a href="#e7tjitffe17" id="e7tjitffe17"></a>

The Brand Style endpoints enables you to manage and modify the style of email, pages, and popup templates. While the Content Defaults feature enables you to set default styles for new content elements like headings, paragraphs, and buttons, the Brand Style Management endpoint takes it a step further. It allows you to make template-wide design changes to existing templates quickly and easily, ensuring that all modules adhere to the broader design system or brand guidelines. In this article, we'll explore what this Content Services API (CSAPI) Brand Style Management endpoint is, its benefits, how to get started with it, and how it differs from Content Defaults.

### How to Apply Styles Globally <a href="#id-7o6uselkp1bb" id="id-7o6uselkp1bb"></a>

To apply a style globally, take the following steps:

1. **Manage Brand Styles:** Begin by defining your brand's styles within the schema. The Brand Style Management endpoint schema mirrors the [Content Defaults’ JSON](https://docs.beefree.io/content-defaults/). This enables you to easily reuse the styles you’ve already defined in your application’s frontend. Use the same schema to specify colors, fonts, and any other design elements you want to apply uniformly.
2. **Prepare the Template:** Ensure you have the JSON template ready, which is the foundation for your branding modifications.
3. **API Call:** Make an API call to the CSAPI Brand Style Management endpoint, providing the schema with your defined brand styles and the JSON template to be updated.
4. **API Processing:** The API will take care of processing your request. It will automatically merge the specified brand styles into the template, applying the desired changes globally.
5. **Receive Modified Template:** After the API processes your request, it will return the modified JSON template with the updated styles. This template is now ready to be used in your marketing campaigns with the consistent branding you've defined.

### Endpoints <a href="#tjfpide02wrb" id="tjfpide02wrb"></a>

`/template/brand` or `/row/brand`

**HTTP Method:** `POST`

**Description:** Apply brand styles to a template or row, ensuring a consistent visual identity.

{% openapi src="../../.gitbook/assets/template_brand.yaml" path="/v1/template/brand" method="post" %}
[template_brand.yaml](../../.gitbook/assets/template_brand.yaml)
{% endopenapi %}



**Request Parameters:**

* `styles` (JSON): The brand styles to apply to the template.
* `template` (JSON): The JSON template to be updated with the brand styles.
* `HTML` Return the template with or without HTML.

The following section displays an example request. Note that the syntax for the CSAPI Brand Style Management endpoint is similar to the syntax for [Content Defaults](../../other-customizations/appearance/content-defaults.md).

Example Request:

```json
POST / template / brand
Content-Type: application / json
Authorization: Bearer YOUR_API_KEY 

{
    "styles": {
        "general": {
            "background": "#eeeeee",
            "links": "#0068a5"
        },
        "h1": {
            "styles": {
                "color": "#333333",
                "fontSize": "36px"
            }
        },
        "h2": {
            "styles": {
                "color": "#CCCCCC",
                "fontSize": 246 px "
            }
        },
        "paragraph": {
            "styles": {
                "color": "#333333",
                "fontSize": "16px"
            }
        },
        "button": {
            "styles": {
                "backgroundColor": "#ff9900",
                "borderRadius": "5px"
            }
        }
    },
    "template": {
        // Your template JSON here
    }
}
```

You can define multiple classes of buttons, images, and rows by passing an array of styles targeting design elements by their class names. To provide multiple styles, use the `className` property to define as many styles as you like. Before defining the `className` within the array, ensure you define the `className` within the template using the [Custom Attribute feature](https://docs.beefree.io/custom-attributes/).

The following examples displays a button array.

```json
{
  "styles": {
    "button": [
      {
        "className": "Primary",
        ...more styles
      },
      {
        "className": "Secondary",
        ...more styles     
      }
    ]
  }
}
```

Response Format:

* **200 OK:** The request was successful, and the modified template was returned.
* **400 Bad Request:** There was an issue with the request parameters.
* **401 Unauthorized:** The API key is invalid or missing.
* **500 Internal Server Error:** An unexpected server error occurred.

Example Response:

```json
{
  "html": “html document”,
  "json": {
    // Updated template JSON here
  }
}
```

### Request Format <a href="#y0bhuvxyyjqv" id="y0bhuvxyyjqv"></a>

This section discusses the request formats for the different parameters.

#### Styles <a href="#id-7lu3ox92rnjx" id="id-7lu3ox92rnjx"></a>

The styles parameter in the request should follow this JSON format:

```json
{
  "general": {
    // General brand styles
  },
  "title": {
    // Title block styles
  },
  "text": {
    // Text block styles
  },
  "button": {
    // Button block styles
  },
  // Add more block styles as needed
}
```

Each block style can include attributes such as colors, fonts, borders, and more, depending on your brand's requirements. For additional code samples of each content block type and its respective style customization options, reference the [Content Defaults schema page](https://docs.beefree.io/content-defaults/).

{% hint style="danger" %}
**Note:** The `mobileStyles` and `hoverStyles` properties are not supported by the Brand Style Management API.
{% endhint %}

#### Template <a href="#id-6ac40siq79ge" id="id-6ac40siq79ge"></a>

The template parameter should contain your template's JSON structure. Ensure that the JSON structure aligns with the template you intend to update.

### Table Content Defaults <a href="#id-27qaij98qcq2" id="id-27qaij98qcq2"></a>

Both the [Content Defaults](../../other-customizations/appearance/content-defaults.md#table) (frontend) and Brand Style Management endpoint (backend) include the table content block.

The following code shows an example of how to configure the style for headers within the table content block:

```json
{
  "headersBackgroundColor": "#EAEAEA",
  "headersColor": "#505659",
  "headersFontSize": "14px",
  "headersFontWeight": "400",
  "headersTextAlign": "left",
  "linkColor": "#0068a5"
}
```

### Using the Brand Style Management Schema <a href="#id-27qaij98qcq2" id="id-27qaij98qcq2"></a>

The Brand Style Management endpoint schema is designed to be user-friendly and intuitive. You can use the same [Content Defaults schema](https://docs.beefree.io/content-defaults/) you used to style your application’s frontend with the Brand Style Management endpoint.

For example:

```json
"styles": {
  "general": {
    "background": "#eeeeee",
    "links": "#0068a5"
  }
}
```

The CSAPI Brand Style Management endpoint will take these styles and merge them with your design template, eliminating the need for complex manual editing.

### Difference Between Content Defaults and the Brand Style Management Endpoint <a href="#wclj1emdvfnj" id="wclj1emdvfnj"></a>

While both Content Defaults and the Brand Style Management endpoint aim to streamline the design process, they serve different purposes:

#### Content Defaults <a href="#id-8mbnu8skeyea" id="id-8mbnu8skeyea"></a>

* Can be a part of the [Configuration Parameter](../../getting-started/readme/installation/configuration-parameters/).
* Set default styles for specific content types.
* Useful for quickly creating new templates with consistent styling.

#### Brand Style Management Endpoint <a href="#id-9bf5ceyotoe8" id="id-9bf5ceyotoe8"></a>

* CSAPI endpoint that enables the development of a user interface that empowers end users to make style changes with ease and speed.
* Modify the style of existing templates.
* Suitable for users who need to make template-wide design changes or maintain brand consistency on existing templates.
