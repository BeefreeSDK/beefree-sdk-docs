# Debugging the Beefree SDK Editor

## Overview

The `debug` parameter in the `beeConfig` is an optional object that enables internal debugging features within the Beefree SDK editor. It's designed to help developers inspect configurations, [translations](../../../../other-customizations/advanced-options/custom-languages.md), and [data structures](../../../../data-structures/getting-started.md) more easily during development.

### How to Use

You can pass the `debug` parameter directly in your `beeConfig` object when initializing the editor. Alternatively, you can set or update it live using the `loadConfig` method—no need to refresh the editor.

**Example (in `beeConfig`):**

```js
const beeConfig = {
  debug: {
    all: true,                 // Enables all debug features
    inspectJson: true,        // Shows an eye icon to inspect JSON data for rows/modules
    showTranslationKeys: true // Displays translation keys instead of localized strings
  }
};
```

**Set it live (no refresh needed):**

```js
beeInstance.loadConfig({
  debug: {
    all: true
  }
});
```

### Parameters

The `debug` parameter in the Beefree SDK configuration accepts the following parameters:

* **`all`** (`boolean`): Enables all available debug options (`inspectJson` and `showTranslationKeys`). Use this during heavy debugging sessions.
* **`inspectJson`** (`boolean`): Adds an eye icon in the [module/row](../../../../data-structures/getting-started.md) toolbar that allows you to inspect the specific JSON used for that element. Useful for understanding how your configuration is being rendered.
* **`showTranslationKeys`** (`boolean`): Replaces localized strings with their translation keys throughout the UI. This is especially helpful when debugging i18n issues or checking for missing [translations](../../../../other-customizations/advanced-options/custom-languages.md).

### When It's Useful

The debug parameter is particularly helpful in the following scenarios:

* You're troubleshooting UI rendering issues tied to configuration JSON.
* You need to inspect what exact data is being used for rows/modules.
* You're working on translations and want to ensure correct keys are being used.
