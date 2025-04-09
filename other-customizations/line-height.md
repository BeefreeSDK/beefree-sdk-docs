---
description: Learn more about how to enable and configure Line height for your end users.
---

# Line Height

{% hint style="info" %}
Line height is available for all Beefree SDK plan types, and for all builder types.
{% endhint %}

## Overview

Beefree SDK offers the option to custom the Line height for designs within the builder. This provides end users with greater control over typography and design. The Line height widget includes both preset values with clear indicators, and a custom input field for precise adjustments. This degree of control supports workflows that require consistent, accessible, and brand-compliant typography.

### Benefits

Line height includes the following benefits:

* **Clear Presets** – Easily select from predefined Line height values for quick adjustments.
* **Custom Input** – Enter exact Line height values (in percentage) for fine-tuned control.
* **Full Compatibility** – Works smoothly with co-editing, history tracking, and undo/redo functions.
* **CSS Customization** – Ensure brand consistency with advanced CSS styling options.

The following GIF displays an example of how your application's end users can utilize Line height throughout their content creation process.

<figure><img src="../.gitbook/assets/line height.gif" alt=""><figcaption></figcaption></figure>

## Prerequisites

Line height is available in the Beefree SDK builder by default. The only requirement is that you have the builder embedded with your application and can load it successfully.

## Advanced Permissions

You can use [Advanced Permissions](advanced-options/advanced-permissions.md) with Line height to show or hide the widget for the following module types:

* [Title](line-height.md#title)
* [Paragraph](line-height.md#paragraph)
* [List](line-height.md#list)
* [Button](line-height.md#button)
* [Table](line-height.md#table)
* [Form](line-height.md#form)

### Title

The following code snippet shows an example of how to set advanced permissions for Line height in the Title content block.

```javascript
const advancedPermissions = {
  content: {
    // Hides the widget in the title module
    title: {
      behaviors: {
        canViewSidebar: true,
      },
      properties: {
        lineHeight: {
          show: false,
          locked: false,
        },
      },
    },
  },
};
```

### Paragraph

The following code snippet shows an example of how to set advanced permissions for Line height in the Paragraph content block.&#x20;

```javascript
const advancedPermissions = {
  content: {
    // Locks the widget in for the Paragraph module while keeping it visible
    paragraph: {
      behaviors: {
        canViewSidebar: true,
      },
      properties: {
        lineHeight: {
          show: true,
          locked: true,
        },
      },
    },
  },
};
```

### List

The following code snippet shows an example of how to set advanced permissions for Line height in the List content block.

```javascript
const advancedPermissions = {
  content: {
    // Allows viewing the sidebar but hides the lineHeight property for lists
    list: {
      behaviors: {
        canViewSidebar: true,
      },
      properties: {
        lineHeight: {
          show: false,
          locked: false,
        },
      },
    },
  },
};

```

### Button

The following code snippet shows an example of how to set advanced permissions for Line height in the Button content block.&#x20;

```javascript
const advancedPermissions = {
  content: {
    // Locks the button widget but keeps it visible in the sidebar
    button: {
      behaviors: {
        canViewSidebar: true,
      },
      properties: {
        buttonLineHeight: {
          show: true,
          locked: true,
        },
      },
    },
  },
};

```

### Table

The following code snippet shows an example of how to set advanced permissions for Line height in the Table content block.&#x20;

```javascript
const advancedPermissions = {
  content: {
    // Hides the widget in the table module
    table: {
      behaviors: {
        canViewSidebar: false,
      },
      properties: {
        lineHeight: {
          show: false,
          locked: false,
        },
      },
    },
  },
};
```

### Form

The following code snippet shows an example of how to set advanced permissions for Line height in the Form content block.&#x20;

```javascript
const advancedPermissions = {
  content: {
    // Allows form block to be visible while locking properties
    form: {
      behaviors: {
        canViewSidebar: true,
      },
      properties: {
        labelLineHeight: {
          show: true,
          locked: true,
        },
      },
    },
  },
};
```

### Custom CSS Classes <a href="#custom-css-classes" id="custom-css-classes"></a>

You can use the following CSS classes to customize styles related to Line height on the Frontend of your application.

* `line-height-select--cs` for the select element
* `line-height-select-wrapper--cs` for the select element wrapper
* `line-height-custom-input-wrapper--cs` for the custom input wrapper
* `line-height-custom-input--cs` for the custom input element

### Customizable Labels <a href="#customizable-labels" id="customizable-labels"></a>

You can use customizable labels to override the default text for Line height in the Beefree SDK builder and add your own.&#x20;

* `bee-line-height-widget-custom-option` allows users to customize the label for the last option in the `Select` component. The default value is `Custom`.

```javascript
translations: {
  ...,
  "bee-line-height-widget-custom-option": "Other value", // Default is "Custom"
}
```

## Additional Consideration

Consider the following behaviors when using the Line height widget:

* The minimum value is 0.5.
* The maximum value is 3.
* When you select the **Custom** option from the Line height drop-down menu, you can click plus (+) or minus (-) to increase or decrease the Line height value. The Line height value will increase or decrease in increments of 0.1.
* If you manually type in a value with two numbers after the decimal, for example 0.57, the Line height will be rounded to the first number as the final value. So, the final value would be 0.6.&#x20;
