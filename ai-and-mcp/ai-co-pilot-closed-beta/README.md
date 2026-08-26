# AI Co-Pilot (closed beta)

{% hint style="warning" %}
**Join the Beta program and get early access to Beefree SDK's AI Co-Pilot**

Beefree SDK's AI Co-Pilot is currently in closed beta and only accessible to a selected number of early access customers. If you're interested in joining the beta, or if you'd like us to notify you when the tool is available to everyone, [please let us know](https://growens.typeform.com/to/Eji2zu9q).

[I'd love to join the Beta →](https://growens.typeform.com/to/Eji2zu9q)

The Beefree SDK Team
{% endhint %}

Beefree SDK's AI Co-Pilot is the out-of-the-box AI agent that your user can prompt to create email designs, edit layouts, generate variations, and review templates. You install it in the Developer Console, choose a supported provider, and configure your model to make it available for your end users. Hosts can also persist chat history to continue guided sessions across visits and future revisions.

### Overview

Beefree SDK's AI Co-Pilot is installed as a Partner AddOn — part of the same family of ready-to-install extensions available through the [Beefree SDK Partner AddOns directory](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/partner-addons-directory).&#x20;

It is installed and configured directly from the Beefree SDK Developer Console, without any changes to your integration code. For a general walkthrough of how Partner AddOns work, see [Installing Partner AddOns](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/installing-partner-addons).

<figure><img src="../../.gitbook/assets/Screenshot 2026-05-04 at 18.48.40.png" alt=""><figcaption></figcaption></figure>

The AI Co-Pilot is a ready-made conversational agent that enables advanced workflows in the Beefree SDK email builder. Your users can prompt the agent to:

* **create full** **email designs** from scratch
* **edit existing designs**, for example by adding a content block, changing the structure, or switching the color palette
* **generate content variations** while preserving core brand elements
* **check an existing template** for quality or accessibility issues, for example missing image links or alt text

Unlike the [AI Writing Assistant](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant), which targets individual content blocks, the AI Co-Pilot surfaces a "Create with AI" panel. Thanks to this, your users can generate, iterate on, and apply content across their design in a guided chat experience within the Beefree email builder embedded in your application.

End users can always manually edit any design the agent generates. That keeps the workflow collaborative: AI helps your users move faster, while they stay in control as creative directors, shaping the final result to match their vision.

The AddOn is registered as `ai-agent` in the standard `addOns` array passed to `BeePlugin.create()`. Message history is surfaced through the existing `onInfo` callback.

### Activation

To enable Beefree SDK's AI Co-Pilot, contact your Beefree SDK Customer Success Manager. Once enabled for your application, you can configure it through the Beefree SDK Developer Console under **AddOns → Beefree AI AddOn.**

#### Prerequisites

* An API key from one of the [supported AI providers](https://docs.google.com/document/d/1gyhEZZl3x-CzSF8iLBjpk3-PN4KHAilkf6kiyNSf4xI/edit#supported-providers).
* The AI AddOn enabled in the Developer Console for your application.

#### Configure in the Developer Console

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io).
2. Navigate to your application, then open the AddOns section.
3. Click on Browse AddOns.
4. Select the Beefree AI AddOn.
5. Click Install.
6. You will then see the AI AddOn available in the installed AddOn section.
7. Set up your AI AddOn:
   * Select your provider.
   * Select your model.
   * Enter your API key.

Once you’ve completed the setup, toggle on Enable, then click Save.

#### Supported Providers

The AI Co-Pilot currently supports three AI providers.\
\
Three models are marked as Recommended—they offer the best trade-off between cost, speed, and output quality for typical builder workflows. This is not a quality ranking: higher-tier models (Claude Opus 4.7, GPT-5.4, Gemini 2.5 Pro) will generally produce stronger results on demanding tasks, but come with higher cost and latency. For most end-user sessions in a builder context, the recommended models are a good starting point.

#### Anthropic

[Anthropic](https://docs.anthropic.com/en/docs/welcome)'s Claude models prioritize safety, alignment, and high-quality conversational output — making them well-suited for creative and editorial workflows inside the builder.

Available models:

| <h4>Model Name</h4>             | <h4>Model String</h4> |
| ------------------------------- | --------------------- |
| Claude Haiku 4.5 \[recommended] | `claude-haiku-4-5`    |
| Claude Sonnet 4.6               | `claude-sonnet-4-6`   |
| Claude Opus 4.7                 | `claude-opus-4-7`     |

#### OpenAI

[OpenAI](https://platform.openai.com/docs/concepts)'s GPT models offer broad language coverage and advanced text generation capabilities across a wide range of writing styles and use cases.<br>

Available models:

| <h4>Model Name</h4>         | <h4>Model String</h4> |
| --------------------------- | --------------------- |
| GPT-5.4                     | `gpt-5.4`             |
| GPT-5.4 Mini \[recommended] | `gpt-5.4-mini`        |
| GPT-5.4 Nano                | `gpt-5.4-nano`        |

#### Gemini

[Gemini](https://ai.google.dev/) models from Google DeepMind offer multimodal capabilities and competitive performance on text generation tasks.

Available models:

| <h4>Model Name</h4>             | <h4>Model String</h4>   |
| ------------------------------- | ----------------------- |
| Gemini 2.5 Pro                  | `gemini-2.5-pro`        |
| Gemini 2.5 Flash \[recommended] | `gemini-2.5-flash`      |
| Gemini 2.5 Flash Lite           | `gemini-2.5-flash-lite` |

### AI Co-Pilot Configuration

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
      },
    },
  ],
}

```

#### Settings Reference<br>

| Field             | Type          | Required | Description                                                                                                                                                                                                                                                          |
| ----------------- | ------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `initialMessages` | message array | No       | Loads a previous conversation at panel mount. Pass back exactly what you received from `onInfo` as `detail.messages` — the shape is identical. Persist that array (e.g. in `localStorage`) and replay it here on the next session. Pass `[]` or omit to start blank. |
| `systemPrompt`    | `string`      | No       | Forwarded verbatim with every chat request. Use it to inject role, tone, or brand voice instructions.                                                                                                                                                                |
| `maxIterations`   | `number`      | No       | Caps the agent's auto-continue loop on tool-call turns. Defaults to `10`. Lower it to control cost and latency.                                                                                                                                                      |
| `loadingPhrases`  | `string[]`    | No       | Replaces the default cycling phrases shown under the loader (e.g. `"Sending request"`, `"Working"`). Phrases cycle per auto-continue turn and are announced via `aria-live`.                                                                                         |

#### Receiving Message Updates (`onInfo`)

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

#### Event Shape

| <h4>Field</h4>  | <h4>Value</h4>                                          |
| --------------- | ------------------------------------------------------- |
| `code`          | `1010`                                                  |
| `message`       | `"Messages changed for addon handle: ai-agent"`         |
| `detail.handle` | `"ai-agent"`                                            |
| detail.messages | Complete chat history — same shape as `initialMessages` |

#### When it Fires

* After each auto-continue turn (partial progress is preserved if the user closes the panel mid-iteration).
* When the model finishes its full response.
* When the user clicks **Stop** or closes the panel during active generation.

The initial emission caused by seeding the store from `initialMessages` is not echoed back — only real changes trigger the callback.

### Persisting Chat History

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

### Full Configuration Example

```
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

#### Disable the AI Co-Pilot Per User

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

### Additional Considerations

* Only one provider can be active per application at a time. You can switch providers at any time from the Developer Console without code changes.
* The `systemPrompt` field is a powerful lever for brand alignment — use it to enforce tone, language, and content guardrails across all end-user sessions.
* Lowering `maxIterations` from the default of `10` is recommended in cost-sensitive environments, especially when using larger models such as Claude Opus or GPT-5.4.
* For data security and privacy information, refer to the [AI Providers and Data Security](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant/data-security) page.

### Related Resources

* [AI Writing Assistant AddOn](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant) — block-level AI writing, configured separately.
* [Available Providers — AI Writing Assistant](https://docs.beefree.io/beefree-sdk/builder-addons/partner-addons/ai-writing-assistant/available-providers)
* [Configuration Reload](https://docs.beefree.io/beefree-sdk/getting-started/readme/installation/configuration-parameters/configuration-reload) — update AddOn settings in real time via `bee.loadConfig()`.
