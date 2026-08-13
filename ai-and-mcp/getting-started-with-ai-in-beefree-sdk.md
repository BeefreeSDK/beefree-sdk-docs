# Getting started with AI in Beefree SDK

Beefree SDK gives you more than one way to bring AI into your application. Whether you want to launch a ready-made AI feature this week or build a fully custom, agentic content workflow, this documentation page is your starting point for everything AI-related in the SDK.

Use the sections below to find the right entry point for what you're building, or jump straight to a specific feature.

### Three ways to build with AI

Beefree SDK supports three broad pathways for adding AI to your product. You don't have to pick one forever: many teams start on one path and grow into another as their needs evolve.

#### 🚀 AI AddOns: specialized assistants

Beefree SDK's AI AddOns are plug-and-play AI features you can install and launch in your application without any AI development work on your end. Great for specific tasks such as generating copy, images, translations, alt-text, these are the fastest way to bring AI-assisted content creation to your users.

<figure><img src="../.gitbook/assets/AI Writing Assistant.png" alt=""><figcaption></figcaption></figure>

You can install AI AddOns directly from the Developer Console and right away offer them to your end users.

| AddOn                                                                              | What it does                                                                                                               |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| [AI Writing Assistant](ai-writing-assistant/)                                      | Adds a "Write with AI" button to Title, Paragraph, List, and Button blocks. Powered by OpenAI, Azure OpenAI, or Anthropic. |
| [Custom AI Writing Assistant](ai-writing-assistant/custom-ai-writing-assistant.md) | Connect your own LLM to the "Write with AI" experience, with full control over the prompt and modal UI.                    |
| [Stability AI (Text to image)](stability-ai.md)                                    | Text-to-image generation, directly inside the builder.                                                                     |
| [Generate Alt Text with AI](generate-alt-text-with-ai/)                            | Automatically generates alt text for images using computer vision.                                                         |
| [DeepL (AI-powered translation)](deepl.md)                                         | Instantly translates content across multi-language templates.                                                              |

#### ✨Beefree AI: email generation copilot

{% hint style="info" %}
Beefree AI is currently in closed beta. [Learn more](beefree-ai-copilot-closed-beta/).
{% endhint %}

<figure><img src="../.gitbook/assets/Beefree AI Screen.jpg" alt=""><figcaption></figcaption></figure>

[Beefree AI (closed beta)](beefree-ai-copilot-closed-beta/) is a ready-to-launch prompt-to-design AI agent you can bring to your integration with no development work on your end. Unlike the single-purpose AddOns above, it's designed as a more complete AI experience empowering your end-users to

* create email design from a prompt
* edit existing design by adding blocks, modifying copy, or changing colors
* generate content variations
* check the effectiveness of existing templates

Beefree AI supports Anthropic, Gemini, and OpenAI.

#### 🤖 MCP Server: custom agentic workflows

If you want to build truly custom AI experiences, [Beefree SDK's MCP Server](getting-started/) is the way to go. It allows you to connect any AI agent directly to your SDK-powered application, enabling both in-editor and headless use cases:

* Generate email designs from a prompt, including sequences
* Edit and improve existing designs
* Translate content into another language or tone of voice
* Run AI-powered QA and validation workflows

{% embed url="https://drive.google.com/file/d/1sHvjGc82AdyDvUrCyItUo8aXbjfSzP82/view?usp=sharing" %}

{% hint style="info" %}
**Want to reduce AI token usage?** Try [Code Mode](getting-started/mcp-server-installation-and-setup.md#code-mode), an alternative way of connecting the MCP server and your AI agento that exposes a single TypeScript-scripting tool instead of many individual tool calls. This can reduce AI token consumption by up to 96%!
{% endhint %}

Start here with the MCP: [Getting started](getting-started/)

## Your path, our tech

**Building with a vibe coding or AI-assisted dev tool?**

See our [dedicated guide for vibe coders](https://developers.beefree.io/vibecoders) to get up and running fast.

**Have a vision for AI in your product, but not sure where to start?**

Talk to your CSX or [drop us an email](https://devportal.beefree.io/hc/en-us/requests/new). We'll work with you to turn your idea into a great content creation experience for your users.

## What's coming next

This page is the home for all current and future AI capabilities in Beefree SDK. As new AI features, agent updates, and MCP capabilities ship, they'll be added here first: check back or watch the [changelog](https://changelog.beefree.io/) for updates.
