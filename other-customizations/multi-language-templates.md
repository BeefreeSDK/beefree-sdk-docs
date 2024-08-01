# Multi-Language Templates

{% hint style="info" %}
Multi-language Templates are only available for Superpower and Enterprise plans.
{% endhint %}

## Overview

Multi-language Templates (MLT) empower your end users to design customized experiences for their international audiences. Through the use of this feature, your end users will be able to select one default language, and up to three translations reflected in the top bar of their builder. Keep in mind that Multi-language Templates provide you with a means to translate template content, but _does not_ automatically translate the content for you.

MLT provides a translation infrastructure. You can integrate translations into your application using one of the following two methods:

* Enable translations through the [Beefree SDK OpenAI AddOn](../builder-addons/addons/partner-addons/openai-addon/)
* Type the translations manually

**Note:** The style of your templates stays the same across the language version while MLT is in use. The only change that will occur is the language of the text for the relevant components.

This Configuration Guide will help you get started with configuring the MLT feature. We recommend you start with the [Prerequisites](multi-language-templates.md#prerequisites) section to ensure you have everything you need for a successful configuration.&#x20;

If you are uncertain if your host application is a good candidate for this functionality, continue to the [Is MLT for Your Application?](multi-language-templates.md#is-mlt-for-your-application) section to learn more about this feature.

### Is MLT for Your Application? <a href="#is-mlt-for-your-application" id="is-mlt-for-your-application"></a>

The Multi-language Templates (MLT) feature is an enhancement for companies working with end users who build emails that engage with international audiences.

MLT adds the following extended functionality to your host application:

* Add a new language for the content inside Beefree SDK
* Activate the language configuration in the [Beefree SDK configuration file](../getting-started/readme/installation/configuration-parameters/)
* Customize a list of languages the user can choose from
* Allow changes to the default language
* Enable preview for templates in different language versions

To use Multi-language Templates, your host application only needs to store one JSON file with the languages. For more information on this, visit the [Configuration Steps section](multi-language-templates.md#configuration-steps).

For more information on the end user experience for Multi-language Templates, visit our [Multi-language Templates white label end user documentation](https://docs.beefree.io/end-user-guide/multi-language-templates).

### End User Functionality <a href="#end-user-functionality" id="end-user-functionality"></a>

Multi-language Templates (MLT) offers the following in-app features for an application end user:

* Switching the editor and template languages
* Translate contents
  * View a list of eligible content in the [Translate Contents section of the Multi-language Knowledge Base Article](https://devportal.beefree.io/hc/en-us/articles/13704895899026).
* Multi-language Template preview
* Export HTML for multiple languages as single files
* Alternative text descriptions
* Changing an image path
  * This lets users switch email images for different translations. For instance, they can replace an image containing English text with the corresponding image containing Spanish text for the Spanish translation.&#x20;

For more detailed information on the MLT feature offering, visit our Multi-language Knowledge Base article.

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Before proceeding with the configuration, ensure you have:

* Superpower or Enterprise plans
* The multi-language support toggle set to on in the Beefree SDK Console
* Application Client ID
* Application Client secret

## Configuration Steps <a href="#configuration-steps" id="configuration-steps"></a>

To use Multi-language Templates, your host application only needs to store one JSON file with the different languages you’d like to offer. Take the following steps to configure Multi-language Templates (MLT) in your application.

Enable multi-language templates

1. Log in to the [Beefree SDK Console](https://developers.beefree.io/).
2. Click “Details” on the application you’d like to enable multi-language template for.
3. Select “Application configuration”.
4. Navigate to the multi-language template toggle.
5. Toggle the feature to on.

## Initialize multi-language templates

1. Add the `templateLanguage` property to the config object. This property defines the default language for the template.
2. Add the `templateLanguages` property to the config object. This property defines the list of language options for the template translations.
3. Confirm you added both properties with the correct language options and save your changes.&#x20;

The following example shows the properties within the config object. In this example, the languages are read and written from left to right.

**Note:** You can only choose languages that are written and read from left to right, or right to left. You cannot mix languages with different directions of reading and writing within the same JSON.&#x20;

```json

templateLanguage: { value: 'en-US', label: 'English' },
templateLanguages: [
  { value: 'es-ES', label: 'Español' },
  { value: 'de-DE', label: 'Deutsch' },
  { value: 'pt-BR', label: 'Português' },
],

```

The following sample shows an example of a default language and three translation languages that are written and read from right to left.

```json

  templateLanguage: { value: 'fa-IR', label: 'فارسی' },
  templateLanguages: [
    { value: 'ja-JP', label: '日本語' },
    { value: 'ar-SA', label: 'العربية' },
    { value: 'tr-TR', label: 'Türkçe' },
  ],

```

**Note:** You can have up to six different versions of the design using one template.

{% hint style="info" %}
Languages are defined with a value and a label. The label is what will be shown in the language drop-down inside the top bar. The value is a key that stores the translations in the JSON. It is used to set the corresponding language meta attribute for each translation.
{% endhint %}

## Lang Attribute <a href="#lang-attribute" id="lang-attribute"></a>

The lang attribute on the content modules helps with [hyphenation and screen readability](advanced-options/meta-tags.md).

## Test the Configuration <a href="#test-the-configuration" id="test-the-configuration"></a>

Once you have initialized multi-language templates, you can confirm that the configuration was successful by following these instructions:

1. Go to your builder.
2. Navigate to the top bar.
3. Confirm whether or not you see a language drop-down menu.

If you see a drop-down, the configuration was successful. If you do not see a drop-down, reference the following table for troubleshooting steps you can take.

| Issue                              | Description                                                                                                                                                             | Resolution                                                                                                           |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Improper JSON File Storage         | Make sure the JSON file with the desired languages is correctly stored in your application.                                                                             | Review the file location and ensure it’s accessible.                                                                 |
| Disabled Multi-Language Templates  | Double-check if the Multi-Language Templates feature is enabled in the Beefree SDK Console and set to “on.”                                                             | Enable the feature in the configuration settings.                                                                    |
| Incorrect Configuration Properties | Verify the correctness of the \`templateLanguage\` and \`templateLanguages\` properties in the config object.                                                           | Correct any syntax errors or misconfigurations in the properties.                                                    |
| Language Direction Mismatch        | Make certain that chosen languages follow the correct reading direction (left to right or right to left) and are defined with both value and label.                     | Ensure the languages are compatible with the chosen direction and follow the defined format.                         |
| Missing Language Drop-Down         | If the language drop-down is not visible, review the setup steps in the Configuration section.                                                                          | Revisit the configuration steps and check for any missing or incorrect settings.                                     |
| HTML Saving Errors                 | If encountering issues with saving or exporting HTML, check the \`bee.save\` method for language parameters and the \`onSave\` event listener in the configuration.     | Ensure proper usage of the \`bee.save\` method and validate the \`onSave\` event listener for any errors.            |
| Incorrect \`onSave\` Handling      | Ensure that the \`onSave\` callback correctly handles the HTML saving process for each language.                                                                        | Review and update the \`onSave\` callback to address language-specific HTML saving properly.                         |
| Translation Export Issues          | For exporting translations, validate that the defined languages are correctly represented in the array.                                                                 | Double-check the array of languages for accuracy and completeness.                                                   |
| Missing \`onSave\` Callbacks       | Implement \`onSave\` callbacks for each language to handle specific language-related data during export.                                                                | Create \`onSave\` callbacks for each language export to manage language-specific data appropriately.                 |
| Language Change Problems           | When changing the template language, verify the existence of the specified language, and have an \`onTemplateLanguageChange\` callback to respond to language switches. | Confirm the language’s availability and define an \`onTemplateLanguageChange\` callback to handle language switches. |

## Translation HTML

Multi-language Templates (MLT) offer the option to save and export translation HTML. This section outlines the steps you need to take to save or export a translation’s HTML.

### Save HTML

To save the HTML output for a specific language take the following steps:

1. Use the `bee.save` method and provide the desired language as a parameter. In this example, we’ll save it for the Italian language (‘it-IT’).

```javascript

bee.save({ language: 'it-IT' })

```

2. Set up an `onSave` event listener to handle the HTML saving process. This listener will be triggered when the HTML generation is complete. You can add it to the configuration object.

```javascript

bee.configure({
  onSave: (pageJson, pageHtml, ampHtml, templateVersion, language) => {
    myApi.saveHtml(pageHtml, language);
  }
});


```

In the code above:

* `onSave` is an event handler function that takes several parameters related to the generated HTML.
* `pageHtml` contains the generated HTML.
* language contains the requested language value, which was previously set in the `bee.save` method.

If you want to use the default main language for generating HTML when the `bee.save` method is called without parameters, you don’t need to specify a language in the `bee.save method`. The default language will be used automatically.

## Export Translations <a href="#export-translations" id="export-translations"></a>

Take the steps outlined in this section to export the translation HTML.

1. Define an array of languages that you want to export translations for. Each language should be represented as a string.

The following example shows an array of multiple export languages.

```javascript

const languages = ['en-US', 'es-ES', 'it-IT'];

```

2. Create a function, let’s call it `exportAllTranslations` as an example, which will iterate over the array of languages and call the `bee.save method` for each language.

View the following example function.

```javascript

function exportAllTranslations() {
  languages.forEach(language => bee.save({ language }));
}


```

3. Implement the `onSave` callbacks for each language. These callbacks will be triggered when the bee.save method completes for each language. Make sure to handle the specific language-related data within each callback.

```javascript

// onSave callback for en-US
1. onSave: (
  pageJson, pageHtml, ampHtml, templateVersion, language // en-US
) => {
  // Handle the export for en-US here
  // You can access pageHtml, ampHtml, and other data
  // related to the en-US language export
}

// onSave callback for es-ES
2. onSave: (
  pageJson, pageHtml, ampHtml, templateVersion, language // es-ES
) => {
  // Handle the export for es-ES here
  // You can access pageHtml, ampHtml, and other data
  // related to the es-ES language export
}

// onSave callback for it-IT
3. onSave: (
  pageJson, pageHtml, ampHtml, templateVersion, language // it-IT
) => {
  // Handle the export for it-IT here
  // You can access pageHtml, ampHtml, and other data
  // related to the it-IT language export
}

// Repeat the above pattern for each language in the array


```

To get HTML in a specific language by our [CSAPI](../apis/content-services-api/content-services-api-reference.md#html), ensure you include a “language” key/value pair to the body of your request.

The following sample code displays this:

```javascript

{
  beautifyHtmlEnabled: false,
  page: {...},
  language: "it-IT"
}

```

## Changing the Language <a href="#changing-the-language" id="changing-the-language"></a>

Follow the steps outlined in this section to create a specified functionality that allows the end user to change their template language when a custom top bar is enabled.

1. Ensure you have a [custom top bar](../server-side-configurations/server-side-options/toolbar-options.md).
2. Create a function to handle the language change. You can use the instance method `bee.switchTemplateLanguage` for this purpose.

```javascript

bee.switchTemplateLanguage({ language: 'es-ES' })

```

3.  Verify if the specified language exists in the available languages. If it does, the language switch will happen automatically.

    **Note:** If the specified language _does not_ exist among the available languages, an event will be fired to the `onError` callback.
4. Once the language is successfully changed, a callback named `onTemplateLanguageChange` will be triggered.

You need to define this callback function to respond to the language change.

```javascript

onTemplateLanguageChange: (lang) => {
  console.log(lang) // Example output: { label: 'Spanish', value: 'es-ES', isMain: false }
}

```

The `onTemplateLanguageChange` callback will receive an object (lang) containing information about the language the user switched to. This object will have three properties:

* `label`: The label or name of the language.
* `value`: The value representing the language (e.g., ‘es-ES’ for Spanish).
* `isMain`: A boolean property indicating whether the selected language is the default one, as defined with `templateLanguage` in the configuration object.

5. Test the language switching functionality by calling `bee.switchTemplateLanguage` with different language values, and make sure that the `onTemplateLanguageChange` callback responds correctly.

## Triggering the Translation Preview <a href="#triggering-the-translation-preview" id="triggering-the-translation-preview"></a>

If you have a custom Preview, you can handle switching languages on the Preview.

To open the Preview, you can call either of two methods:

* &#x20;`bee.togglePreview`
* `bee.switchPreview`

The methods perform the following tasks:

* `togglePreview`: a toggle that opens and closes the Preview.
* `switchPreview`: accepts a parameter to specify the language and get the HTML preview. It also opens the Preview if it’s closed.

The following code shows an example of the methods applied for the default language.

```javascript

// Open the preview in the default language
bee.togglePreview() or bee.switchPreview()

// Switch to Italian
bee.switchPreview({ language: 'it-IT' })

// Close the preview
bee.togglePreview()

```

The following code shows an example of the methods applied for a preview in French.

```javascript

// Open the preview in French
bee.switchPreview({ language: 'fr-FR' })

// Switch to Russian
bee.switchPreview({ language: 'ru-RU' })

// Close the preview
bee.togglePreview()

```

**Note:** The language parameter is optional in `switchPreview`. Calling it without parameters will open the Preview with the default language selected. If the Preview is open, nothing will happen. The same behavior is applied when the language passed is not valid or doesn’t exist.

## Automating Translations <a href="#triggering-the-translation-preview" id="triggering-the-translation-preview"></a>

If you would like to provide your end users with the option to automatically translate all of the translatable content within their design, you can use the [DeepL addOn](../builder-addons/addons/partner-addons/deepl.md).&#x20;
