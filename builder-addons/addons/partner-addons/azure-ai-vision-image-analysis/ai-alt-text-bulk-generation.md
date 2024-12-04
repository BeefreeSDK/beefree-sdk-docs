---
description: >-
  Read this technical documentation to learn more about how to configure bulk
  Alt text generation with AI.
---

# AI Alt Text Bulk Generation

## Overview

Bulk Alt text Generation with AI is a feature that works as an extension to our existing [Alt-text generation with AI feature](https://docs.beefree.io/beefree-sdk/addons/partner-addons/openai-addon/alternate-text-generation-with-ai). The new functionality enables you to provide your end users with an easy method to create alt text captions across multiple image module types simultaneously using artificial intelligence. Through this feature, your application end users will be able to boost the accessibility of their content while also saving a significant amount of time.

{% hint style="info" %}
While this feature works for multiple image modules, it _does not_ work for dynamic images.
{% endhint %}

## Prerequisites

Prior to configuring this feature, ensure that you have the following:

* Superpowers or Enterprise account
* Enabled Azure Vision AddOn in your Developer Console

## Default Contents

If you have a default alt text set, the image won't be included among the ones that need an AI-generated alt text. If you have a default value set in your `defaultContents`, this will require the end user to delete the default text before being able to generate the new alt text with AI. To avoid this behavior, and for this feature to work best, we recommend you do not set a default value for alt text in your `beeConfig`.

If you do have a default value set, you can delete it one of the following ways:

* Set the alt property as an empty string
* Delete the line of code from your `defaultContents`

The following code shows an example of the `alt` property within the `defaultContents`. In the scenario presented in the following code, we recommend deleting the Default `alt` value set within the `alt` property.

```javascript
var beeConfig = {
  ...,
  defaultContents: {
    ...,
    image: {
      alt: "Default alt value",
      // Add any other default properties as needed
    },
    // Add other default content settings if necessary
  },
  ...,
};
```

The following code shows an example of the `alt` property set as an empty string. This is how we recommend you set your code for this feature to work best.

```javascript
var beeConfig = {
  ...,
  defaultContents: {
    ...,
    image: {
      alt: "",
      // Add any other default properties as needed
    },
    // Add other default content settings if necessary
  },
  ...,
};
```

**Note:** You can still use the `defaultContents` `alt` value and the AI-generated Alt text in Bulk at the same time. However, it will require the end user to delete the default alt text prior to using the AI-generation tool for that particular image module.

## Configuration Steps

To configure Bulk Alt Text Generation with AI for your application, take the Configuration Steps outlined in our [Alternate Text Generation with AI documentation](https://docs.beefree.io/beefree-sdk/addons/partner-addons/openai-addon/alternate-text-generation-with-ai).

## Token Upselling Compatibility

AI Alt Text Generation in Bulk is compatible with [Token Upselling](https://docs.beefree.io/beefree-sdk/addons/partner-addons/openai-addon/token-upselling). Through Token Upselling, you can configure your application to verify that end users have enough tokens to generate alt-text for multiple images at once.&#x20;

The type of images they can create alt-text for are the following:

* Images
* Stickers
* Icons
* GIFs
* Custom AddOn Images

If they do not have sufficient image tokens in their account, you can redirect them to [purchase additional image tokens](../ai-writing-assistant/token-upselling.md) prior to performing the bulk generation. &#x20;

## Multi-Language Templates Compatibility

This feature is not compatible with Multi-language Templates, and is currently only available in English.

## Troubleshooting

If you experience any issues with setting up this AddOn, take the following measures to troubleshoot your configuration:

* Ensure your Azure API key is connected correctly within your Beefree SDK Developer Console. &#x20;
* Ensure your custom endpoint is set up correctly in the SDK console.
* Repeat the configuration steps outlined in [this document](alternate-text-generation-with-ai.md).&#x20;

## Additional Considerations

As you configure this feature, ensure you consider the following:

* You will be billed through your Microsoft Azure account for AI generation-related features. Ensure you [consult their billing page](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/computer-vision/) for details on pricing.
