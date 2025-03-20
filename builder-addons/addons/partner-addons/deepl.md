---
description: >-
  Automatically translate content for different language templates using the
  DeepL addOn.
---

# DeepL

{% hint style="info" %}
The DeepL AddOn is only available for [Superpowers](https://developers.beefree.io/pricing-plans) and [Enterprise](https://developers.beefree.io/pricing-plans) plans. Superpowers customers can add up to 6 translations per template. If you're on an Enterprise plan, you can add up to 20 translations.&#x20;
{% endhint %}

## MLT Automatic Bulk Translation with DeepL

The new [DeepL](https://www.deepl.com/en/translator) addOn available in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) empowers your end users to translate all the translatable content within their designs using the new translate button. This feature requires that you have [Multi-language templates](../../../other-customizations/multi-language-templates.md) configured for your application, and that you have a DeepL API key. Once you configure both within your host application, your end users will be able to automatically translate the translatable content within the additional language versions of their designs. If you are on the Superpowers plan, your end users can add up to 6 additional translations, and for Enterprise, your end users can add up to 20 additional translations. Visit the [Automatic Translations white label end user documentation](https://docs.beefree.io/end-user-guide/multi-language-templates/automatic-translations) to learn more about how this feature works for your application's end users.

The following content types qualify as translatable content:

| Modules and translatable properties                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Header Meta information                                                       |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| <ul><li><strong>Button</strong>: <code>label</code> - The text displayed on the button.</li><li><strong>Paragraph</strong>: <code>html</code> - The HTML content of the paragraph.</li><li><strong>Heading/Title</strong>: <code>text</code> - The textual content of the heading or title.</li><li><strong>List</strong>: <code>html</code> - The HTML content of the list.</li><li><strong>Image</strong>: <code>alt</code> - The alternative text for the image.</li><li><strong>Video</strong>: <code>thumbAlt</code> - The alternative text for the video's thumbnail.</li><li><strong>Icon</strong>: <code>text</code>, <code>alt</code>, <code>title</code> - The textual content, alternative text, and title of the icon.</li><li><strong>Menu</strong>: <code>text</code>, <code>title</code> - The textual content and title of the menu.</li></ul> | <ul><li>Title</li><li>Description</li><li>Subject</li><li>Preheader</li></ul> |

The HTML translatable property refers to the text within the HTML tags of the element itself. For the "Button" module, the translatable property is "label," which specifies the text displayed on the button. In the "Paragraph" module, the translatable property is "html," indicating the HTML content within the paragraph tags. For "Heading/Title," the property is "text," representing the textual content of the heading or title. The "List" module also uses "html," referring to the HTML content within the list tags. The "Image" module has the "alt" property, which provides alternative text for the image. In the "Video" module, "thumbAlt" denotes the alternative text for the video's thumbnail. The "Icon" module includes "text," "alt," and "title," covering the textual content, alternative text, and title of the icon, respectively. Lastly, the "Menu" module uses "text" and "title" for its textual content and title.

The following video shows a template with Heading, Paragraph, and List modules. When the **Translate** button is clicked, the text within the translatable properties for those modules are translated. The following section displays a JSON example with a translation in Spanish.

{% embed url="https://drive.google.com/file/d/1Z0FnlCE0DwvWUZMXnVeg66LFF4ow4YmU/view?usp=sharing" %}

### Example JSON Translation

<details>

<summary>Example JSON with Spanish Translation</summary>

In the following JSON, English is the primary language and Spanish is set as the translation language.

```json
{
  "page": {
    "body": {
      "container": {
        "style": {
          "background-color": "#FFFFFF"
        }
      },
      "content": {
        "computedStyle": {
          "linkColor": "#0068A5",
          "messageBackgroundColor": "transparent",
          "messageWidth": "500px"
        },
        "style": {
          "color": "#000000",
          "font-family": "Arial, Helvetica, sans-serif"
        },
        "type": "page-properties",
        "webFonts": []
      },
      "description": "Empty template for BEE",
      "head": {
        "meta": {
          "description": "Enjoy a heartwarming moment with your furry friends while savoring your morning coffee. Learn about life's lessons and the importance of hard work together.",
          "subject": "Morning Coffee Conversations with Pets",
          "title": "Morning Coffee Conversations with Pets",
          "translations": {
            "es-ES": {
              "title": "Café matinal Conversaciones con mascotas",
              "description": "Disfrute de un momento entrañable con sus amigos peludos mientras saborea su café matutino. Aprendan juntos las lecciones de la vida y la importancia del trabajo duro.",
              "subject": "Café matinal Conversaciones con mascotas"
            }
          }
        }
      },
      "language": {
        "label": "English",
        "value": "en-US"
      },
      "rows": [
        {
          "columns": [
            {
              "grid-columns": 12,
              "modules": [
                {
                  "descriptor": {
                    "computedStyle": {
                      "hideContentOnDesktop": false,
                      "hideContentOnMobile": false
                    },
                    "heading": {
                      "prompt": "00000000-0000-0000-0000-000000000000",
                      "style": {
                        "color": "#555555",
                        "direction": "ltr",
                        "font-family": "inherit",
                        "font-size": "23px",
                        "font-weight": "700",
                        "letter-spacing": "0px",
                        "line-height": "120%",
                        "link-color": "#E01253",
                        "text-align": "center"
                      },
                      "text": "Morning Coffee Conversations with Pets",
                      "title": "h1",
                      "translations": {
                        "es-ES": {
                          "text": "Café matinal Conversaciones con mascotas"
                        }
                      }
                    },
                    "style": {
                      "padding-bottom": "0px",
                      "padding-left": "0px",
                      "padding-right": "0px",
                      "padding-top": "0px",
                      "text-align": "center",
                      "width": "100%"
                    }
                  },
                  "locked": false,
                  "type": "newsletter-modules-heading",
                  "uuid": "11111111-1111-1111-1111-111111111111"
                },
                {
                  "descriptor": {
                    "computedStyle": {
                      "align": "center",
                      "hideContentOnMobile": false
                    },
                    "divider": {
                      "style": {
                        "border-top": "1px solid #BBBBBB",
                        "width": "100%"
                      }
                    },
                    "style": {
                      "padding-bottom": "10px",
                      "padding-left": "10px",
                      "padding-right": "10px",
                      "padding-top": "10px"
                    }
                  },
                  "locked": false,
                  "type": "newsletter-modules-divider",
                  "uuid": "22222222-2222-2222-2222-222222222222"
                },
                {
                  "descriptor": {
                    "computedStyle": {
                      "hideContentOnAmp": false,
                      "hideContentOnDesktop": false,
                      "hideContentOnHtml": false,
                      "hideContentOnMobile": false
                    },
                    "paragraph": {
                      "computedStyle": {
                        "linkColor": "#0068a5",
                        "paragraphSpacing": "16px"
                      },
                      "html": "<p>Once upon a time, a man sat at his kitchen table, enjoying his morning coffee as his two dogs and one cat gathered around him. With a warm cup in hand, he began to share with his furry companions the harsh reality of life after school. \"You see,\" he explained, \"we have to work every day to earn money so we can afford simple pleasures like pizza.\"</p>\n<p>The man's pets listened intently, their eyes filled with curiosity as he continued to elaborate on the importance of hard work and dedication. \"It may seem daunting at first,\" he reassured them, \"but with perseverance and a positive attitude, we can achieve our goals.\" The dogs wagged their tails in agreement, while the cat purred softly in approval.</p>\n<p>As the morning sun streamed through the windows, casting a warm glow over the kitchen, the man smiled at his beloved pets. \"Remember,\" he said affectionately, \"life is full of challenges, but as long as we stick together and work hard, we can enjoy the simple pleasures that make it all worthwhile.\" And with that heartwarming sentiment, they continued their morning ritual of coffee and conversation, grateful for each other's company.</p>",
                      "prompt": "33333333-3333-3333-3333-333333333333",
                      "style": {
                        "color": "#000000",
                        "direction": "ltr",
                        "font-family": "inherit",
                        "font-size": "14px",
                        "font-weight": "400",
                        "letter-spacing": "0px",
                        "line-height": "120%",
                        "text-align": "left"
                      },
                      "translations": {
                        "es-ES": {
                          "html": "<p>Érase una vez un hombre sentado a la mesa de su cocina, disfrutando de su café matutino mientras sus dos perros y un gato se reunían a su alrededor. Con una taza caliente en la mano, empezó a compartir con sus peludos compañeros la dura realidad de la vida después de la escuela. \"Veréis\", explicó, \"tenemos que trabajar todos los días para ganar dinero y poder permitirnos placeres sencillos como la pizza\"</p>\n<p>Las mascotas del hombre escuchaban atentamente, con los ojos llenos de curiosidad, mientras él seguía explicando la importancia del trabajo duro y la dedicación. \"Al principio puede parecer desalentador\", les tranquilizó, \"pero con perseverancia y una actitud positiva, podemos conseguir nuestros objetivos\" Los perros movieron la cola en señal de acuerdo, mientras el gato ronroneaba suavemente en señal de aprobación.</p>\n<p>Mientras el sol de la mañana se colaba por las ventanas, arrojando un cálido resplandor sobre la cocina, el hombre sonrió a sus queridas mascotas. \"Recordad\", les dijo cariñosamente, \"la vida está llena de retos, pero mientras permanezcamos unidos y trabajemos duro, podremos disfrutar de los placeres sencillos que hacen que todo merezca la pena\" Y con ese sentimiento reconfortante, continuaron su ritual matutino de café y conversación, agradecidos por la compañía mutua.</p>"
                        }
                      }
                    }
                  }
                }
              ]
            }
          ]
        }
      ]
    }
  }
}

```

</details>

## How to activate

This section discusses the prerequisites and steps you need to take to get started with this feature.

### Prerequisites

* Ensure the Multi-language templates feature is toggled on inside of the Developer Console.
*   [DeepL API key](https://www.deepl.com/en/pro)

    **Note:** DeepL offers a [free tier](https://www.deepl.com/en/pro) for their plans. You can obtain an [API key from DeepL](https://www.deepl.com/en/pro) for free to get started with this feature.

### Activate the addOn in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu)

Take the following steps to activate this feature:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you'd like install the addOn in.
3. Install the [DeepL](https://www.deepl.com/en/translator) addOn.
4. Provide the requested details.
5. Save your changes.

### Auto Translation Configuration Parameter

Activate this feature by adding the new [configuration parameter](https://docs.beefree.io/beefree-sdk/readme/installation/configuration-parameters) `templateLanguageAutoTranslation` and setting it to `true`.

The following code sample displays an example of the `templateLanguageAutoTranslation`, `templateLanguage`, and `templateLanguages` parameters.

```javascript
// Configuration for the bee plugin
// Configuration for the bee plugin
var beeConfig = {
  uid: 'fakeUid123',
  container: 'bee-plugin-container',
  templateLanguageAutoTranslation: true,
  templateLanguage: {
    value: 'en-US',
    label: 'English'
  },
  templateLanguages: [
    { value: 'it-IT', label: 'Italian' },
    { value: 'fr-FR', label: 'French' },
    { value: 'es-ES', label: 'Spanish' },
    { value: 'ru-RU', label: 'Russian' },
    { value: 'el-GR', label: 'Greek' },
    { value: 'hy-AM', label: 'Armenian' }
  ]
};
```

If you have a custom top bar in your application, take the following additional steps:

1. Describe how to translate a template:&#x20;
   1. `translateTemplate` → `bee.translateTemplate({ language: 'it-IT' })`
2. Describe how to reset a translation:
   1. `resetTemplateTranslation` → `bee.resetTemplateTranslation({ language: 'it-IT' })`

#### Translate a Template

A function to translate the template to a specified language using the Beefree SDK.

{% tabs %}
{% tab title="React" %}
React **Translate a Template** example

```jsx
import React from 'react'; // Importing React
import { bee } from 'bee-plugin'; // Importing the bee plugin

// Define a functional component
const TranslateTemplateButton = () => {
  // Function to translate the template to Italian
  const translateTemplate = () => {
    bee.translateTemplate({ language: 'it-IT' }); // Calling the translateTemplate function with Italian language code
  };

  // Returning a button that triggers the translateTemplate function when clicked
  return (
    <button onClick={translateTemplate}>
      Translate Template to Italian
    </button>
  );
};

export default TranslateTemplateButton; // Exporting the component
```
{% endtab %}

{% tab title="JavaScript" %}
JavaScript **Translate a Template** example

```javascript
// Function to translate the template to Italian
function translateTemplate() {
  bee.translateTemplate({ language: 'it-IT' }); // Calling the translateTemplate function with Italian language code
}

// Adding an event listener to the button with id 'translateButton'
// When the button is clicked, the translateTemplate function is triggered
document.getElementById('translateButton').addEventListener('click', translateTemplate);
```

HTML example

```html
<!-- Button that will translate the template to Italian when clicked -->
<button id="translateButton">Translate Template to Italian</button>
```
{% endtab %}
{% endtabs %}

#### Reset a Translation

A function to reset the translation of the template to its original state using Beefree SDK.

{% tabs %}
{% tab title="React " %}
React Reset a Translation example

```jsx
import React from 'react'; // Importing React
import { bee } from 'bee-plugin'; // Importing the bee plugin

// Define a functional component
const ResetTemplateTranslationButton = () => {
  // Function to reset the template translation to the original state
  const resetTemplateTranslation = () => {
    bee.resetTemplateTranslation({ language: 'it-IT' }); // Calling the resetTemplateTranslation function with Italian language code
  };

  // Returning a button that triggers the resetTemplateTranslation function when clicked
  return (
    <button onClick={resetTemplateTranslation}>
      Reset Template Translation
    </button>
  );
};

export default ResetTemplateTranslationButton; // Exporting the component
```
{% endtab %}

{% tab title="JavaScript" %}
**Reset a Translation** JavaScript example

```javascript
// Function to reset the template translation to the original state
function resetTemplateTranslation() {
  bee.resetTemplateTranslation({ language: 'it-IT' }); // Calling the resetTemplateTranslation function with Italian language code
}

// Adding an event listener to the button with id 'resetButton'
// When the button is clicked, the resetTemplateTranslation function is triggered
document.getElementById('resetButton').addEventListener('click', resetTemplateTranslation);
```

HTML example

```html
<!-- Button that will reset the template translation when clicked -->
<button id="resetButton">Reset Template Translation</button>
```
{% endtab %}
{% endtabs %}

## Error handling

If errors occur, `onWarning` or `onError` will be triggered. If the request completes successfully there’s no direct feedback.

The following errors are returned by the backend service when something goes wrong during the translation.

| Code | Message                | HTTP Status                     | Details                                                    |
| ---- | ---------------------- | ------------------------------- | ---------------------------------------------------------- |
| 6001 | Unauthorized           | 401                             |                                                            |
| 6050 | Generic Error          | 500                             |                                                            |
| 6100 | Bad Request            | 400                             | E.g. 'sourceLanguage' and 'targetLanguage' must be defined |
| 6150 | Validation Error       | 400                             | E.g. language X is not supported                           |
| 6200 | Bump service error     | \[error returned by the Bumper] | E.g. Error while computing the fields to translate         |
| 6250 | Bump service error     | 500                             | E.g. Error while applying the translation                  |
| 6350 | Provider service error | 500                             | \[error returned by DeepL]                                 |
