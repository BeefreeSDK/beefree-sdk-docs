# Brand Style API Endpoint

### Overview <a href="#_e7tjitffe17" id="_e7tjitffe17"></a>

The Brand Management API endpoint enables you to manage and modify the style of email, pages, and popup templates. While the Content Defaults feature enables you to set default styles for new content elements like headings, paragraphs, and buttons, the Brand Management API takes it a step further. It allows you to make template-wide design changes to existing templates quickly and easily, ensuring that all modules adhere to the broader design system or brand guidelines. In this article, we'll explore what this API endpoint is, its benefits, how to get started with it, and how it differs from Content Defaults.

### How to Apply Styles Globally <a href="#_7o6uselkp1bb" id="_7o6uselkp1bb"></a>

To apply a style globally, take the following steps:

1. **Define Brand Styles:** Begin by defining your brand's styles within the schema. The CSAPI Brand Style mirrors the [Content Defaults’ JSON](https://docs.beefree.io/content-defaults/). This enables you to reuse the styles you’ve defined in your application’s frontend. Use the same schema to specify colors, fonts, and any other design elements that you want to apply uniformly.
2. **Prepare the Template:** Ensure that you have the JSON template ready, which serves as the foundation for your branding modifications.
3. **API Call:** Make an API call to the Brand Management API endpoint, providing the schema with your defined brand styles and the JSON template to be updated.
4. **API Processing:** The API will take care of processing your request. It will automatically merge the specified brand styles into the template, applying the desired changes globally.
5. **Receive Modified Template:** After the API processes your request, it will return the modified JSON template with the updated styles. This template is now ready to be used in your marketing campaigns with the consistent branding you've defined.

### Authentication <a href="#_cd49yafb8cb2" id="_cd49yafb8cb2"></a>

Authentication is essential to secure access to the Brand Style API. We use API keys to authenticate requests. The API key you should use to access this endpoint is the CSAPI API key available in your Beefree SDK Developer Console. If you do not have a CSAPI key in your Developer Console, ensure you have a [paid plan](https://developers.beefree.io/pricing-plans).

Include the API key in the request header as follows:

```http
Authorization: Bearer YOUR_API_KEY
```

### Endpoint <a href="#_tjfpide02wrb" id="_tjfpide02wrb"></a>

`/template/brand`

**HTTP Method:** POST

**Description:** Apply brand styles to a template, ensuring a consistent visual identity.

Request Parameters:

* `styles` (JSON): The brand styles to apply to the template.
* `template` (JSON): The JSON template to be updated with the brand styles.
* `HTML:` Return the template with or without HTML.

The following section displays an example request. Note that the syntax for the Content Services Brand Style API is similar to the [syntax for Content Defaults](https://docs.beefree.io/content-defaults/).

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

You can define multiple classes of buttons, images, and rows by passing an array of styles targeting design elements by their class names.To provide multiple styles, use the className property to define as many styles as you like. Prior to defining the className within the array, ensure you define the className within the template using the [Custom Attribute feature](https://docs.beefree.io/custom-attributes/).

The following examples displays a button array.

```
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

* 200 OK: The request was successful, and the modified template is returned.
* 400 Bad Request: There was an issue with the request parameters.
* 401 Unauthorized: The API key is invalid or missing.
* 500 Internal Server Error: An unexpected server error occurred.

Example Response:

```json
{
  "html": “html document”,
  "json": {
    // Updated template JSON here
  }
}
```

### Request Format <a href="#_y0bhuvxyyjqv" id="_y0bhuvxyyjqv"></a>

This section discusses the request formats for the different parameters.

#### Styles <a href="#_7lu3ox92rnjx" id="_7lu3ox92rnjx"></a>

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

#### Template <a href="#_6ac40siq79ge" id="_6ac40siq79ge"></a>

The template parameter should contain your template's JSON structure. Ensure that the JSON structure aligns with the template you intend to update.

### Using the Brand Style Schema <a href="#_27qaij98qcq2" id="_27qaij98qcq2"></a>

The Brand Style API schema is designed to be user-friendly and intuitive. You can use the same [Content Defaults schema](https://docs.beefree.io/content-defaults/) you used to style your application’s frontend with the Brand Style API.

For example:

```json
"styles": {
  "general": {
    "background": "#eeeeee",
    "links": "#0068a5"
  }
}
```

The API will take these styles and automatically merge them with your design template, eliminating the need for complex manual editing.

### Difference Between Content Defaults and the Brand Management API Endpoint <a href="#_wclj1emdvfnj" id="_wclj1emdvfnj"></a>

While both Content Defaults and the Brand Management API aim to streamline the design process, they serve different purposes:

#### Content Defaults <a href="#_8mbnu8skeyea" id="_8mbnu8skeyea"></a>

* Can be a part of the [Configuration Parameter](https://docs.beefree.io/configuration-parameters/).
* Set default styles for specific content types.
* Useful for quickly creating new templates with consistent styling.

#### Brand Management API Endpoint <a href="#_9bf5ceyotoe8" id="_9bf5ceyotoe8"></a>

* API that enables the development of a user interface that empowers end users to make style changes with ease and speed.
* Modify the style of existing templates.
* Suitable for users who need to make template-wide design changes or maintain brand consistency on existing templates.
