---
description: >-
  This page lists and describes the Brand Style category of endpoints within the
  Content Services API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Brand Style

### Overview <a href="#e7tjitffe17" id="e7tjitffe17"></a>

The Brand Style endpoints enables you to manage and modify the style of email, pages, and popup templates. While the [Content Defaults](../../other-customizations/appearance/content-defaults.md) feature enables you to set default styles for new content elements like headings, paragraphs, and buttons, the Brand Style Management endpoint takes it a step further. It allows you to make template-wide design changes to existing templates quickly and easily, ensuring that all modules adhere to the broader design system or brand guidelines. In this article, we'll explore what this Content Services API (CSAPI) Brand Style Management endpoint is, its benefits, how to get started with it, and how it differs from Content Defaults.

### How to Apply Styles Globally <a href="#id-7o6uselkp1bb" id="id-7o6uselkp1bb"></a>

To apply a style globally, take the following steps:

1. **Manage Brand Styles:** Begin by defining your brand's styles within the schema. The Brand Style Management endpoint schema mirrors the [Content Defaults’ JSON](https://docs.beefree.io/content-defaults/). This enables you to easily reuse the styles you’ve already defined in your application’s frontend. Use the same schema to specify colors, fonts, and any other design elements you want to apply uniformly.
2. **Prepare the Template:** Ensure you have the JSON template ready, which is the foundation for your branding modifications.
3. **API Call:** Make an API call to the CSAPI Brand Style Management endpoint, providing the schema with your defined brand styles and the JSON template to be updated.
4. **API Processing:** The API will take care of processing your request. It will automatically merge the specified brand styles into the template, applying the desired changes globally.
5. **Receive Modified Template:** After the API processes your request, it will return the modified JSON template with the updated styles. This template is now ready to be used in your marketing campaigns with the consistent branding you've defined.

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the Brand Style resource. Reference the [Brand Style Resource and Collection Options table](./#brand-style) for a list of available option.
{% endhint %}

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

### Understanding API Responses

The Brand Style API includes a `422` status code (unprocessable entity). This status code is returned when an API call is successful, but the brand style defined in the body of the API call does not apply to the template specified. For example, if the brand style defined in the body of the API call applies to buttons, and there are no buttons within the specified template, no styles will be applied. In this scenario, the final result of the API call is that no styles were applied to the template because there were none applicable. Be sure to handle this specific case when implementing the API.

### Validation Schema

<details>

<summary>Brand Styles Validation Schema</summary>

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Brand Management Styles",
  "type": "object",
  "definitions": {
    "liSpacing": {
      "type": "string",
      "pattern": "^\\d+px$",
      "description": "The liSpacing is a string that represents spacing in pixels with no upper limit."
    },
    "liIndent": {
      "type": "string",
      "pattern": "^\\d+px$",
      "description": "The liIndent is a string that represents spacing in pixels with no upper limit."
    },
    "listType": {
      "type": "string",
      "enum": [
        "ul",
        "ol"
      ],
      "description": "The list type can be 'ul' or 'ol'"
    },
    "listStylePosition": {
      "type": "string",
      "enum": [
        "inside"
      ],
      "description": "The list style position can only be 'inside'."
    },
    "listStyleType": {
      "type": "string",
      "enum": [
        "circle",
        "square",
        "disc",
        "lower-alpha",
        "upper-alpha",
        "lower-roman",
        "upper-roman",
        "revert",
        "auto"
      ],
      "description": "The list style type can be 'revert', 'upper-roman','lower-roman', 'circle', 'square', 'disc', 'upper-alpha', 'lower-alpha' or 'auto'."
    },
    "startList": {
      "type": "string",
      "pattern": "^(100|[1-9][0-9]?|1)$",
      "description": "The startList can be any integer from 1 to 100."
    },
    "textInput": {
      "type": "string",
      "description": "A general text input value.",
      "maxLength": 255
    },
    "target": {
      "type": "string",
      "description": "Specifies where to open the linked URL. Typically used in web development for anchor tags.",
      "enum": [
        "_blank",
        "_self",
        "_parent",
        "_top"
      ]
    },
    "alt": {
      "type": "string",
      "description": "Alternative text for the image, typically used for accessibility."
    },
    "href": {
      "type": "string",
      "description": "URL that the image links to when clicked.",
      "pattern": "^(http|https)://"
    },
    "src": {
      "type": "string",
      "description": "Source URL of the image.",
      "pattern": "^(http|https)://"
    },
    "foregroundColor": {
      "type": "string",
      "description": "Foreground color as hexadecimal value.",
      "examples": [
        "#000000",
        "#FFFFFF",
        "#FF5733"
      ],
      "pattern": "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$"
    },
    "backgroundColor": {
      "type": "string",
      "description": "Background color as hexadecimal value or 'transparent'.",
      "examples": [
        "#000000",
        "#FFFFFF",
        "#FF5733",
        "transparent"
      ],
      "pattern": "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$|^transparent$"
    },
    "backgroundImage": {
      "type": "string",
      "description": "Source URL of the image.",
      "pattern": "^url\\('(http|https)://[^']+'\\)$"
    },
    "backgroundPosition": {
      "type": "string",
      "enum": [
        "top left",
        "top center"
      ],
      "description": "Background position."
    },
    "backgroundRepeat": {
      "type": "string",
      "enum": [
        "no-repeat",
        "repeat"
      ],
      "description": "Does the backaground repeat?"
    },
    "backgroundSize": {
      "type": "string",
      "enum": [
        "cover",
        "auto",
        "none"
      ],
      "description": "The size of the backaground."
    },
    "height": {
      "type": "string",
      "description": "Height of the image, usually in pixels (e.g., '50px').",
      "pattern": "^\\d+(px)?$"
    },
    "width": {
      "type": "string",
      "description": "Width in pixels (e.g., '50px').",
      "pattern": "^(\\d+(px|%)|auto)?$"
    },
    "autoWidth": {
      "type": "string",
      "description": "Width in pixels (e.g., '50px'), percent, or 'auto'",
      "pattern": "^(\\d+(px|%)|auto)?$"
    },
    "maxWidth": {
      "type": "string",
      "description": "Width in pixels (e.g., '50px') or percent.",
      "pattern": "^(\\d+(px|%)|auto)?$"
    },
    "color": {
      "type": "string",
      "description": "Text color as hexadecimal value.",
      "examples": [
        "#000000",
        "#FFFFFF",
        "#FF5733"
      ],
      "pattern": "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$"
    },
    "letterSpacing": {
      "type": "string",
      "pattern": "^(\\d|[0-9]\\d)px$",
      "description": "The letter spacing can be between 0px and 99px."
    },
    "direction": {
      "type": "string",
      "enum": [
        "ltr",
        "rtl"
      ],
      "description": "The text direction can be either 'ltr' (left-to-right) or 'rtl' (right-to-left)."
    },
    "lineHeight": {
      "type": "string",
      "enum": [
        "120%",
        "150%",
        "180%",
        "200%"
      ],
      "description": "The line height can be 120%, 150%, 180%, or 200%."
    },
    "hideContentOnMobile": {
      "type": "boolean",
      "description": "Determines if content can be seen on mobile. If true, the content will be hidden on mobile devices."
    },
    "textAlign": {
      "type": "string",
      "enum": [
        "left",
        "right",
        "center"
      ],
      "description": "The text alignment can be left, right, or center."
    },
    "align": {
      "type": "string",
      "enum": [
        "left",
        "right",
        "center"
      ],
      "description": "The alignment can be left, right, or center."
    },
    "fontSize": {
      "type": "string",
      "description": "The font size as pixels",
      "examples": [
        "18px",
        "24px",
        "32px"
      ]
    },
    "fontFamily": {
      "type": "string",
      "description": "The font family",
      "examples": [
        "Arial, Helvetica, sans-serif",
        "Tahoma, Verdana, sans-serif",
        "\"Courier New\", Courier, monospace"
      ]
    },
    "fontWeight": {
      "type": "string",
      "enum": [
        "",
        "100",
        "200",
        "300",
        "400",
        "500",
        "600",
        "700",
        "800",
        "900"
      ],
      "description": "The font weight can be values from 100 to 900 in increments of 100."
    },
    "linkColor": {
      "type": "string",
      "description": "Link color as hexadecimal value.",
      "examples": [
        "#000000",
        "#FFFFFF",
        "#FF5733"
      ],
      "pattern": "^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$"
    },
    "paddingValue": {
      "type": "string",
      "pattern": "^(0|[1-5]?\\d|60)px$",
      "description": "Padding can be between 0px and 60px."
    },
    "borderValue": {
      "type": "string",
      "description": "A border value.",
      "pattern": "^(\\d+px)|(dotted|dashed|solid|double|groove|ridge|inset|outset)|(#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})|transparent)$",
      "maxLength": 50
    },
    "borderBottom": {
      "$ref": "#/definitions/borderValue"
    },
    "borderLeft": {
      "$ref": "#/definitions/borderValue"
    },
    "borderRight": {
      "$ref": "#/definitions/borderValue"
    },
    "borderTop": {
      "$ref": "#/definitions/borderValue"
    },
    "borderRadius": {
      "type": "string",
      "pattern": "^(0|[1-5]?\\d|60)px$",
      "description": "Border radius value can be between 0px and 60px."
    },
    "blockOptions": {
      "type": "object",
      "properties": {
        "paddingTop": {
          "$ref": "#/definitions/paddingValue"
        },
        "paddingRight": {
          "$ref": "#/definitions/paddingValue"
        },
        "paddingBottom": {
          "$ref": "#/definitions/paddingValue"
        },
        "paddingLeft": {
          "$ref": "#/definitions/paddingValue"
        },
        "align": {
          "$ref": "#/definitions/align"
        },
        "hideContentOnMobile": {
          "$ref": "#/definitions/hideContentOnMobile"
        }
      }
    },
    "mobileStyles": {
      "type": "object",
      "properties": {
        "paddingTop": {
          "$ref": "#/definitions/paddingValue"
        },
        "paddingRight": {
          "$ref": "#/definitions/paddingValue"
        },
        "paddingBottom": {
          "$ref": "#/definitions/paddingValue"
        },
        "paddingLeft": {
          "$ref": "#/definitions/paddingValue"
        },
        "textAlign": {
          "$ref": "#/definitions/textAlign"
        },
        "align": {
          "$ref": "#/definitions/align"
        },
        "fontSize": {
          "$ref": "#/definitions/fontSize"
        }
      }
    },
    "className": {
      "type": "string",
      "description": "Used to target styles at a specific class."
    },
    "buttonStyles": {
      "type": "object",
      "properties": {
        "className": {
          "$ref": "#/definitions/className"
        },
        "label": {
          "$ref": "#/definitions/textInput"
        },
        "href": {
          "$ref": "#/definitions/href"
        },
        "width": {
          "$ref": "#/definitions/autoWidth"
        },
        "styles": {
          "type": "object",
          "properties": {
            "color": {
              "$ref": "#/definitions/color"
            },
            "fontSize": {
              "$ref": "#/definitions/fontSize"
            },
            "fontFamily": {
              "$ref": "#/definitions/fontFamily"
            },
            "fontWeight": {
              "$ref": "#/definitions/fontWeight"
            },
            "backgroundColor": {
              "$ref": "#/definitions/backgroundColor"
            },
            "borderBottom": {
              "$ref": "#/definitions/borderValue"
            },
            "borderTop": {
              "$ref": "#/definitions/borderValue"
            },
            "borderLeft": {
              "$ref": "#/definitions/borderValue"
            },
            "borderRight": {
              "$ref": "#/definitions/borderValue"
            },
            "lineHeight": {
              "$ref": "#/definitions/lineHeight"
            },
            "maxWidth": {
              "$ref": "#/definitions/maxWidth"
            },
            "paddingTop": {
              "$ref": "#/definitions/paddingValue"
            },
            "paddingRight": {
              "$ref": "#/definitions/paddingValue"
            },
            "paddingBottom": {
              "$ref": "#/definitions/paddingValue"
            },
            "paddingLeft": {
              "$ref": "#/definitions/paddingValue"
            }
          }
        },
        "blockOptions": {
          "$ref": "#/definitions/blockOptions"
        },
        "mobileStyles": {
          "$ref": "#/definitions/mobileStyles"
        }
      }
    },
    "imageStyles": {
      "type": "object",
      "properties": {
        "className": {
          "$ref": "#/definitions/className"
        },
        "alt": {
          "$ref": "#/definitions/alt"
        },
        "href": {
          "$ref": "#/definitions/href"
        },
        "src": {
          "$ref": "#/definitions/src"
        },
        "width": {
          "$ref": "#/definitions/width"
        },
        "blockOptions": {
          "$ref": "#/definitions/blockOptions"
        },
        "mobileStyles": {
          "$ref": "#/definitions/mobileStyles"
        }
      }
    },
    "rowStyles": {
      "type": "object",
      "properties": {
        "className": {
          "$ref": "#/definitions/className"
        },
        "styles": {
          "type": "object",
          "properties": {
            "color": {
              "$ref": "#/definitions/color"
            },
            "width": {
              "$ref": "#/definitions/width"
            },
            "backgroundColor": {
              "$ref": "#/definitions/backgroundColor"
            },
            "backgroundImage": {
              "$ref": "#/definitions/backgroundImage"
            },
            "backgroundPosition": {
              "$ref": "#/definitions/backgroundPosition"
            },
            "backgroundRepeat": {
              "$ref": "#/definitions/backgroundRepeat"
            },
            "backgroundSize": {
              "$ref": "#/definitions/backgroundSize"
            }
          }
        },
        "contentStyles": {
          "type": "object",
          "properties": {
            "backgroundColor": {
              "$ref": "#/definitions/backgroundColor"
            },
            "backgroundImage": {
              "$ref": "#/definitions/backgroundImage"
            },
            "backgroundPosition": {
              "$ref": "#/definitions/backgroundPosition"
            },
            "backgroundRepeat": {
              "$ref": "#/definitions/backgroundRepeat"
            },
            "backgroundSize": {
              "$ref": "#/definitions/backgroundSize"
            },
            "paddingTop": {
              "$ref": "#/definitions/paddingValue"
            },
            "paddingRight": {
              "$ref": "#/definitions/paddingValue"
            },
            "paddingBottom": {
              "$ref": "#/definitions/paddingValue"
            },
            "paddingLeft": {
              "$ref": "#/definitions/paddingValue"
            }
          }
        }
      }
    }
  },
  "properties": {
    "styles": {
      "type": "object",
      "properties": {
        "row": {
          "oneOf": [
            {
              "$ref": "#/definitions/rowStyles"
            },
            {
              "type": "array",
              "items": {
                "$ref": "#/definitions/rowStyles"
              }
            }
          ]
        },
        "logo": {
          "type": "object",
          "description": "module",
          "properties": {
            "alt": {
              "$ref": "#/definitions/alt"
            },
            "href": {
              "$ref": "#/definitions/href"
            },
            "src": {
              "$ref": "#/definitions/src"
            },
            "height": {
              "$ref": "#/definitions/height"
            },
            "width": {
              "$ref": "#/definitions/width"
            },
            "target": {
              "$ref": "#/definitions/target"
            }
          }
        },
        "title": {
          "type": "object",
          "description": "module",
          "properties": {
            "color": {
              "$ref": "#/definitions/color"
            },
            "fontSize": {
              "$ref": "#/definitions/fontSize"
            },
            "fontFamily": {
              "$ref": "#/definitions/fontFamily"
            },
            "fontWeight": {
              "$ref": "#/definitions/fontWeight"
            },
            "linkColor": {
              "$ref": "#/definitions/linkColor"
            },
            "lineHeight": {
              "$ref": "#/definitions/lineHeight"
            },
            "textAlign": {
              "$ref": "#/definitions/textAlign"
            },
            "direction": {
              "$ref": "#/definitions/direction"
            },
            "letterSpacing": {
              "$ref": "#/definitions/letterSpacing"
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "h1": {
          "$ref": "#/properties/styles/properties/title"
        },
        "h2": {
          "$ref": "#/properties/styles/properties/title"
        },
        "h3": {
          "$ref": "#/properties/styles/properties/title"
        },
        "h4": {
          "$ref": "#/properties/styles/properties/title"
        },
        "h5": {
          "$ref": "#/properties/styles/properties/title"
        },
        "h6": {
          "$ref": "#/properties/styles/properties/title"
        },
        "button": {
          "oneOf": [
            {
              "$ref": "#/definitions/buttonStyles"
            },
            {
              "type": "array",
              "items": {
                "$ref": "#/definitions/buttonStyles"
              }
            }
          ]
        },
        "image": {
          "oneOf": [
            {
              "$ref": "#/definitions/imageStyles"
            },
            {
              "type": "array",
              "items": {
                "$ref": "#/definitions/imageStyles"
              }
            }
          ]
        },
        "divider": {
          "type": "object",
          "description": "module",
          "properties": {
            "width": {
              "$ref": "#/definitions/maxWidth"
            },
            "line": {
              "$ref": "#/definitions/borderValue"
            },
            "align": {
              "$ref": "#/definitions/align"
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "social": {
          "type": "object",
          "description": "module",
          "properties": {
            "icons": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "type": {
                    "$ref": "#/definitions/textInput"
                  },
                  "name": {
                    "$ref": "#/definitions/textInput"
                  },
                  "image": {
                    "type": "object",
                    "properties": {
                      "prefix": {
                        "$ref": "#/definitions/textInput"
                      },
                      "alt": {
                        "$ref": "#/definitions/alt"
                      },
                      "src": {
                        "$ref": "#/definitions/src"
                      },
                      "title": {
                        "$ref": "#/definitions/textInput"
                      },
                      "href": {
                        "$ref": "#/definitions/href"
                      }
                    },
                    "required": [
                      "prefix",
                      "alt",
                      "src",
                      "title",
                      "href"
                    ]
                  },
                  "text": {
                    "type": "string"
                  }
                },
                "required": [
                  "type",
                  "name",
                  "image",
                  "text"
                ]
              }
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "dynamic": {
          "type": "object",
          "description": "module",
          "properties": {
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            }
          }
        },
        "video": {
          "type": "object",
          "description": "module",
          "properties": {
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "general": {
          "type": "object",
          "description": "module",
          "properties": {
            "backgroundColor": {
              "$ref": "#/definitions/backgroundColor"
            },
            "contentAreaBackgroundColor": {
              "$ref": "#/definitions/backgroundColor"
            },
            "contentAreaWidth": {
              "$ref": "#/definitions/width"
            },
            "defaultFont": {
              "$ref": "#/definitions/textInput"
            },
            "linkColor": {
              "$ref": "#/definitions/linkColor"
            }
          }
        },
        "form": {
          "type": "object",
          "description": "module",
          "properties": {
            "styles": {
              "type": "object",
              "properties": {
                "width": {
                  "$ref": "#/definitions/autoWidth"
                },
                "fontSize": {
                  "$ref": "#/definitions/fontSize"
                },
                "fontFamily": {
                  "$ref": "#/definitions/fontFamily"
                },
                "fontWeight": {
                  "$ref": "#/definitions/fontWeight"
                }
              }
            },
            "labelsOptions": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "lineHeight": {
                  "$ref": "#/definitions/lineHeight"
                },
                "fontWeight": {
                  "$ref": "#/definitions/fontWeight"
                },
                "fontStyle": {
                  "$ref": "#/definitions/textInput"
                },
                "align": {
                  "$ref": "#/definitions/align"
                },
                "position": {
                  "type": "string"
                },
                "letterSpacing": {
                  "$ref": "#/definitions/letterSpacing"
                },
                "minWidth": {
                  "type": "string"
                }
              }
            },
            "fieldsOptions": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "backgroundColor": {
                  "$ref": "#/definitions/backgroundColor"
                },
                "outlineColor": {
                  "$ref": "#/definitions/color"
                },
                "borderRadius": {
                  "$ref": "#/definitions/borderRadius"
                },
                "borderTop": {
                  "$ref": "#/definitions/borderValue"
                },
                "borderBottom": {
                  "$ref": "#/definitions/borderValue"
                },
                "borderLeft": {
                  "$ref": "#/definitions/borderValue"
                },
                "borderRight": {
                  "$ref": "#/definitions/borderValue"
                },
                "paddingTop": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingRight": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingBottom": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingLeft": {
                  "$ref": "#/definitions/paddingValue"
                }
              }
            },
            "buttonsOptions": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "backgroundColor": {
                  "$ref": "#/definitions/backgroundColor"
                },
                "borderRadius": {
                  "$ref": "#/definitions/borderRadius"
                },
                "borderTop": {
                  "$ref": "#/definitions/borderValue"
                },
                "borderBottom": {
                  "$ref": "#/definitions/borderValue"
                },
                "borderLeft": {
                  "$ref": "#/definitions/borderValue"
                },
                "borderRight": {
                  "$ref": "#/definitions/borderValue"
                },
                "lineHeight": {
                  "$ref": "#/definitions/lineHeight"
                },
                "align": {
                  "$ref": "#/definitions/align"
                },
                "width": {
                  "$ref": "#/definitions/width"
                },
                "maxWidth": {
                  "$ref": "#/definitions/maxWidth"
                },
                "paddingTop": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingRight": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingBottom": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingLeft": {
                  "$ref": "#/definitions/paddingValue"
                },
                "marginBottom": {
                  "type": "string"
                },
                "margingLeft": {
                  "type": "string"
                },
                "marginRight": {
                  "type": "string"
                },
                "marginTop": {
                  "type": "string"
                }
              }
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "icons": {
          "type": "object",
          "description": "module",
          "properties": {
            "items": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "image": {
                    "type": "string"
                  },
                  "textPosition": {
                    "type": "string"
                  },
                  "text": {
                    "$ref": "#/definitions/textInput"
                  },
                  "alt": {
                    "$ref": "#/definitions/alt"
                  },
                  "title": {
                    "type": "string"
                  },
                  "href": {
                    "$ref": "#/definitions/href"
                  },
                  "target": {
                    "$ref": "#/definitions/target"
                  },
                  "height": {
                    "$ref": "#/definitions/height"
                  },
                  "width": {
                    "$ref": "#/definitions/width"
                  }
                },
                "required": [
                  "image",
                  "textPosition",
                  "text",
                  "alt",
                  "title",
                  "href",
                  "target",
                  "height",
                  "width"
                ]
              }
            },
            "styles": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "fontSize": {
                  "$ref": "#/definitions/fontSize"
                },
                "fontFamily": {
                  "$ref": "#/definitions/fontFamily"
                },
                "fontWeight": {
                  "$ref": "#/definitions/fontWeight"
                }
              }
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "iconSpacing": {
              "type": "object",
              "properties": {
                "paddingTop": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingRight": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingBottom": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingLeft": {
                  "$ref": "#/definitions/paddingValue"
                }
              }
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "menu": {
          "type": "object",
          "description": "module",
          "properties": {
            "items": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "text": {
                    "$ref": "#/definitions/textInput"
                  },
                  "link": {
                    "type": "object",
                    "properties": {
                      "href": {
                        "$ref": "#/definitions/href"
                      },
                      "title": {
                        "$ref": "#/definitions/textInput"
                      },
                      "target": {
                        "$ref": "#/definitions/target"
                      }
                    },
                    "required": [
                      "href",
                      "title",
                      "target"
                    ]
                  }
                },
                "required": [
                  "text",
                  "link"
                ]
              }
            },
            "style": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "linkColor": {
                  "$ref": "#/definitions/linkColor"
                },
                "fontSize": {
                  "$ref": "#/definitions/fontSize"
                },
                "fontFamily": {
                  "$ref": "#/definitions/fontFamily"
                },
                "fontWeight": {
                  "$ref": "#/definitions/fontWeight"
                }
              }
            },
            "hamburger": {
              "type": "object",
              "properties": {
                "mobile": {
                  "type": "boolean"
                },
                "foregroundColor": {
                  "$ref": "#/definitions/foregroundColor"
                },
                "backgroundColor": {
                  "$ref": "#/definitions/backgroundColor"
                },
                "iconSize": {
                  "type": "string"
                },
                "iconType": {
                  "type": "string"
                }
              }
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "itemsSpacing": {
              "type": "object",
              "properties": {
                "paddingTop": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingRight": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingBottom": {
                  "$ref": "#/definitions/paddingValue"
                },
                "paddingLeft": {
                  "$ref": "#/definitions/paddingValue"
                }
              }
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "spacer": {
          "type": "object",
          "description": "module",
          "properties": {
            "height": {
              "$ref": "#/definitions/height"
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            }
          }
        },
        "paragraph": {
          "type": "object",
          "description": "module",
          "properties": {
            "styles": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "fontSize": {
                  "$ref": "#/definitions/fontSize"
                },
                "fontFamily": {
                  "$ref": "#/definitions/fontFamily"
                },
                "fontWeight": {
                  "$ref": "#/definitions/fontWeight"
                },
                "lineHeight": {
                  "$ref": "#/definitions/lineHeight"
                },
                "textAlign": {
                  "$ref": "#/definitions/textAlign"
                },
                "direction": {
                  "$ref": "#/definitions/direction"
                },
                "letterSpacing": {
                  "$ref": "#/definitions/letterSpacing"
                },
                "linkColor": {
                  "$ref": "#/definitions/linkColor"
                },
                "paragraphSpacing": {
                  "type": "string",
                  "pattern": "^\\d+px$",
                  "description": "The paragraph spacing is a string that represents spacing in pixels with no upper limit."
                }
              }
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "list": {
          "type": "object",
          "description": "module",
          "properties": {
            "styles": {
              "type": "object",
              "properties": {
                "color": {
                  "$ref": "#/definitions/color"
                },
                "fontSize": {
                  "$ref": "#/definitions/fontSize"
                },
                "fontFamily": {
                  "$ref": "#/definitions/fontFamily"
                },
                "fontWeight": {
                  "$ref": "#/definitions/fontWeight"
                },
                "lineHeight": {
                  "$ref": "#/definitions/lineHeight"
                },
                "textAlign": {
                  "$ref": "#/definitions/textAlign"
                },
                "direction": {
                  "$ref": "#/definitions/direction"
                },
                "letterSpacing": {
                  "$ref": "#/definitions/letterSpacing"
                },
                "linkColor": {
                  "$ref": "#/definitions/linkColor"
                },
                "liSpacing": {
                  "$ref": "#/definitions/liSpacing"
                },
                "liIndent": {
                  "$ref": "#/definitions/liIndent"
                },
                "listStylePosition": {
                  "$ref": "#/definitions/listStylePosition"
                },
                "listStyleType": {
                  "$ref": "#/definitions/listStyleType"
                },
                "startList": {
                  "$ref": "#/definitions/startList"
                }
              }
            },
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        },
        "carousel": {
          "type": "object",
          "description": "module",
          "properties": {
            "blockOptions": {
              "$ref": "#/definitions/blockOptions"
            },
            "mobileStyles": {
              "$ref": "#/definitions/mobileStyles"
            }
          }
        }
      }
    },
    "template": {
      "type": "object",
      "properties": {}
    },
    "row": {
      "type": "object",
      "properties": {}
    },
    "rows": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {}
      }
    }
  },
  "oneOf": [
    { "required": ["styles", "template"] },
    { "required": ["styles", "rows"] },
    { "required": ["styles", "row"] }
  ]
}
```

</details>
