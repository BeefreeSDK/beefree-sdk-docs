# Custom Languages

{% hint style="info" %}
You can choose one of [20+ languages](../../getting-started/readme/installation/configuration-parameters/) for the visual builder's UI when initializing the builder. If you want to use custom language strings, however, you will need to use a Custom Language. This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

## What are Custom Languages?

In Beefree SDK, Custom Languages allow you to accomplish two things:

* Translate the default text in the builder to your preferred language.
* Override the default text in the builder to your preferred text, even if you keep the same language.

Translating the default text in the builder is useful when you have diverse end users and you'd like to provide them with a builder experience that resonates with them.

Overriding the default text in the builder with your preferred text is useful when you want to customize the builder experience and apply your application's unique tone.

This page discusses how you can accomplish both use cases with Custom Languages. Keep in mind that you can utilize Custom Languages for overriding default text in the builder, even if you are not translating any of it to another language.

Before getting started, ensure you access and familiarize yourself with the [beefree-sdk-assets-languages](https://github.com/BeefreeSDK/beefree-sdk-assets-languages/tree/master) GitHub repository. This repository includes important JSON files for you to utilize to accomplish the steps outlined on this page.

{% hint style="warning" %}
**Important:** Familiarize yourself with the [beefree-sdk-assets-lanaguges GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-assets-languages/blob/master/en-US.json) prior to continuing into the steps.
{% endhint %}

## How to Use Custom Languages

This section includes two examples on how to use Custom Languages based on the above scenarios.

**Example One: Overriding Default Text**

In the [.en-US JSON file](https://github.com/BeefreeSDK/beefree-sdk-assets-languages/blob/master/en-US.json), you'll find the following section at the beginning:

```json
{
    "bee-common-top-bar": {
        "actions": "Actions",
        "help": "Help",
        "preview": "Preview",
        "save": "SAVE",
        "save-as-template": "Save as template",
        "show-structure": "Show structure",
    },
```

This JSON includes the default text in the builder, which you can see in the image of the Top bar below.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 19.24.48.png" alt=""><figcaption></figcaption></figure>

By adding the `translations` parameter to the `beeConfig` with the following configuration, the top bar can easily be customized.

```typescript
const beeConfig = {
  uid: config.uid,
  container: 'bee-plugin-container',
  translations: {
    'bee-common-top-bar': {
      'actions': 'Design Management',
      'send-test': 'Test your design',
      'help': 'Need support? Contact us.',
      'preview': 'View your masterpiece',
      'save': 'Save changes',
      'save-as-template': 'Download your design',
      'show-structure': 'Show outline',
    },
  },
```

The following image shows how this configuration appears in the builder.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 19.39.33.png" alt=""><figcaption></figcaption></figure>

**Example Two: Translating Default Text**

Translating the content to another language follows the same approach. The following configuration overrides the default text with the Spanish translation.

```typescript
const beeConfig = {
  uid: config.uid,
  container: 'bee-plugin-container',
  translations: {
    'bee-common-top-bar': {
      'actions': 'Acciones',
      'send-test': 'Enviar prueba',
      'help': 'Ayuda',
      'preview': 'Vista Previa',
      'save': 'GUARDAR',
      'save-as-template': 'Guardar como plantilla',
      'show-structure': 'Mostrar estructura',
    },
```

The following image shows the result of the configuration with the Spanish configuration.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 19.48.43.png" alt=""><figcaption></figcaption></figure>

## Using a Translation URL

You can override the default Beefree SDK language file by providing a URL to your own translations.  This is an advanced feature and will replace all languages used by the editor with the languages defined in the custom file.

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      translationsUrl: 'https://www.yourdomain.com/xx-XX.json',
      ...
}

```

## Using a JSON Object

The easiest method to override specific text labels is to [pass a JSON object in your `beeConfig`](../../getting-started/readme/installation/configuration-parameters/#passing-configurations-to-beefree-sdk), which contains the segments of the language file you want to override.

```javascript
var beeConfig = {
    uid: config.uid,
    // additional configuration properties...
    language: 'en-US',
    translations: {
        'bee-common-widget-bar': {
            content: 'MODULES',
        },
        // additional translations...
    },
    // other properties...
};
```

### **Additional Examples**&#x20;

Overriding the Help icon label in the default toolbar

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      translations: {
         "bee-common-top-bar": {
           help: "Support"
         },
      }
      ...
}

```

Overriding the Rows tab label in the sidebar

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      translations: {
          "bee-common-widget-bar": {
            "structure": "Catalog"
          }
        },
      }
      ...
}

```

Overriding the Preheader

```json
{
    "translations": {
        "bee-head-meta-preheader": {
            "name": "New Preheader",
            "placeholder": "New Enter Preheader"
        }
    }
}

```

Defining or adding a translation for "email"

The following code defines a translation object where the title for "bee-settings-details" is set to "New Email Details" specifically for the "email" field.

```json
translations: {
    "bee-settings-details": {
        "title": {
            "email": "New Email Details"
        }
    }
}
```

## Overriding AI Writing Assistant Default Text

You can override the default text for the [AI Writing Assistant](../../builder-addons/addons/partner-addons/ai-writing-assistant/#customize-prompt-suggestions). The following configuration sample includes the AI component and the various default text fields you can override.

```typescript
const beeConfig = {
  uid: config.uid,
  container: 'bee-plugin-container',
  translations: {
    'bee-common-top-bar': {
      'actions': 'Design Management',
      'send-test': 'Test your design',
      'help': 'Need support? Contact us.',
      'preview': 'View your masterpiece',
      'save': 'Save changes',
      'save-as-template': 'Download your design',
      'show-structure': 'Show outline',
    },
    'mailup-bee-common-component-ai': {
      'welcome-body-title': 'Welcome to Your Design Journey',
      'welcome-body-subtitle': 'Start creating stunning emails with ease.',
      'welcome-example': 'Example: Explore our templates to get inspired.',
      'welcome-heading-title': 'Craft Your Message',
      'welcome-heading-subtitle': 'Make every word count with our tools.',
      'welcome-heading-example': 'Example: Write a compelling subject line.',
      'welcome-list-title': 'Key Features to Explore',
      'welcome-list-subtitle': 'Discover what makes our editor unique.',
      'welcome-list-example': 'Example: Drag-and-drop functionality.',
      'welcome-button-title': 'Get Started Now',
      'welcome-button-subtitle': 'Click to begin your design adventure.',
      'welcome-button-example': 'Example: Create your first email.',
    },
  },
};
```

### Paragraph Block

The following image shows the results for the overwritten default text for AI Paragraph Assistant based on the above configuration.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 20.04.58.png" alt=""><figcaption></figcaption></figure>

### Title Block <a href="#sample-language-file" id="sample-language-file"></a>

The following image shows the results for the overwritten default text for AI Title Assistant based on the above configuration.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 20.06.10.png" alt=""><figcaption></figcaption></figure>

### List Block <a href="#sample-language-file" id="sample-language-file"></a>

The following image shows the results for the overwritten default text for AI List Assistant based on the above configuration.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 20.06.47.png" alt=""><figcaption></figcaption></figure>

### Button Block <a href="#sample-language-file" id="sample-language-file"></a>

The following image shows the results for the overwritten default text for AI Button Assistant based on the above configuration.

<figure><img src="../../.gitbook/assets/CleanShot 2025-01-27 at 20.07.15.png" alt=""><figcaption></figcaption></figure>

Reference the [Customize Prompt Suggestions section of the AI Writing Assistant page](https://docs.beefree.io/beefree-sdk/builder-addons/addons/partner-addons/ai-writing-assistant#customize-prompt-suggestions) for additional customization options and details.

## Confirmation Dialogs <a href="#sample-language-file" id="sample-language-file"></a>

The following section lists translations that correspond with Confirmation Dialogs for Rows, Columns, Modules, and the File Manager.&#x20;

### Delete Row <a href="#sample-language-file" id="sample-language-file"></a>

This list details the translations corresponding with the Delete Row Confirmation Dialog.

#### **Translations Variations**

* **Title:** 🆕 _Delete row_
  * `confirmation-dialogs.delete-row-confirmation-title`
* **Secondary Button:** 🆕 _Keep_
  * `confirmation-dialogs.keep-button`
* **Primary Button:** 🆕 _Delete_
  * `confirmation-dialogs.delete-button`

Reference the corresponding [classnames for Delete Row](../appearance/custom-css/change-log.md#delete-row-confirmation-dialog).

### Delete Column <a href="#sample-language-file" id="sample-language-file"></a>

This list details the translations corresponding with the Delete Column Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _Delete column_
  * `confirmation-dialogs.delete-column-confirmation-title`
* **Secondary Button:** 🆕 _Keep_
  * `confirmation-dialogs.keep-button`
* **Primary Button:** 🆕 _Delete_
  * `confirmation-dialogs.delete-button`

Reference the corresponding [classnames for Delete Column](../appearance/custom-css/change-log.md#delete-column-confirmation-dialog).

### Delete Module <a href="#sample-language-file" id="sample-language-file"></a>

This list details the translations corresponding with the Delete Module Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _Delete module_
  * `confirmation-dialogs.delete-module-confirmation-title`
* **Secondary Button:** 🆕 _Keep_
  * `confirmation-dialogs.keep-button`
* **Primary Button:** 🆕 _Delete_
  * `confirmation-dialogs.delete-button`

Reference the corresponding [classnames for Delete Module](../appearance/custom-css/change-log.md#delete-module-confirmation-dialog).&#x20;

### Hide Row on Mobile with Module Already Hidden on Desktop

This list details the translations corresponding with the Hide Row on Mobile Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _Hide row_
  * `confirmation-dialogs.hide-row-confirmation-title`
* **Heading:** 🆕 _Are you sure you want to hide this?_
  * `confirmation-dialogs.hide-row-confirmation-heading`

Reference the corresponding classnames for [Hide Row on Mobile with Module Already Hidden on Desktop](../appearance/custom-css/change-log.md#hide-row-on-mobile-with-module-already-hidden-on-desktop).

### Remove Custom Display Condition <a href="#sample-language-file" id="sample-language-file"></a>

This list details the translations corresponding with the Remove Custom Display Condition Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _Delete display condition_
  * `confirmation-dialogs.delete-display-condition-confirmation-title`

Reference the corresponding classnames for [Remove Custom Display Condition](../appearance/custom-css/change-log.md#remove-custom-display-condition).

### Confirm Delete Single File <a href="#sample-language-file" id="sample-language-file"></a>

This list details the translations corresponding with the Confirm Delete Single File Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _Delete {filename}_
  * `confirmation-dialogs.delete-file-confirmation-title`
* **Secondary Button:** 🆕 _Keep_
  * `confirmation-dialogs.keep-button`
* **Primary Button:** 🆕 _Delete_
  * `confirmation-dialogs.delete-button`

Reference the corresponding classnames for [Confirm Delete Single File](../appearance/custom-css/change-log.md#confirm-delete-single-file).

### **Confirm Delete Multiple Files**

This list details the translations corresponding with the Confirm Delete Multiple Files Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _Delete {count} files_
  * `confirmation-dialogs.delete-files-confirmation-title`
* **Secondary Button:** 🆕 _Keep_
  * `confirmation-dialogs.keep-button`
* **Primary Button:** 🆕 _Delete_
  * `confirmation-dialogs.delete-button`

Reference the corresponding [classnames for Confirm Delete Multiple Files](../appearance/custom-css/change-log.md#confirm-delete-multiple-files).

### Confirm Update Existing File | Custom FSP <a href="#sample-language-file" id="sample-language-file"></a>

{% hint style="info" %}
**Note:** This section is relevant if both the [Custom FSP](../../server-side-configurations/server-side-options/storage-options/connect-your-file-storage-system.md) and `ConfirmOverwriteModalEnabled` are activate.
{% endhint %}

This list details the translations corresponding with the Confirm Update Existing File Confirmation Dialog.

**Text Updates:**

* **Title:** 🆕 _Replace {filename}_
  * `confirmation-dialogs.replace-file-confirmation-title`
* **Secondary Button:** 🆕 _Keep_
  * `confirmation-dialogs.keep-button`

Reference the corresponding [classnames for Confirm Update Existing File](../appearance/custom-css/change-log.md#confirm-upload-existing-file).

### Confirm Update Existing File <a href="#sample-language-file" id="sample-language-file"></a>

This list details the translations corresponding with the Update Existing File Confirmation Dialog.

**Translations Variations**

* **Title:** 🆕 _File {filename} already exists_
  * `confirmation-dialogs.file-already-exists-title`
* **Heading:** 🆕 _Do you want to replace or keep both files?_
  * `confirmation-dialogs.replace-file-confirmation-heading`

Reference the corresponding classnames: Not applicable.

### File Manager - Move File Replace Confirmation

This list details the translations corresponding with the Move File Replace Confirmation Dialog.

#### **Translations Variations**

* **Title:** 🆕 _File {filename} already exists_
  * `confirmation-dialogs.file-already-exists-title`
* **Heading:** 🆕 _Do you want to replace or keep both files?_
  * `confirmation-dialogs.replace-file-confirmation-heading`

Reference the corresponding classnames: Not applicable.

## Sample language file <a href="#sample-language-file" id="sample-language-file"></a>

Check out our Github repository for [starter language templates](https://dam.beefree.io/beecustomlanguages) in all supported languages.
