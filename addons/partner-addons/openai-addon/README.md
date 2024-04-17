# OpenAI AddOn

## Overview <a href="#overview" id="overview"></a>

The OpenAI AddOn is fully functional from the moment it’s enabled via the [Beefree SDK Console](https://developers.beefree.io/). For information about enabling OpenAI AddOn [click here](https://devportal.beefree.io/hc/en-us/articles/10838757053330-How-do-I-enable-the-OpenAI-AddOn-).

Once enabled, the OpenAI AddOn is available in the side panel for the following content blocks:

* Title
* Paragraph
* List
* Button

In certain scenarios, you may find the need to personalize both the user interface (UI) and the operational features of the OpenAI AddOn. This is particularly applicable when you want to achieve objectives such as:

1. **Monitoring Token Usage for Cost Management:** By tracking the number of tokens being used, you can effectively manage and regulate your expenses related to using the OpenAI AddOn. This becomes important when your usage is high, and you must keep a budget check. [Learn more about tokens.](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)
2. **Controlling Access to the Prompt:** You might want to limit who can access and manipulate the prompt. In a shared environment, for instance, you may want to restrict certain users from altering the prompt, which is crucial for maintaining consistency and avoiding unwanted changes.
3. **Enabling Per User or Per Content Type:** You might want to limit who can access the AI so you can up-sell the feature to end-users. Or, you may only want to enable the AI capability for specific content types, such as paragraphs vs. buttons.
4. **Disabling Automatic Suggestions:** The OpenAI AddOn can generate automatic suggestions at the prompt, which may not always be desirable. In such cases, you might want to disable this feature to have more control over the input and output at the prompt.

We’ll cover all of these scenarios in the following sections as we discuss the settings and configuration options available for developers.

## General Settings <a href="#general-settings" id="general-settings"></a>

Note: All settings are _optional_ and may be refreshed, in real-time, via the [configuration reload](../../../readme/installation/configuration-parameters/configuration-reload.md) instance method (e.g. `bee.loadConfig(settings)`) during the active session.

Currently, the following settings are supported:

<table><thead><tr><th>Setting</th><th width="249.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>tokensAvailable</code></td><td>number</td><td>Display only value for the optional <a href="./">Display Usage Widget</a>: The total tokens available for the user to consume during the session. If provided, <code>tokensUsed</code> and <code>tokenLabel</code> are required.</td></tr><tr><td><code>tokensUsed</code></td><td>number</td><td>Display only value for the optional <a href="./">Display Usage Widget</a>: The number of tokens that the addon user has consumed during the current session. If provided, <code>tokensAvailable</code> and <code>tokenLabel</code> are required.</td></tr><tr><td><code>tokenLabel</code></td><td>string</td><td>Display only value for the optional <a href="./">Display Usage Widget</a>: The API reports token usage, but the host app may refer to tokens as words or any other nomenclature that makes sense to its users. Required when providing usage limits via <code>tokensAvailable</code> and <code>tokensUsed</code> parameters.</td></tr><tr><td><code>isPromptDisabled</code></td><td>boolean</td><td>Set to true to lock the prompt. The chat interface will be disabled but allow previous answers to be applied.</td></tr><tr><td><code>isSuggestionsDisabled</code>  </td><td>boolean</td><td>Set to true to hide the suggestions popup. Set this to <code>false</code> to disable the prompt presets. </td></tr><tr><td><code>isUpsellEnabled</code>  </td><td>boolean</td><td>A boolean that confirms whether or not the <a href="token-upselling.md">Token Upsell</a> feature is enabled.</td></tr><tr><td><code>metadataGeneration</code></td><td>boolean</td><td>A boolean that confirms whether or not the <a href="ai-generated-meta-tag-fields.md">AI-Generated Meta Tag fields feature</a> is enabled</td></tr></tbody></table>

### Example

```javascript
const beeConfig = {
    uid: 'string',  // Unique identifier for the user
    ... 
    addOns: [
      {
        id: "ai-integration",  // Identifier for the AI integration add-on
        settings: {
          tokensAvailable: tokensAvailable,  // Total tokens available for user consumption during the session
          tokensUsed: tokenCounter,  // Number of tokens consumed by the user during the current session
          tokenLabel: 'tokens',  // Label for the token usage, customizable by the host app
          isPromptDisabled: false,  // Whether to lock the prompt interface
          isSuggestionsDisabled: false,  // Use to remove prompt presets, decide whether to hide the suggestions popup 
          isUpsellEnabled: true,  // Whether Token Upsell feature is enabled
          metadataGeneration: true  // Whether AI-Generated Meta Tag fields feature is enabled (enabled by default)
        }
      },
    ],
    ...
}
```

## Monitor Usage <a href="#monitor-usage" id="monitor-usage"></a>

With each prompt response, the addon will report the usage data provided by the OpenAI API via the editor’s `onInfo` callback without storing or tracking the data.

### Example

```javascript

const beeConfig = {
    uid: 'string',
    ... 
    onInfo: function (data) {

        // Check information is addon
        if (data.code === 1000) {

            // Check which addon
            const handle = data.detail.handle
            if (handle === 'ai-integration') {
                // Get the total tokens
                const totalTokens = data.detail.usage.total_tokens
                // Update running total in database
                // --> host app code goes here
            }
        }
    },
    ...
}
     
```

## Display Usage Widget

You may choose to track the end-user’s total usage through the aforementioned `onInfo` callback if desired. Additionally, you may choose to show the usage data to the user via the built-in display widget. To activate the display usage widget, provide the usage data via the addon settings.  Since the editor doesn’t track usage, you’ll need to refresh the values via the `bee.loadConfig` method to keep the display widget data current.

### Example

```javascript

let tokenCounter = 0
let tokensAvailable = 2000

const beeConfig = {
    uid: 'string',
    ...
    // Initial AddOn configuration
    addOns: [
      {
        id: "ai-integration",
        settings: {
          tokensAvailable: tokensAvailable,
          tokensUsed: tokenCounter,
          tokenLabel: 'words',
          isPromptDisabled: false,
        }
      },
    ],
    ...
    // Monitor for information
    onInfo: function (data) {

        // Check information code is 1000 for addon reporting
        if (data.code === 1000) {

            // Check which addon
            const handle = data.detail.handle
            if (handle === 'ai-integration') {
                const totalTokens = data.detail.usage.total_tokens
                tokenCounter = tokenCounter + totalTokens

                // Refresh Usage AddOn Settings
                const refreshedUsageSettings = {
                    addOns: [
                        {
                            id: "ai-integration",
                            settings: {
                                tokensAvailable: tokensAvailable,
                                tokensUsed: tokenCounter,
                                tokenLabel: 'tokens',
                                isPromptDisabled: (tokenCounter >= tokensAvailable) ? true : false,
                            }
                        },
                    ],
                }

                // Reload Config
                bee.loadConfig(refreshedUsageSettings)
            }
        }
    },
}

```

See below for an example of how the UI will render when provided with the optional display usage widget.

<figure><img src="../../../.gitbook/assets/06e76ffc-23fc-46da-b433-609cabc86a9f-1024x549.png" alt=""><figcaption></figcaption></figure>

## Disable Prompts Per User <a href="#disable-prompts-per-user" id="disable-prompts-per-user"></a>

To enable OpenAI AddOn, but disable the prompt per user, pass the `isPromptDisabled` boolean parameter as `true`.

The following example will **disable** the prompts for the user with an `uid` of `inactive-user`.

### Example

```json

const beeConfig = {
    uid: 'inactive-user',
    ... 
    addOns: [
      {
        id: "ai-integration",
        settings: {
          isPromptDisabled: true,
        }
      },
    ],
    ...
}
     
```

## Disable AddOn Per User <a href="#disable-addon-per-user" id="disable-addon-per-user"></a>

To disable the OpenAI AddOn for a particular user, use the following configuration. Ensure the `enabled` parameter is set to `false`. To turn the AddOn back on for a user, edit the parameter to `true`.

```json

const beeConfig = {
    uid: 'inactive-user',
    ... 
    addOns: [
      {
        id: "ai-integration",
        enabled: false
      },
    ],
    ...
}
     
```

## Disable AddOn Per Content Block Type <a href="#disable-addon-per-content-block-type" id="disable-addon-per-content-block-type"></a>

The OpenAI AddOn is available for the following content blocks:

* Title
* Paragraph
* List
* Button

You may utilize the Advanced Permissions configuration to disable OpenAI AddOn per content type.

The following example will disable the addon for the paragraph block:

### Example

```json

const beeConfig = {
    uid: 'string',
    ... 
    advancedPermissions: {
      content: {
        paragraph: {
          behaviors: {
            canViewSidebar: true,
          },
          properties: {
            aiIntegration: {
              show: false,
              locked: true
            },
          },
        },
      },
    }
    ...
}
     
```

## Prompt Suggestions <a href="#prompt-suggestions" id="prompt-suggestions"></a>

OpenAI AddOn includes preset prompt suggestions to facilitate the content creation process. These appear after the initial draft of your text has been formulated and whenever further refinement is needed. **Please note** that this function applies only when editing existing text through the AI prompt. The suggestions will not appear for placeholder text.

Here’s a simplified step-by-step guide on how to use suggestions, as shown below:

1. Start with your draft text added to the design area.
2. If you desire to adjust the tone to be more formal, for example, click on the paragraph, list, title, or button you want to modify.
3. Navigate to the ‘Write with AI’ option.
4. Click on the area designated for adding prompts.
5. You’ll notice the prompt suggestions popup.
6. Select the ‘Make it \[desired tone]’ option, making sure to replace \[desired tone] with a value (e.g., funny)
7. Click ‘Generate’.

The AI will then generate a revised version of your content, matching the tone you entered.

## Customize Prompt Suggestions <a href="#customize-prompt-suggestions" id="customize-prompt-suggestions"></a>

Below are the preset prompt suggestions we have identified for the different content tiles, along with their corresponding translation key, incase you’d like to revise the prompt through our custom languages feature.

### Paragraph

| Label                                                               | Key                                                   |
| ------------------------------------------------------------------- | ----------------------------------------------------- |
| Spell-check the content                                             | mailup-bee-common-component-ai.suggest-check-spelling |
| Correct grammar mistakes in the content                             | mailup-bee-common-component-ai.correct-grammar        |
| Translate content to \[language]                                    | mailup-bee-common-component-ai.translate              |
| Make it \[tone] without changing the format                         | mailup-bee-common-component-ai.adjust-tone            |
| Use Active Voice                                                    | mailup-bee-common-component-ai.use-active-voice       |
| Summarize the content                                               | mailup-bee-common-component-ai.summarize-text         |
| Convert the content to the third person without changing the format | mailup-bee-common-component-ai.convert-third-person   |

### Button

| Label                            | Key                                             |
| -------------------------------- | ----------------------------------------------- |
| Translate content to \[language] | mailup-bee-common-component-ai.translate        |
| Make it \[tone]                  | mailup-bee-common-component-ai.make-it-tone     |
| Use Active Voice                 | mailup-bee-common-component-ai.use-active-voice |

### List

| Label                                           | Key                                                   |
| ----------------------------------------------- | ----------------------------------------------------- |
| Spell-check the content                         | mailup-bee-common-component-ai.suggest-check-spelling |
| Correct grammar mistakes and return the content | mailup-bee-common-component-ai.correct-grammar-list   |
| Translate content to \[language]                | mailup-bee-common-component-ai.translate              |
| Make it \[tone] without changing the format     | mailup-bee-common-component-ai.adjust-tone            |
| Use Active Voice                                | mailup-bee-common-component-ai.use-active-voice       |

### Title

| Label                                       | Key                                                 |
| ------------------------------------------- | --------------------------------------------------- |
| Capitalize all letters                      | mailup-bee-common-component-ai.capitalize-text      |
| Capitalize the first letter of each word    | mailup-bee-common-component-ai.capitalize-all-words |
| Make it \[number] words long                | mailup-bee-common-component-ai.characters-length    |
| Make it \[tone] without changing the format | mailup-bee-common-component-ai.adjust-tone          |
| Translate it to \[language]                 | mailup-bee-common-component-ai.translate-heading    |
