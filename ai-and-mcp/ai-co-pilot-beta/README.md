# AI Co-Pilot (beta)

{% hint style="info" %}
Beefree SDK's AI Co-Pilot is currently in open beta and freely accessible to all customers with a paid plan. You just need to activate it in your Developer Console to make it available for your end-users.
{% endhint %}

Beefree SDK's AI Co-Pilot is the out-of-the-box AI agent that your user can prompt to create email designs, edit layouts, generate variations, and review templates. You install it in the Developer Console, choose a supported provider, and configure your model to make it available for your end users. Hosts can also persist chat history to continue guided sessions across visits and future revisions.&#x20;

### Overview

Beefree SDK's AI Co-Pilot is installed as a Partner AddOn — part of the same family of ready-to-install extensions available through the [Beefree SDK Partner AddOns directory](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/partner-addons-directory).&#x20;

It is installed and configured directly from the Beefree SDK Developer Console, without any changes to your integration code. For a general walkthrough of how Partner AddOns work, see [Installing Partner AddOns](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/installing-partner-addons).

<figure><img src="../../.gitbook/assets/Screenshot 2026-05-04 at 18.48.40.png" alt=""><figcaption></figcaption></figure>

The AI Co-Pilot is a ready-made conversational agent that enables advanced workflows in the Beefree SDK email builder. Your users can prompt the agent to:

* **create full** **email designs** from scratch
* **edit existing designs**, for example by adding a content block, changing the structure, or switching the color palette
* **generate content variations** while preserving core brand elements
* **check an existing template** for quality or accessibility issues, for example missing image links or alt text

If you'd like the Co-Pilot to follow specific brand guardrails, you can work with [Brand Rules](./#using-brand-rules-with-the-ai-co-pilot) to ensure the Co-Pilot's output matches your user's brand.&#x20;

Unlike the [AI Writing Assistant](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant), which targets individual content blocks, the AI Co-Pilot surfaces a "Create with AI" panel. Thanks to this, your users can generate, iterate on, and apply content across their design in a guided chat experience within the Beefree email builder embedded in your application.

End users can always manually edit any design the agent generates. That keeps the workflow collaborative: AI helps your users move faster, while they stay in control as creative directors, shaping the final result to match their vision.

AI Co-Pilot is registered as `ai-agent` in the standard `addOns` array passed to `BeePlugin.create()`. Message history is surfaced through the existing `onInfo` callback.

### Activation

You can configure AI Co-Pilot through the Beefree SDK Developer Console under **AddOns → AI Co-Pilot.**

<figure><img src="../../.gitbook/assets/AI Co-Pilot.png" alt=""><figcaption></figcaption></figure>

#### Prerequisites

* An API key from one of the [supported AI providers](./#supported-providers).

#### Configure in the Developer Console

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io).
2. Navigate to your application, then open the AddOns section.
3. Click on Browse AddOns and select **AI Co-Pilot**.
4. Click Install. You will then see the AI Co-Pilot available in the installed AddOn section.
5. Set up your AI Co-Pilot:
   * Select your provider.
   * Select your model.
   * Enter your API key.

Once you’ve completed the setup, toggle on Enable, then click Save.

### Supported providers

Three providers are currently supported: Anthropic, OpenAI, and Gemini. Each provider offers a range of models, from faster and more economical options to higher-capability ones that produce stronger output at higher cost and latency. The [Developer Console](https://developers.beefree.io/login?from=website_menu) shows a recommended default for each provider and flags any models that've been deprecated or retired. You'll always find current availability and status there, rather than on this page.

#### Anthropic

[Anthropic](https://docs.anthropic.com/en/docs/welcome)'s Claude models prioritize safety, alignment, and high-quality conversational output — making them well-suited for creative and editorial workflows inside the builder.

#### OpenAI

[OpenAI](https://platform.openai.com/docs/concepts)'s GPT models offer broad language coverage and advanced text generation capabilities across a wide range of writing styles and use cases.

#### Gemini

[Gemini](https://ai.google.dev/) models from Google DeepMind offer multimodal capabilities and competitive performance on text generation tasks.

### AI Co-Pilot configuration

Add an entry with `id: 'ai-agent'` to `beeConfig.addOns`. All `settings` fields are optional.

```
const beeConfig = {
  // ...your standard config
  addOns: [
    {
      id: 'ai-agent',
      settings: {
        initialMessages,  // seed the chat on open — same shape returned by onInfo
        systemPrompt,     // string — appended to every chat request
        maxIterations,    // number — auto-continue cap (default: 10)
        loadingPhrases,   // string[] — overrides default cycling loader text
        brandRules,       // brandRules object
        beforeSendTimeout, // number (ms) — wait for the aiAgentBeforeSend hook (default: 30000)
      },
    },
  ],
}

```

#### Custom System Prompt

Customizing the system prompt lets you control how the AI Co-Pilot behaves in your application. Use it to define tone of voice, brand guidelines, and the kind of content the assistant should favor or avoid, so generated design and copy stays consistent with your product and your users’ expectations.

{% hint style="info" %}
System Prompt customization is only available for Superpowers and Enterprise plans.
{% endhint %}

#### Settings reference

| Field             | Type                | Required | Description                                                                                                                                                                                                                                                          |
| ----------------- | ------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `initialMessages` | message array       | No       | Loads a previous conversation at panel mount. Pass back exactly what you received from `onInfo` as `detail.messages` — the shape is identical. Persist that array (e.g. in `localStorage`) and replay it here on the next session. Pass `[]` or omit to start blank. |
| `systemPrompt`    | `string`            | No       | Forwarded verbatim with every chat request. Use it to inject role, tone, or brand voice instructions.                                                                                                                                                                |
| `maxIterations`   | `number`            | No       | Caps the agent's auto-continue loop on tool-call turns. Defaults to `10`. Lower it to control cost and latency.                                                                                                                                                      |
| `loadingPhrases`  | `string[]`          | No       | Replaces the default cycling phrases shown under the loader (e.g. `"Sending request"`, `"Working"`). Phrases cycle per auto-continue turn and are announced via `aria-live`.                                                                                         |
| `brandRules`      | `brandRules` object | No       | Brand Rules the Co-Pilot must follow (presets, permissions, limits). See the [Brand Rules](../brand-rules-for-ai.md) page for the full schema and logic.                                                                                                             |
| `beforeSendTimeout` | `number`          | No       | How long (in milliseconds) the Co-Pilot waits for your [`aiAgentBeforeSend`](./#checking-prompts-before-they-are-sent-aiagentbeforesend) hook to answer. Defaults to `30000`. With no answer in time, the prompt is not sent. Ignored when the hook is not configured. |

#### Receiving message updates (`onInfo`)

The panel's chat history is broadcast through the SDK's top-level `onInfo` callback. Filter by `code` and `detail.handle`:

```
const beeConfig = {
  // ...
  onInfo(data) {
    if (data?.code === 1010 && data?.detail?.handle === 'ai-agent') {
      // data.detail.messages — full conversation so far.
      // Persist it and pass it back next session as initialMessages.
      persistAiAgentMessages(data.detail.messages)
    }
  },
}

```

#### Event shape

| <h4>Field</h4>  | <h4>Value</h4>                                          |
| --------------- | ------------------------------------------------------- |
| `code`          | `1010`                                                  |
| `message`       | `"Messages changed for addon handle: ai-agent"`         |
| `detail.handle` | `"ai-agent"`                                            |
| detail.messages | Complete chat history — same shape as `initialMessages` |

#### When it fires

* After each auto-continue turn (partial progress is preserved if the user closes the panel mid-iteration).
* When the model finishes its full response.
* When the user clicks **Stop** or closes the panel during active generation.

The initial emission caused by seeding the store from `initialMessages` is not echoed back — only real changes trigger the callback.

### Persisting chat history

The SDK does not store the conversation itself — persistence is the host application's responsibility. The simplest approach uses `localStorage`:

```
const STORAGE_KEY = 'aiAgent.messages'

function getInitialMessages() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY)
    return raw ? JSON.parse(raw) : []
  } catch { return [] }
}

function persistMessages(messages) {
  try { localStorage.setItem(STORAGE_KEY, JSON.stringify(messages)) }
  catch (err) { console.warn('[aiAgent] persist failed', err) }
}

const beeConfig = {
  addOns: [{ id: 'ai-agent', settings: { initialMessages: getInitialMessages() } }],
  onInfo(data) {
    if (data?.code === 1010 && data?.detail?.handle === 'ai-agent') {
      persistMessages(data.detail.messages)
    }
  },
}

```

This produces a conversation that survives page reloads and follows the user across sessions.

### Full configuration example

```javascript
const STORAGE_KEY = 'aiAgent.messages'

const beeConfig = {
  client,
  uid,
  // ...standard config
  addOns: [
    {
      id: 'ai-agent',
      settings: {
        initialMessages: JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'),
        systemPrompt:    "You write in the brand's friendly, concise voice.",
        maxIterations:   8,
        loadingPhrases:  ['Drafting', 'Tweaking copy', 'Polishing'],
        brandRules: {
          presets: {
            blocks: {
              button: {
                'brand-cta': {
                  description: 'Mandatory brand CTA button style',
                  properties: {
                    backgroundColor: '#7747FF',
                    color: '#FFFFFF',
                    borderRadius: '24px',
                  },
                },
              },
            },
          },
          permissions: {
            blocks: {
              noAdd: ['video'],
              noDelete: ['menu'],
            },
          },
          limits: {
            rows: { max: 12 },
          },
        },
      },
    },
  ],
  onInfo(data) {
    if (data?.code === 1010 && data?.detail?.handle === 'ai-agent') {
      try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(data.detail.messages))
      } catch (err) { /* noop */ }
    }
    // ...handle other onInfo codes here
  },
}

BeePlugin.create(token, beeConfig, (instance) => {
  // editor ready
})
```

### Checking prompts before they are sent (`aiAgentBeforeSend`)

You can inspect every prompt your users type into the Co-Pilot **before** it leaves the browser, for example to run a DLP check that keeps personal or sensitive data away from Beefree and the AI provider. Define the optional `aiAgentBeforeSend` hook in `beeConfig.hooks`, the same way as other hooks such as `getMentions`.

The Co-Pilot calls the hook first, before anything reaches Beefree's backend. The prompt is sent only when your handler resolves with `{ allowed: true }`.

```javascript
const beeConfig = {
  // ...
  hooks: {
    aiAgentBeforeSend: {
      handler: async (resolve, reject, { promptText }) => {
        try {
          const verdict = await checkPrompt(promptText) // your own DLP / policy check
          if (verdict.ok) {
            resolve({ allowed: true })
          } else {
            resolve({ allowed: false, message: 'Please remove patient data from your prompt.' })
          }
        } catch (err) {
          reject() // the prompt is not sent
        }
      },
    },
  },
}
```

#### Handler arguments

| Field        | Type     | Description                       |
| ------------ | -------- | --------------------------------- |
| `promptText` | `string` | The text the user typed and sent. |

#### Response

Call `resolve` with:

| Field     | Type      | Required | Description                                                                                                                                                                  |
| --------- | --------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `allowed` | `boolean` | Yes      | `true` sends the prompt, `false` blocks it.                                                                                                                                  |
| `message` | `string`  | No       | Shown to the user when the prompt is blocked, as plain text (no HTML), truncated to 500 characters. When omitted, a default message asks the user to edit the prompt and try again. |

#### What the user sees

* **Allowed:** the Co-Pilot proceeds as usual.
* **Blocked** (`allowed: false`): the chat shows your `message` (or the default text). The prompt stays in the input so the user can edit it. No Retry button is offered, since the same prompt would be blocked again.
* **Check failed:** the prompt is not sent and the chat shows a "couldn't verify this prompt" message with a Retry button. Retry calls your hook again. This happens when:
  * your handler calls `reject`,
  * your handler resolves with a malformed response (for example, `allowed` is missing or not a boolean),
  * your handler does not answer within `beforeSendTimeout` (default 30 seconds), including when it throws before calling `resolve` or `reject`.

The check is **fail-closed**: whenever there is no clear `{ allowed: true }`, nothing is sent.

When the hook is not configured, the Co-Pilot behaves exactly as before, with no extra round trip.

{% hint style="warning" %}
Only the text the user types is passed to the hook. The template content, including the selected element's content, still reaches the AI provider through the Co-Pilot's tools while it works on the design. Account for this in your data protection policy.
{% endhint %}

### Using Brand Rules with the AI Co-Pilot

With [Brand Rules](../brand-rules-for-ai.md), you can attach a `brandRules` object when starting an AI editing session. Brand Rules act as guardrails that the Co-Pilot must work within so that the output it generates matches your (or your end users') brand.&#x20;

Please check out the [Brand Rules page](../brand-rules-for-ai.md) for a full overview of the different types of Brand Rules you can set and to access the full JSON Schema for Brand Rules.&#x20;

To make the Co-Pilot work with Brand Rules, you simply pass the `brandRules` object in the AI Agent `settings` section of your config file when starting an AI editing session. Check out the [example above ](./#full-configuration-example)to see what that can look like.

{% hint style="info" %}
Tip: You can use the [Brand Rules validation endpoint](../brand-rules-for-ai.md#testing-and-validating-your-brand-rules) to validate your Brand Rules JSON before starting an AI editing session with the Co-Pilot.
{% endhint %}

### Disable the AI Co-Pilot per user

To disable the AI Co-Pilot for a specific user, set `enabled: false` on the AddOn entry. To re-enable it, change the value to `true`.

```
const beeConfig = {
  uid: 'inactive-user',
  addOns: [
    {
      id: 'ai-agent',
      enabled: false,
    },
  ],
}
```

### Additional considerations

* Only one provider can be active per application at a time. You can switch providers at any time from the Developer Console without code changes.
* The `systemPrompt` field is a powerful lever for brand alignment — use it to enforce tone, language, and content guardrails across all end-user sessions.
* Lowering `maxIterations` from the default of `10` is recommended in cost-sensitive environments, especially when using larger models such as Claude Opus or GPT-5.4.
* To enforce your own data policy on user prompts (for example DLP for personal or health data), use the [`aiAgentBeforeSend`](./#checking-prompts-before-they-are-sent-aiagentbeforesend) hook. It adds one round trip to your handler on every send.
* For data security and privacy information, refer to the [AI Providers and Data Security](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant/data-security) page.

### Related resources

* [AI Writing Assistant AddOn](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant) — block-level AI writing, configured separately.
* [Available Providers — AI Writing Assistant](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant/available-providers)
* [Configuration Reload](https://docs.beefree.io/beefree-sdk/getting-started/readme/installation/configuration-parameters/configuration-reload) — update AddOn settings in real time via `bee.loadConfig()`.
