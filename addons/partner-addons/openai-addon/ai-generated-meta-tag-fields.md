---
description: >-
  How to enable AI-generated Titles and Descriptions for Page Builder, and
  Subject and Preheaders for Email Builder.
---

# AI-Generated Meta Tag Fields

Read this technical documentation to learn more about how to configure AI [generated titles, meta descriptions for pages, preheaders, and subject lines for emails](https://docs.beefree.io/beefree-sdk/advanced-options/meta-tags) within your host application.

### Overview

AI addresses common issues in crafting effective subject lines, pre-headers, and titles, such as vague messaging, lack of urgency, and limited personalization. By utilizing AI, users can generate compelling copy for email campaigns and landing pages. The key benefits include optimizing title formats for character count and mobile responsiveness, avoiding common mistakes, and expediting the copy creation process. This tool aims to enhance efficiency in marketing endeavors by providing a solution to errors commonly encountered in title and subject line composition. The feature is applicable to both Page and Email applications within the builder.

### Prerequisites

* Beefree SDK Superpowers or Enterprise plan subscription
* OpenAI API Key
* [Activated OpenAI AddOn](https://docs.beefree.io/beefree-sdk/addons/partner-addons/openai-addon) within your Beefree SDK Developer Console

### Activation Steps

Learn more about how activate this feature for email and page builder respectively.

#### Email Builder

To activate AI Generated Meta tag fields for your email builder application, take the following steps:

1. Sign into your [Beefree SDK Developer Console](https://developers.beefree.io/)
2. Navigate to your application’s settings
3. Toggle on Enable Subject - Meta tag
4. Toggle on Enable Preheader - Meta tag

#### Page Builder

To activate AI Generated Meta tag fields for your page builder application, take the following steps:

1. Sign into your [Beefree SDK Developer Console](https://developers.beefree.io/)
2. Navigate to your application’s settings
3. Toggle on Enable Title - Meta tag
4. Toggle on Enable Description - Meta tag&#x20;

### Configuration Steps

This section outlines the steps for configuring this feature within your host application.

To configure AI Generated meta tag fields within your host application, take the following steps:

1. Enable the “`ai-integration`” AddOn
2. Add the `metadataGeneration` parameter
3. Set the parameter to `true` is your configuration code

The following code displays an example of the enabled feature.

```javascript
addOns: 
[{
    id: "ai-integration",
    settings: {
        tokensAvailable: tokensAvailable,
        tokensUsed: tokenCounter,
        tokenLabel: 'tokens',
        isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
        isSuggestionsDisabled: false,
        isUpsellEnabled: true,
        metadataGeneration: true  // Enabled by default
    }
}, ],
```

### Disable AI Generated Meta Tag Fields

To disable the AI Generated Metadata feature, set `metadataGeneration` to `false` in your code.

The following code sample displays the disabled feature.

```javascript
addOns: [{
    id: "ai-integration",
    settings: {
        tokensAvailable: tokensAvailable,
        tokensUsed: tokenCounter,
        tokenLabel: 'tokens',
        isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
        isSuggestionsDisabled: false,
        isUpsellEnabled: true,
        metadataGeneration: false
    }
}, ]
```

### Multi-Language Templates Compatibility

AI Generated Titles, Descriptions, Preheaders, and Subject Lines is compatible with Multi-language templates.

To use both Multi-language templates and AI-Generated Titles, Descriptions, Preheaders, and Subject Lines, take the following steps:

1. Perform the Multi-language Configuration Steps
2. Perform the AI-Generated Titles, Descriptions, Preheaders, and Subject Lines Configuration steps
3. Test the AI-generated content in a few different languages
4. Confirm everything works as intended

### Troubleshooting

If AI-driven generation fails, check the OpenAI AddOn configuration. Ensure your OpenAI API key is working properly, and that the AddOn is configured correctly within your Beefree SDK developer Console.

### Additional Considerations

* Customers will be billed through their OpenAI accounts for AI generation-related features. This is done through connecting their OpenAI API key in the Beefree SDK Developer Console.\
