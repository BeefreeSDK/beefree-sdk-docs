# Beefree AI FAQs

#### **What is Beefree SDK's AI Co-Pilot ?**&#x20;

The AI Co-Pilot is a ready-made promt-to-design agent available in the email builder. It is installed as  a Partner AddOn in Developer Console. Once installed, it surfaces a conversational AI panel directly inside the builder within your application, letting end users generate, iterate on, and apply content across their email design, all without leaving the editor.

#### **How is this different from the AI Writing Assistant?**&#x20;

The AI Writing Assistant targets individual content blocks. The AI Co-Pilot goes further, surfacing a full conversational agent panel that allows users to work across their entire design in a guided chat experience.

#### **How do I get access?**&#x20;

The AI Co-Pilot is freely accessible in open beta. You just need to log in to the Beefree SDK Developer Console, navigate to your application, and open the AddOns section. From there, click Browse AddOns, select the Beefree AI AddOn, and click Install. Once installed, select your provider and model, enter your API key, toggle Enable, and save. Make sure you have an API key from your chosen AI provider before starting.

#### **Do I need my own AI provider API key?**&#x20;

Yes. You supply an API key from a supported provider during setup in the Developer Console. Beefree does not provide API keys.

#### **Which AI providers and models are supported?**&#x20;

Three providers are currently supported: Anthropic, OpenAI, and Gemini. Each provider offers multiple models. Higher-tier models will provide stronger output, but come with higher cost and latency. For Anthropic, Claude Haiku 5.5 leads at the lower tier and Claude Opus 5 at the higher tier. For OpenAI, GPT-6 Sol produces the strongest results, though at higher cost; GPT-5.6 Luna and GPT-5.5 follow closely behind. For Gemini, Gemini 3.7 Flash and Gemini 3.8 Flash are the strongest performers. In our internal testing, Gemini models as a group tended to produce lower-quality output than Anthropic or OpenAI models.

#### **Can I customize how the AI behaves for my users?**&#x20;

Yes. The `systemPrompt` setting lets you inject role, tone, or brand voice instructions that are forwarded with every chat request.&#x20;

You can also use [Brand Rules](../brand-rules-for-ai.md) to ensure the Co-Pilot follows specific brand guidelines.&#x20;

#### **Can I control costs?**&#x20;

Yes. The `maxIterations` setting caps the agent's auto-continue loop, with a default of 10. Lowering it is recommended in cost-sensitive environments, especially when using larger models.

#### **Can I persist chat history across sessions?**&#x20;

Yes, though persistence is the responsibility of the host application. The SDK broadcasts the full conversation through the `onInfo` callback after each turn. You store it, then pass it back as `initialMessages` on the next session.

#### **Can I disable the Co-Pilot for specific users?**&#x20;

Yes. Set `enabled: false` on the AI Co-Pilot entry in `beeConfig` for any user you want to exclude.

#### **Is this available in production?**&#x20;

Not yet. The AI Co-Pilot is currently in closed beta for selected partners. The interface, configuration options, supported models, and underlying behavior are all subject to change. Do not use it in production. Share feedback directly with your Beefree customer success manager.

#### **What is the applicable use policy?**

During the beta, you may use the MCP Server and its tools for development, prototyping, and evaluation. Access is subject to Beefree SDK's standard Terms of Service. Abuse or production-scale misuse will result in suspension of access.
