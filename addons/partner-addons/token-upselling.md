# Token Upselling

1. [Overview](broken-reference)
2. [Prerequisites](broken-reference)
3. [Configuration Steps](broken-reference)
4. [Enable Token Upselling](broken-reference)
5. [Limit Usage](broken-reference)
6. [onInfo Callback](broken-reference)
7. [Trigger the Handler Function](broken-reference)
8. [Content Dialog Config](broken-reference)
9. [Configure Resolve](broken-reference)
10. [Settings, Data Types, and Defaults](broken-reference)
11. [Disable the Regenerate Button](broken-reference)
12. [Customize Notification Banner Trigger](broken-reference)
13. [Customize Notification Banner Text](broken-reference)
14. [Feature Limitations](broken-reference)
15. [Billing](broken-reference)
16. [Error Handling](broken-reference)
17. [Additional Considerations](broken-reference)

### Overview <a href="#overview" id="overview"></a>

The Token Upselling feature is a notification banner that you can integrate within your OpenAI AddOn. This notification banner informs your application end users of when their available tokens are running low and when they are completely out. Both notification banners display an option for the end user to purchase additional tokens. These notification banners support a healthy token management workflow, and help avoid any potential interruptions in the end user’s workflow through transparently informing them about their available tokens.

The following notification banner will appear to an end user when their tokens are running low. “Running low” is defined as when an end user has a remaining token balance equal to or less than 20 percent of their initial token count.

Note: You can edit the notification banner trigger to a remaining percentage other than the default 20 percent. Reference the [Customize Notification Trigger](https://docs.beefree.io/?page\_id=8256\&preview=true#customize-notification-banner-trigger) to learn more about how to change this percentage.

The following notification will appear to an end user when they no longer have any remaining tokens. This is triggered when tokenCounter is greater than or equal to tokensAvailable. For reference, tokenCounter refers to the amount of tokens an end user has used since their initial token balance.\


![Token Upselling notification banner that appears to the end user. The notification banner displays the message "You're out of tokens. Purchase more" The lower-right hand side of the image displays the tokens used out of total available tokens.](https://docs.beefree.io/wp-content/uploads/2023/11/CleanShot-2023-11-07-at-14.36.22.png)

Image 1: Token Upselling Notification Banner

The text inside the banner notifications is customizable. Reference the [Customize Notification Banner Text section](https://docs.beefree.io/?page\_id=8256\&preview=true#customize-notification-banner-text) to learn more about customizing the notification banner text within your application.&#x20;

Read this article to learn more about configuring token upselling within your host application.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Prior to getting started with the configuration, ensure you have the following:

* Superpower or Enterprise plan
* An OpenAI AddOn within your application

### Configuration Steps <a href="#configuration-steps" id="configuration-steps"></a>

This section discusses the configuration steps you need to follow to integrate the Token Upselling feature into your web application.

To integrate the Token Upselling feature into your application, take the following steps:

1. [Enable Token Upselling](https://docs.beefree.io/?page\_id=8256\&preview=true#enable-token-upselling)
2. [Limit Usage](https://docs.beefree.io/?page\_id=8256\&preview=true#limit-usage)
3. [Content Dialog Config](https://docs.beefree.io/?page\_id=8256\&preview=true#content-dialog-config)
4. [Configure Resolve](https://docs.beefree.io/?page\_id=8256\&preview=true#configure-resolve)

#### Enable Token Upselling <a href="#enable-token-upselling" id="enable-token-upselling"></a>

To enable Token Upselling, you need to pass your configuration code to the AI Integration AddOn within the Developer Console.

When you pass your code, ensure you define the following variables:

* tokenCounter: Counts how many tokens an end user has used in total
* tokensAvailable: Displays how many remaining tokens an end user had
* isUpsellEnabled: A boolean that confirms whether or not the Token Upsell feature is enabled

Note: If you do not provide tokenCounter and tokensAvailable, the end user will have unlimited access to the AI functionality within your application.

The purpose of the following code is to initialize and track the number of tokens available and the number of tokens used. It also checks if the upsell feature is enabled.

```

 var tokenCounter = 0
  var tokensAvailable = 1000
  var isUpsellEnabled=true

```

#### Limit Usage <a href="#limit-usage" id="limit-usage"></a>

When you define tokensAvailable and tokenCounter, you limit the end user’s token usage.

isPromptDisabled automatically disables the ai-integration when the number of tokens used by an end user (tokenCounter) is greater than or equal to the number of tokens available (tokensAvailable).

The following code displays an example of the AddOn AI Integration configuration code.

```

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

**onInfo Callback**

The purpose of the onInfo callback in the following code snippet is to handle information messages related to the usage of the ai-integration AddOn. It checks if the code of the infoMessage is 1000 and if the handle is “ai-integration”. If both conditions are met, it updates the AddOn settings and reloads the configuration.

```

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

1. Retrieving the handle from the infoMessage.
2. Checking if the handle is ‘ai-integration’.
3. If the handle is ‘ai-integration’, retrieving the totalTokens from the infoMessage.
4. Updating the tokenCounter by adding the totalTokens.
5. Creating a newConfig object with the updated tokenCounter and other settings.
6. Reloading the configuration by calling bee.loadConfig(newConfig).

**Trigger the Handler Function**

The purpose of the “upsell” action is to trigger the handler function, which, based on the following code sample, increases the number of tokens available by 1000 and returns an object with updated settings for the “ai-integration” add-on.

The handler function is a function that is executed when the “upsell” action is triggered. It has two parameters: resolve and reject. The resolve parameter is a function that is called when the handler function successfully completes its task, and the reject parameter is a function that is called when the handler function encounters an error or fails to complete its task.

```

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

#### Content Dialog Config <a href="#content-dialog-config" id="content-dialog-config"></a>

Configure the content dialog and upgrade path to enable the token upselling notification banner. This configuration is important because it defines the steps the end user takes to purchase more tokens.&#x20;

The following code displays an example of how to configure the content dialog.

```

contentDialog: {   
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
                    isPromptDisabled: false,
                    isUpsellEnabled:isUpsellEnabled
                    }}]
                  })
          }
        },

```

#### Configure Resolve <a href="#configure-resolve" id="configure-resolve"></a>

Ensure you define how your host application will resolve the upsell feature. You can do this by returning the configuration on how to handle the content dialog within the addOn configuration. The code provided in the previous step displays an example of this.

### Settings, Data Types, and Defaults <a href="#settings-data-types-and-defaults" id="settings-data-types-and-defaults"></a>

The following table shows a list of what your web application can pass to the Beefree SDK in the addOn configuration of ai-integration.

| Settings              | Data Type | Defaults                                                                                               |
| --------------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| tokenLabel            | string    | Default is “tokens”.                                                                                   |
| isPromptDisabled      | boolean   | Default is false. If changed to true, it can override tokens balance and disable the prompt.           |
| isUpsellEnabled       | boolean   | Default is false. If changed to true, it enables the upsell.                                           |
| tokensCounter         | number    | Tokens used, if not provided in the configuration, the user has unlimited tokens.                      |
| tokensAvailable       | number    | Tokens available to the end user. If not provided in the configuration, the user has unlimited tokens. |
| upsellTrigger         | number    | Default is 80 (%) of tokens available.                                                                 |
| isSuggestionsDisabled | boolean   | Default is false.                                                                                      |
| isRegenerateEnabled   | boolean   | Default is false.                                                                                      |

### Disable the Regenerate Button <a href="#disable-the-regenerate-button" id="disable-the-regenerate-button"></a>

The regenerate button appears after an end user submits their first prompt to OpenAI through the OpenAI AddOn. This button enables the end user to resubmit the same prompt to OpenAI in order to receive a newly generated response. This is helpful when an end user may want a variety of prompt responses to select from. However, each regenerated response incurs additional token usage and costs. This section will discuss how to disable the regenerate button in the event you would like to remove it from your application’s user interface.

Image 1.0 shows the regenerate button as an example at the bottom of an AI generated prompt response.

![Regenerate button appears at the bottom of an AI generated prompt response](https://docs.beefree.io/wp-content/uploads/2023/11/CleanShot-2023-11-07-at-14.58.35.png)

Image 2: Regenerate button appears at the bottom of an AI generated prompt response

To achieve this, configure the isRegenerateEnabled setting to false.

The following example displays the sample code for the regenerate button.

```

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
}]

```

The default trigger for the upsell notification banner is when an end user has used 80% of their initial tokens, and only has 20% of their initial tokens available. These percentages are customizable based on your use case. You can edit the notification banner to trigger at any percentage of the initial token count that best works for your host application.

Take the following steps to customize your notification banner trigger:

1. Pass upsellTrigger to the initial addOn configuration

```

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
}]

```

This section discusses how you can customize the notification banner text. For reference, the notification banner has the following default message:

“_You’re out tokens. Purchase more_”

To edit the notification banner text, take the following steps:

1\. Identify the Template: Locate the notification template you want to customize. In this example, the template is specified with a custom language ID: \`bee-common-component-ai.no-token-message\`.

```

const notificationTemplateId = "bee-common-component-ai.no-token-message";

```

2\. Understand the Template: Read and understand the original template text, which is “You’re out of {tokenLabel}. {ctaLabel} to continue.” This template includes two placeholders: \`{tokenLabel}\` and \`{ctaLabel}\`.

```

const originalTemplate = "You're out of {tokenLabel}. {ctaLabel} to continue.";

```

3. Understand the Default Behavior: Understand that by default, the template includes a Call-to-Action (CTA) button represented by the \`{ctaLabel}\` placeholder.
4. Determine Your Customization Needs: Decide what changes you want to make to the template.&#x20;

Options include:

* Removing the CTA button entirely.
* Changing the CTA button label.
* Reordering the text within the template.

5\. Create a Custom Language Entry: If you want to customize the template, create a custom language entry. This entry should have the same custom language ID: \`bee-common-component-ai.no-token-message\`.

```

// Create a custom language entry with the same ID.
const customLanguageId = "bee-common-component-ai.no-token-message";

```

6. Modify the Template: Customize the template in your custom language entry according to your needs. For example:

* To remove the CTA: “You’re out of {tokenLabel}.”
* To change the CTA label: “You’re out of {tokenLabel}. Click here to refill.”

```

// To remove the CTA:
const customTemplateWithoutCTA = "You're out of {tokenLabel}.";

// To change the CTA label:
const customTemplateWithCustomCTA = "You're out of {tokenLabel}. Click here to refill.";

```

7\. Implement the Custom Language Entry: In your web application code, replace the default template with the custom language entry you’ve created. Ensure that you use the correct custom language ID when accessing the text.

```

// For the case without CTA
const notificationTextWithoutCTA = customLanguageEntries[customLanguageId];

// For the case with a custom CTA label
const notificationTextWithCustomCTA = customLanguageEntries[customLanguageId];

```

### Feature Limitations <a href="#feature-limitations" id="feature-limitations"></a>

This section discusses the Token Upselling feature limitations:

* Customization features only extend to the text within the notification banner, and are _not_ available for the design of the notification banner.

### Billing <a href="#billing" id="billing"></a>

The only billing related to this feature is on OpenAI’s end with token purchasing through use of your OpenAI API key.

### Error Handling <a href="#error-handling" id="error-handling"></a>

This section discusses the error handling for token upselling. If an error occurs, end user’s will receive the following message:

“_Something went wrong. Retry your request after a brief wait._”

The following image shows an example of how this message will appear within the user interface.

![AI Prompt Request Error Message within the User Interface](https://docs.beefree.io/wp-content/uploads/2023/11/CleanShot-2023-11-07-at-15.07.13.png)

Image 3: AI Prompt Request Error Message within the User Interface

### Additional Considerations <a href="#additional-considerations" id="additional-considerations"></a>

For more information on how the Token Upselling feature will visually look to an end user within the user interface, visit the [OpenAI Feature Enhancements article](https://devportal.beefree.io/hc/en-us/articles/14935326915218/).
