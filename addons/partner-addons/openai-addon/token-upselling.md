# Token Upselling

## Overview

The Token Upselling feature is a notification banner that you can integrate within your OpenAI AddOn. This notification banner informs your application end users of when their available tokens are running low and when they are completely out. Both notification banners display an option for the end user to purchase additional tokens. These notification banners support a healthy token management workflow, and help avoid any potential interruptions in the end user’s workflow through transparently informing them about their available tokens.

The following notification banner will appear to an end user when their tokens are running low. “Running low” is defined as when an end user has a remaining token balance equal to or less than 20 percent of their initial token count.

**Note:** You can edit the notification banner trigger to a remaining percentage other than the default 20 percent. Reference the Customize Notification Trigger to learn more about how to change this percentage.

The following notification will appear to an end user when they no longer have any remaining tokens. This is triggered when `tokenCounter` is greater than or equal to `tokensAvailable`. For reference, `tokenCounter` refers to the amount of tokens an end user has used since their initial token balance.\


<figure><img src="https://lh7-eu.googleusercontent.com/PGcgDNS5Wbuls8HY45OY6VUPQQ50unTxqJN5rDcUPx65o3wBOBvZ8Z5nbL0fKcjH6SPp2SfF7PES1l9w5RtAasUKKbEVjc7zeguXzSKy64zh41XqvfXD4-uwM8qV5N5CA5U9PLouu5o7DQYpAAejjMM" alt=""><figcaption></figcaption></figure>

The text inside the banner notifications is customizable. Reference the Customize Notification Banner Text section to learn more about customizing the notification banner text within your application.&#x20;

Read this article to learn more about configuring token upselling within your host application.

## Prerequisites

Prior to getting started with the configuration, ensure you have the following:

* Superpower or Enterprise plan
* An OpenAI AddOn within your application

## Configuration Steps

This section discusses the configuration steps you need to follow to integrate the Token Upselling feature into your web application.

To integrate the Token Upselling feature into your application, take the following steps:

1. [Enable Token Upselling](token-upselling.md#enable-token-upselling)
2. [Limit Usage](token-upselling.md#limit-usage)
3. [Content Dialog Config](token-upselling.md#content-dialog-config)
4. [Configure Resolve](token-upselling.md#configure-resolve)

### Enable Token Upselling

To enable Token Upselling, you need to pass your configuration code to the AI Integration AddOn within the Developer Console.

When you pass your code, ensure you define the following variables:

* `tokenCounter`: Counts how many tokens an end user has used in total
* `tokensAvailable`: Displays how many remaining tokens an end user had
* `isUpsellEnabled`: A boolean that confirms whether or not the Token Upsell feature is enabled

**Note:** If you do not provide `tokenCounter` and `tokensAvailable`, the end user will have unlimited access to the AI functionality within your application.

The purpose of the following code is to initialize and track the number of tokens available and the number of tokens used. It also checks if the upsell feature is enabled.

```javascript
 
 var tokenCounter = 0
  var tokensAvailable = 1000
  var isUpsellEnabled=true
  
```

### Limit Usage

When you define `tokensAvailable` and `tokenCounter,` you limit the end user’s token usage.

`isPromptDisabled` automatically disables the `ai-integration` when the number of tokens used by an end user (`tokenCounter`) is greater than or equal to the number of tokens available (`tokensAvailable`).

The following code displays an example of the AddOn AI Integration configuration code.

```javascript

addOns: [
      {
        id: "ai-integration",
        settings: {
          tokensAvailable: tokensAvailable,
          tokensUsed: tokenCounter,
          tokenLabel: 'tokens',
          isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
          isSuggestionsDisabled: false,
          isUpsellEnabled: isUpsellEnabled,
        }
      },
    ],

```

#### onInfo Callback

The purpose of the `onInfo` callback in the following code snippet is to handle information messages related to the usage of the `ai-integration` AddOn. It checks if the code of the `infoMessage` is 1000 and if the handle is `ai-integration`. If both conditions are met, it updates the AddOn settings and reloads the configuration.

```javascript
   // Watch for AddOn Usage
    onInfo: function (infoMessage) {

      if (infoMessage.code === 1000) {
        var handle = infoMessage.detail.handle

        if (handle === 'ai-integration') {
          var totalTokens = infoMessage.detail.usage.total_tokens
          tokenCounter = tokenCounter + totalTokens

          // Update AddOn Settings
          var newConfig = {
            addOns: [
              {
                id: "ai-integration",
                settings: {
                  tokensAvailable: tokensAvailable,
                  tokensUsed: tokenCounter,
                  tokenLabel: 'tokens',
                  isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
                  isUpsellEnabled:isUpsellEnabled
                }
              },
            ],
          }
          // Reload Config
          bee.loadConfig(newConfig)
        }
      }
    },

```

The code works by:

1. Retrieving the handle from the `infoMessage`.
2. Checking if the handle is `ai-integration`.
3. If the handle is `ai-integration`, retrieve the `totalTokens` from the `infoMessage`.
4. Updating the `tokenCounter` by adding the `totalTokens`.
5. Creating a `newConfig` object with the updated `tokenCounter` and other settings.
6. Reloading the configuration by calling `bee.loadConfig(newConfig)`.

#### Trigger the Handler Function

The purpose of the "upsell" action is to trigger the handler function, which, based on the following code sample, increases the number of tokens available by 1000 and returns an object with updated settings for the `ai-integration` add-on.

The handler function is a function that is executed when the `upsell` action is triggered. It has two parameters: `resolve` and `reject`. The `resolve` parameter is a function that is called when the handler function successfully completes its task, and the `reject` parameter is a function that is called when the handler function encounters an error or fails to complete its task.

```javascript
       upsell: {
          label: 'upsell',
          handler:(resolve, reject, args)=>{
            tokensAvailable+=1000
            resolve({
              addOns:[{
                  id: "ai-integration",
                  settings: {
                    tokensAvailable: tokensAvailable,
                    tokensUsed: tokenCounter,
                    tokenLabel: 'tokens',
                    isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
                    isUpsellEnabled:isUpsellEnabled
                    }}]
                  })
          }
        },

```

### Content Dialog Config

Configure the content dialog and upgrade path to enable the token upselling notification banner. This configuration is important because it defines the steps the end user takes to purchase more tokens.&#x20;

The following code displays an example of how to configure the content dialog.

<pre class="language-javascript"><code class="lang-javascript"><strong>
</strong><strong>contentDialog: {   
</strong>   upsell: {
          label: 'upsell',
          handler:(resolve, reject, args)=>{
            tokensAvailable+=1000
            resolve({
              addOns:[{
                  id: "ai-integration",
                  settings: {
                    tokensAvailable: tokensAvailable,
                    tokensUsed: tokenCounter,
                    tokenLabel: 'tokens',
                    isPromptDisabled: false,
                    isUpsellEnabled:isUpsellEnabled
                    }}]
                  })
          }
        },

</code></pre>

### Configure Resolve

Ensure you define how your host application will resolve the upsell feature. You can do this by returning the configuration on how to handle the content dialog within the addOn configuration. The code provided in the previous step displays an example of this.

## Settings, Data Types, and Defaults

The following table shows a list of what your web application can pass to the Beefree SDK in the addOn configuration of ai-integration.

<table><thead><tr><th width="259">Settings</th><th width="160">Data Types</th><th>Defaults</th></tr></thead><tbody><tr><td><code>tokenLabel</code></td><td>string</td><td>Default is “tokens”.</td></tr><tr><td><code>isPromptDisabled</code></td><td>boolean</td><td>Default is false. If changed to true, it can override tokens balance and disable the prompt.</td></tr><tr><td><code>isUpsellEnabled</code></td><td>boolean</td><td>Default is false. If changed to true, it enables the upsell.</td></tr><tr><td><code>tokensCounter</code></td><td>number</td><td>Tokens used, if not provided in the configuration, the user has unlimited tokens.</td></tr><tr><td><code>tokensAvailable</code></td><td>number</td><td>Tokens available to the end user. If not provided in the configuration, the user has unlimited tokens.</td></tr><tr><td><code>upsellTrigger</code></td><td>number</td><td>Default is 80 (%) of tokens available.</td></tr><tr><td><code>isSuggestionsDisabled</code></td><td>boolean</td><td>Default is false.</td></tr><tr><td><code>isRegenerateEnabled</code></td><td>boolean</td><td>Default is false.</td></tr></tbody></table>

## Disable the Regenerate Button

The regenerate button appears after an end user submits their first prompt to OpenAI through the OpenAI AddOn. This button enables the end user to resubmit the same prompt to OpenAI in order to receive a newly generated response. This is helpful when an end user may want a variety of prompt responses to select from. However, each regenerated response incurs additional token usage and costs. This section will discuss how to disable the regenerate button in the event you would like to remove it from your application’s user interface.

\
**Image 1.0** shows the regenerate button as an example at the bottom of an AI generated prompt response.

<figure><img src="https://lh7-eu.googleusercontent.com/fUEjs1x_kJKC8tDPOjqmrgJVCkXUTGxaa4Og91qGmzZsoYu5QItPV2l-5FAbcy_1v_z3sXhZgExzJhqzFxDdzVG5_iFPv_tsEVo_sFHjVXtoqWAKVeZdVzYiz3RK76XDTo3AExa8lafGyOJGTzVYw2w" alt="" width="563"><figcaption><p>Image 1.0: Regenerate button appears at the bottom of an AI generated prompt response</p></figcaption></figure>

To achieve this, configure the isRegenerateEnabled setting to false.

The following example displays the sample code for the regenerate button.

```javascript

// Configure AddOn Settings
addOns: [{
  id: "ai-integration",
  settings: {
    tokensAvailable: tokensAvailable,
    tokensUsed: tokenCounter,
    tokenLabel: 'tokens',
    isPromptDisabled: (tokenCounter >= tokensAvailable) ? true: false,
    isSuggestionsDisabled: false,
    isUpsellEnabled: isUpsellEnabled,
    isRegenerateEnabled: false,
    upsellTrigger: 90],
  },
}

```

## Customize Notification Banner Trigger

The default trigger for the upsell notification banner is when an end user has used 80% of their initial tokens, and only has 20% of their initial tokens available. These percentages are customizable based on your use case. You can edit the notification banner to trigger at any percentage of the initial token count that best works for your host application.

Take the following steps to customize your notification banner trigger:

1. Pass `upsellTrigger` to the initial AddOn configuration

```javascript

// Configure AddOn Settings
addOns: [{
  id: "ai-integration",
  settings: {
    tokensAvailable: tokensAvailable,
    tokensUsed: tokenCounter,
    tokenLabel: 'tokens',
    isPromptDisabled: (tokenCounter >= tokensAvailable) ? true: false,
    isSuggestionsDisabled: false,
    isUpsellEnabled: isUpsellEnabled,
    isRegenerateEnabled: false,
    upsellTrigger: 90],
  },
}

```

## Customize Notification Banner Text

This section discusses how you can customize the notification banner text. For reference, the notification banner has the following default message:

“You’re out tokens. Purchase more”

To edit the notification banner text, take the following steps:

1. **Identify the Template:** Locate the notification template you want to customize. In this example, the template is specified with a custom language ID: `` `bee-common-component-ai.no-token-message` ``.

```javascript
const notificationTemplateId = "bee-common-component-ai.no-token-message";
```

2. **Understand the Template:** Read and understand the original template text, which is "You're out of {tokenLabel}. {ctaLabel} to continue." This template includes two placeholders: `{tokenLabel}` and `{ctaLabel}`.

```javascript
const originalTemplate = "You're out of {tokenLabel}. {ctaLabel} to continue.";
```

3. **Understand the Default Behavior:** Understand that by default, the template includes a Call-to-Action (CTA) button represented by the `` `{ctaLabel}` `` placeholder.
4.  **Determine Your Customization Needs:** Decide what changes you want to make to the template.

    Options include:

    1. Removing the CTA button entirely.
    2. Changing the CTA button label.
    3. Reordering the text within the template.
5. **Create a Custom Language Entry:** If you want to customize the template, create a custom language entry. This entry should have the same custom language ID: `` `bee-common-component-ai.no-token-message` ``.

```javascript
/// Create a custom language entry with the same ID.
const customLanguageId = "bee-common-component-ai.no-token-message";
```

6. **Modify the Template:** Customize the template in your custom language entry according to your needs. For example:
   * To remove the CTA: "You're out of `{tokenLabel}`."
   * To change the CTA label: "You're out of `{tokenLabel}`. Click here to refill."

```javascript
// To remove the CTA:
const customTemplateWithoutCTA = "You're out of {tokenLabel}.";

// To change the CTA label:
const customTemplateWithCustomCTA = "You're out of {tokenLabel}. Click here to refill.";

```

7. **Implement the Custom Language Entry:** In your web application code, replace the default template with the custom language entry you've created. Ensure that you use the correct custom language ID when accessing the text.&#x20;

```javascript

// For the case without CTA
const notificationTextWithoutCTA = customLanguageEntries[customLanguageId];

// For the case with a custom CTA label
const notificationTextWithCustomCTA = customLanguageEntries[customLanguageId];

```

## Configure Image Tokens

You can also configure the Token Upselling feature to guide your application's end user to purchase images. Purchasing additional image tokens allows your end users to continue using features such as [Alt Text Generation with AI](../azure-ai-vision-image-analysis/alternate-text-generation-with-ai.md) and [Bulk Alt Text Generation](../azure-ai-vision-image-analysis/ai-alt-text-bulk-generation.md).

The following code shows an example of a Token Upselling configuration for both text and image tokens. Purchasing text tokens supports end users as they use features connected to the [OpenAI AddOn](./), and purchasing image tokens supports ends users as they use features connected to the [Azure AI Vision AddOn](../azure-ai-vision-image-analysis/).

```javascript
// AddOns configuration

addOns: [{
            id: "ai-integration",
            settings: {
                tokensAvailable: tokensAvailable,
                tokensUsed: tokenCounter,
                tokenLabel: 'tokens',
                isPromptDisabled: false,
                isSuggestionsDisabled: false,
                isUpsellEnabled: isUpsellEnabled,
            }
        },
        {
            id: "ai-alt-text",
            settings: {
                imagesAvailable: imagesAvailable,
                imagesUsed: imagesCounter,
                isPromptDisabled: (imagesCounter >= imagesAvailable) ? true : false,
                isUpsellEnabled: isUpsellEnabled,
            }
        },
    ],

    // onInfo callback

    onInfo: function(infoMessage) {

        if (infoMessage.code === 1000) {
            var handle = infoMessage.detail.handle
            if (handle === 'ai-integration') {
                var totalTokens = infoMessage.detail.usage.total_tokens
                tokenCounter = tokenCounter + totalTokens

                // Update AddOn Settings
                var newConfig = {
                    addOns: [{
                        id: "ai-integration",
                        settings: {
                            tokensAvailable: tokensAvailable,
                            tokensUsed: tokenCounter,
                            tokenLabel: 'tokens',
                            isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
                            isUpsellEnabled: isUpsellEnabled
                        }
                    }, ],
                }
                // Reload Config
                bee.loadConfig(newConfig)
            } else if (handle === 'ai-alt-text') {
                imagesCounter++
                const refreshedUsageSettings = {
                    addOns: [{
                        id: "ai-alt-text",
                        settings: {
                            imagesAvailable: imagesAvailable,
                            imagesUsed: imagesCounter,
                            isPromptDisabled: (imagesCounter >= imagesAvailable) ? true : false,
                            isUpsellEnabled: isUpsellEnabled,
                        }
                    }, ],
                }
                // Reload Config
                bee.loadConfig(refreshedUsageSettings)
            }
        }
    },

    // content dialog

    upsell: {
        label: 'upsell',
        handler: (resolve, reject, args) => {
                if (args.handle === 'ai-integration') {
                    tokensAvailable += 1000
                    resolve({
                        addOns: [{
                            id: "ai-integration",
                            settings: {
                                tokensAvailable: tokensAvailable,
                                tokensUsed: tokenCounter,
                                tokenLabel: 'tokens',
                                isPromptDisabled: false,
                                isUpsellEnabled: isUpsellEnabled
                            }
                        }]
                    })
                } else if (args.handle === 'ai-alt-text') {
                    imagesAvailable += 5
                    resolve({
                                addOns: [{
                                            id: "ai-alt
```

## Feature Limitations

This section discusses the Token Upselling feature limitations:

* Customization features only extend to the text within the notification banner, and are not available for the design of the notification banner.

## Billing

The only billing related to this feature is on OpenAI’s end with token purchasing through use of your OpenAI API key.

## Error Handling

This section discusses the error handling for token upselling. If an error occurs, end user’s will receive the following message:

“Something went wrong. Retry your request after a brief wait.”

The following image shows an example of how this message will appear within the user interface.

<figure><img src="https://lh7-eu.googleusercontent.com/m67ppiVwbfT5SWAW4dypinW-emI1oY0FIbnOGTZzn7Ww6zrKPlCRLAR7-kx4jhhshuqZqndqYgQGcxX70bCS0EyQs8zG0LYDoIN_HH0qPmxYaUXB3X3v1VM3KbLfRuMret6YfJtnhW7nq5CCSdOHR0M" alt=""><figcaption><p>Image 1.0 AI Prompt Request Error Message within the User Interface</p></figcaption></figure>

## Additional Considerations

For more information on how the Token Upselling feature will visually look to an end user within the user interface, visit the [OpenAI Feature Enhancements article](https://devportal.beefree.io/hc/en-us/articles/14935326915218-OpenAI-Feature-Enhancements).
