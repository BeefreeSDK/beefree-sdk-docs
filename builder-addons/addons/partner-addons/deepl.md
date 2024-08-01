---
description: >-
  Automatically translate content for different language templates using the
  DeepL addOn.
---

# DeepL

## MLT Automatic Bulk Translation with DeepL

The new [DeepL](https://www.deepl.com/en/translator) addOn available in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website\_menu) empowers your end users to translate all the translatable content within their designs using the new translate button. This feature requires that you have [Multi-language templates](../../../other-customizations/multi-language-templates.md) configured for your application, and that you have a DeepL API key. Once you configure both within your host application, your end users will be able to automatically translate the translatable content within the different language versions of their designs. Also, now your end users can have up to six different language versions of their designs. Visit the [Automatic Translations white label end user documentation](https://docs.beefree.io/end-user-guide/multi-language-templates/automatic-translations) to learn more about how this feature works for your application's end users.

The following content types qualify as translatable content:

| Modules (and translatable property)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Header Meta information                                                       |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| <ul><li><strong>Button</strong>: <code>label</code> - The text displayed on the button.</li><li><strong>Paragraph</strong>: <code>html</code> - The HTML content of the paragraph.</li><li><strong>Heading/Title</strong>: <code>text</code> - The textual content of the heading or title.</li><li><strong>List</strong>: <code>html</code> - The HTML content of the list.</li><li><strong>Image</strong>: <code>alt</code> - The alternative text for the image.</li><li><strong>Video</strong>: <code>thumbAlt</code> - The alternative text for the video's thumbnail.</li><li><strong>Icon</strong>: <code>text</code>, <code>alt</code>, <code>title</code> - The textual content, alternative text, and title of the icon.</li><li><strong>Menu</strong>: <code>text</code>, <code>title</code> - The textual content and title of the menu.</li></ul> | <ul><li>title</li><li>description</li><li>subject</li><li>preheader</li></ul> |

{% embed url="https://drive.google.com/file/d/1J0mi-SUwdo9mGnSm4-cs7rIxnqm3TgUR/view?usp=sharing" %}

## How to activate

This section discusses the prerequisites and steps you need to take to get started with this feature.

### Prerequisites

* Ensure the Multi-language templates feature is toggled on inside of the Developer Console.
*   [DeepL API key](https://www.deepl.com/en/pro)

    **Note:** DeepL offers a [free tier](https://www.deepl.com/en/pro) for their plans. You can obtain an [API key from DeepL](https://www.deepl.com/en/pro) for free to get started with this feature.

### Activate the addOn in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website\_menu)

Take the following steps to activate this feature:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website\_menu).
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
