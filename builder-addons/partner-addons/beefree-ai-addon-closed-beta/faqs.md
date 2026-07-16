# FAQs

#### **What is the Beefree AI AddOn?**&#x20;

The Beefree AI AddOn is a Partner AddOn available through the Beefree SDK. Once installed, it surfaces a conversational AI panel directly inside the builder within your application, letting end users generate, iterate on, and apply content across their email design, all without leaving the editor.

#### **How is this different from the AI Writing Assistant?**&#x20;

The AI Writing Assistant targets individual content blocks. The AI AddOn goes further, surfacing a full conversational agent panel that allows users to work across their entire design in a guided chat experience.

#### **How do I get access?**&#x20;

Log in to the Beefree SDK Developer Console, navigate to your application, and open the AddOns section. From there, click Browse AddOns, select the Beefree AI AddOn, and click Install. Once installed, select your provider and model, enter your API key, toggle Enable, and save. Make sure you have an active Superpowers or Enterprise plan and an API key from your chosen AI provider before starting.

#### **What plans support the AI AddOn?**&#x20;

The AI AddOn requires an active Beefree SDK Superpowers or Enterprise plan.

#### **Do I need my own AI provider API key?**&#x20;

Yes. You supply an API key from a supported provider during setup in the Developer Console. Beefree does not provide API keys.

#### **Which AI providers and models are supported?**&#x20;

Three providers are currently supported: Anthropic, OpenAI, and Gemini (Gemini support is currently in preview). Each provider offers multiple models. Recommended starting points, chosen for their balance of cost, speed, and output quality, are Claude Haiku 4.5, GPT-5.4 Mini, and Gemini 2.5 Flash. Higher-tier models are available if your use case demands stronger output, but come with higher cost and latency.

#### **Can I customize how the AI behaves for my users?**&#x20;

Yes. The `systemPrompt` setting lets you inject role, tone, or brand voice instructions that are forwarded with every chat request. This is the primary lever for ensuring the AI stays aligned with your brand across all end-user sessions.

#### **Can I control costs?**&#x20;

Yes. The `maxIterations` setting caps the agent's auto-continue loop, with a default of 10. Lowering it is recommended in cost-sensitive environments, especially when using larger models.

#### **Can I persist chat history across sessions?**&#x20;

Yes, though persistence is the responsibility of the host application. The SDK broadcasts the full conversation through the `onInfo` callback after each turn. You store it, then pass it back as `initialMessages` on the next session.

#### **Can I disable the AddOn for specific users?**&#x20;

Yes. Set `enabled: false` on the AddOn entry in `beeConfig` for any user you want to exclude.

#### **Is this available in production?**&#x20;

Not yet. The AI AddOn is currently a research preview, available to selected partners. The interface, configuration options, supported models, and underlying behavior are all subject to change. Do not use it in production. Share feedback directly with your Beefree customer success manager.

#### **What is the applicable use policy?**

During the beta, you may use the MCP Server and its tools for development, prototyping, and evaluation. Access is subject to Beefree SDK's standard Terms of Service. Abuse or production-scale misuse will result in suspension of access.

<br>
