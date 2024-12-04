---
description: >-
  Learn how to connect your large language model (LLM) and create your own AI
  Writing Assistant with Beefree SDK.
---

# Custom AI Writing Assistant

{% hint style="info" %}
This AddOn is available on Beefree SDK [Enterprise](https://developers.beefree.io/pricing-plans) and VPC plans.
{% endhint %}

## Overview

The Custom AI Writing Assistant AddOn enables host applications to integrate their own LLM models with Beefree SDK. This allows host applications to provide their end users with advanced AI writing capabilities that are specific to their domains. Using the [Content Dialog](../../../other-customizations/advanced-options/content-dialog.md), this AddOn employs the same entry points as the [AI writing assistant](ai-writing-assistant/), allowing full control over the AI experience within your application. Once your Custom AI Writing Assistant AddOn is fully configured, the [Content Dialog](../../../other-customizations/advanced-options/content-dialog.md) displays the modal you created within the user interface when end users click the **Write with AI** button in the sidebar.&#x20;

This AddOn is compatible with the following modules:

* Title
* Paragraph
* List
* Button

With this AddOn, you can deliver a centralized assistant experience that caters to your specific application needs. By integrating your own LLM model, you reduce irrelevant content in AI-generated outputs and ensure consistency in how the AI generates content, all while aligning it with your brand’s voice and tone. This increased level of control helps increase AI adoption and usage across your customer base, because your end users are engaging with an AI tool that feels familiar and reliable.

Integrating your custom LLM also allows for continuous improvement, because the model can be trained and refined based on user feedback and real-world interactions. This results in more accurate suggestions, higher relevance, and greater user satisfaction, empowering your end users to create better content with minimal effort.

The following video displays an example of a [Content Dialog](../../../other-customizations/advanced-options/content-dialog.md) with a custom built user interface that is connected to the Custom AI Writing Assistant AddOn.

{% embed url="https://drive.google.com/file/d/1RQo5AwHK9SYLC6u9varViKoxYovHXI6a/view?t=4" %}

## Prerequisites

Prior to getting started with the configuration, ensure you have the following:

* Enterprise plan
* A custom LLM service to call from within the [Content Dialog](../../../other-customizations/advanced-options/content-dialog.md)
* Access to the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu)

## **Configuration Steps**

This section outlines the steps you need to take to integrate the Custom AI Writing Assistant AddOn into your web application.

These steps are the following:

1. [Install and enable the AddOn](custom-ai-writing-assistant.md#install-and-enable-the-addon)
2. [Configure the Content Dialog](custom-ai-writing-assistant.md#content-dialog-configuration)
3. [Manage Advanced Permissions](custom-ai-writing-assistant.md#advanced-permission-management)&#x20;

### **Install and Enable the AddOn**

Take the following steps to install and enable the AddOn:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Click on the **Details** button corresponding to the application you'd like to configure the AddOn for.
3. Go to the **AddOns** section and click **Browse AddOns**.
4. Search for and select the **Custom AI Writing Assistant** AddOn.
5. Once selected, click **Install**.
6. After installation, toggle the **Enable** button and save your changes.&#x20;

**Note:** You can revisit this page in the future by clicking **Edit** in the AddOn card to turn the AddOn on or off as needed.

{% hint style="warning" %}
Once you activate the **Custom AI Writing Assistant AddOn** with your own LLM, you cannot activate the [AI Writing Assistant AddOn](ai-writing-assistant/), which uses either OpenAI or Azure OpenAI models. Only one of these two AddOns can be active.&#x20;
{% endhint %}

### **Content Dialog Configuration**&#x20;

To use the Custom AI Writing Assistant AddOn, you need to configure the [Content Dialog](../../../other-customizations/advanced-options/content-dialog.md). This is important for defining how your custom LLM is called and how the response is handled.

The following code snippet displays an example configuration:

```javascript
contentDialog: {   
  customLLM: {
    label: 'Custom LLM',
    handler: (resolve, reject, args) => {
      resolve({ generatedText: `This is module ${args.moduleUUID}, I'm a ${args.moduleType} and my content was ${args.moduleContent}` })
    }
  }
},
```

1.  **Args Parameter Details** The `args` parameter contains the following:

    | Field           | Explanation                                                                                                         |
    | --------------- | ------------------------------------------------------------------------------------------------------------------- |
    | `moduleUUID`    | Unique identifier for the module                                                                                    |
    | `moduleType`    | Type of the module (e.g., TITLE, PARAGRAPH, LIST, BUTTON)                                                           |
    | `moduleContent` | Current content of the module unless it matches the default content. If it does, the value will be an empty string. |
2.  **Configure Resolve** The content dialog must resolve an object corresponding to this interface:

    ```typescript
    {
      generatedText: string
    }
    ```

    * **Handling Lists**: If you are working with a list, ensure the generated text separates each item with a line break. The text will then be split on each line break to construct the list in the stage. The syntax for a line breaks is `\n`.

### **Advanced Permission Management**&#x20;

You can control the visibility and state of the **Write with AI** button using [Advanced Permission](../../../other-customizations/advanced-options/advanced-permissions.md) settings. For example, disabling the AddOn will hide the button, while turning the button off will keep it visible but non-functional.

The following code snippet displays an example configuration for [Advanced Permissions](../../../other-customizations/advanced-options/advanced-permissions.md):

```javascript
addOns: [
  ...,
  {
    id: "custom-ai-integration",
    enabled: true,
    settings: {
      isButtonDisabled: false
    }
  },
]
```

#### **Disable the AddOn for Specific Blocks**

You can disable the Custom AI Writing Assistant for specific content blocks using [Advanced Permissions](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/advanced-permissions#addon). As a reminder, this AddOn is compatible with the following content blocks:

* [Button](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/advanced-permissions#button)
* [List](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/advanced-permissions#list)
* [Paragraph](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/advanced-permissions#paragraph)
* [Title](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/advanced-permissions#title)

&#x20;You can use [Advanced Permissions](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/advanced-permissions#addon) to disable access to a specific block using the following:

```typescript
aiIntegration: {
            locked: false,
            show: false
          }
```

To hide the AddOn for a specific module, the `show` property should be set to `false`.

## **Settings**

The table below outlines the settings available for the **ai-integration** AddOn in the Beefree SDK:

| Setting            | Data Type | Default | Description                                                   |
| ------------------ | --------- | ------- | ------------------------------------------------------------- |
| `enabled`          | boolean   | `true`  | If `false`, the “Write with AI” button is hidden              |
| `isButtonDisabled` | boolean   | `false` | If `true`, the “Write with AI” button is visible but disabled |

## **Edit the Button Label**

After your activate and configure this AddOn, a **Write with AI** button will appear to your application's end users for the applicable content blocks.

The following video displays how the **Write with AI** button inside the Content Properties once a content block is dragged and dropped onto the stage.&#x20;

{% embed url="https://drive.google.com/file/d/1THXsWzi0pzQPY97iuIC5aY3Zw3wHQDro/view?usp=sharing" %}

The following section provides an example of changing the Write with AI button text to "Generate copy". You can follow the same approach in the following example, but replace "Generate copy" with the text you'd like to use for your label.

### Edit Label Example

To change the "Write with AI" button label to "Generate copy" using the `mailup-bee-common-component-ai.config-label`, follow these steps:

1. **Set up the BeeFree SDK**: Initialize your `beeConfig` object as usual.
2. **Add the translations object**: In your `beeConfig`, include the `translations` object where you will specify the label override.
3. **Override the label**: Inside the `translations` object, add the `"mailup-bee-common-component-ai.config-label"` key and set its value to `"Generate copy"`.

```javascript
var beeConfig = {
    uid: config.uid,
    // additional configuration properties...
    translations: {
        "mailup-bee-common-component-ai.config-label": "Generate copy"
    },
    // other properties...
};
```

This will update the button text from "Write with AI" to "Generate copy."

## Additional Considerations

Consider the following when using the Custom AI Writing Assistant AddOn:

* You can reference the [AI Writing Assistant](ai-writing-assistant/) [End user documentation](https://docs.beefree.io/end-user-guide/ai-writing-assistant) as an example of how engaging with AI features looks like for end users.
* We are committed to maintaining the highest standards of security to protect your data at every level. For more information on our security practices, visit our [GDPR and Cybersecurity page](https://developers.beefree.io/gdpr-and-cybersecurity).
