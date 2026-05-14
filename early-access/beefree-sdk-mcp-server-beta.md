# Getting Started

{% hint style="warning" %}
**Join the Beta program and get early access to the Beefree SDK MCP Server**

Our MCP Server is currently in Beta and only accessible to a selected number of early access customers. If you're interested in joining the Beta, or if you'd like us to notify you when the tool is available to everyone, [please let us know](https://growens.typeform.com/to/gyH0gVgp#source=docs).

[I'd love to join the Beta →](https://growens.typeform.com/to/gyH0gVgp#source=docs)

Beefree SDK Team
{% endhint %}

## Introduction

The Beefree SDK MCP Server allows you to connect your AI agents to the Beefree SDK. It makes key functionality of the Beefree SDK — the [Editor](/broken/pages/OHBhoQNH2Zk7nqbwr3I3) and the [Check API](../apis/content-services-api/check.md) — accessible to AI agents, opening new ways to bring agentic design directly into your application.&#x20;

{% hint style="info" %}
**Important**:&#x20;

* The MCP Server requires either a live and correctly configured editor session or a server-side session created via the Headless API. See [Installation & Setup](../mcp-server/installation-and-setup.md) to choose the right path for your setup.
* Providing the agent is the responsibility of the host application. If you don't have your own agent yet, see the [sample projects](beefree-sdk-mcp-server-beta.md#sample-projects) below.
{% endhint %}

### What can you do with the Beefree MCP Server?

The Beefree MCP Server empowers your product team to seamlessly integrate AI-driven design into your Beefree SDK-powered application — letting your end users leverage AI to create, edit, and optimize email designs with less friction between idea and execution.

By replacing custom integrations with a universal standard, the Beefree MCP Server delivers:

1. **Drastic reduction in time-to-market:** deploy AI-powered features in hours instead of weeks.
2. **A Future-proof** **AI strategy**: MCP decouples your application from any specific AI model, so you can swap providers without rebuilding infrastructure.
3. **A seamless end-user experience**: deep integration lets users achieve professional results in seconds with no learning curve.

### Use Cases

#### Interactive Design in the Editor

These use cases involve an AI agent editing a template while the user is working in the editor — changes appear in real time.

**Prompt to design**

Create complete, high-quality email designs from scratch with a single prompt.

{% embed url="https://www.youtube.com/watch?v=XNRL9bcJUPE" %}

**Instant rebranding**

Editing existing email designs by applying a different brand identity or color palette via AI.

{% embed url="https://www.youtube.com/watch?v=5oRqr1jA95E" %}

**Content iteration**

Generate content variations while maintaining your core brand elements.

{% embed url="https://www.youtube.com/watch?v=bxQuCAr-Qic" %}

#### Automated & Headless Workflows

These use cases run entirely server-side — no editor session required. The agent operates on templates through the Headless API, making them suitable for large-scale automation and backend pipeline integration.

**Bulk generation**

Programmatically generate large volumes of unique email variants without manual intervention. Ideal for large-scale campaigns where each variant requires tailored content or layout.

**Iterative variation**

Automatically produce a series of design or layout variations from a single template. Useful for rapid A/B testing or content experimentation driven entirely by backend scripts or AI agents.

**External workflow integration**

Trigger template modifications directly from third-party automation platforms such as n8n, Zapier, Make, Retool, or Tines. Because there is no frontend dependency, Beefree SDK actions slot into any workflow that can make an HTTP request.

…and many more! Feel free to reach out to our team [talk about your use case](mailto:beta-feedback@beefree.io)!

### Sample Projects

**Interactive Editor Agent**

A sample implementation using a [PydanticAI](https://ai.pydantic.dev/) agent connected to a MCP editor session. Supports Gemini, OpenAI, and Anthropic as LLM providers.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

The sample showcases:

* [PydanticAI](https://ai.pydantic.dev/) agent integration with MCP
* Real-time chat interface
* Beefree SDK editor with MCP integration

Clone and run from the [Beefree SDK MCP v2 example demo repository](https://github.com/BeefreeSDK/beefree-sdk-mcp-v2-example-demo). See the `/integration` page for setup instructions.

**Headless Agent**

A fully functioning **headless MCP** demo covering five end-to-end automation use cases. Supports Gemini, OpenAI, and Anthropic as LLM providers.

{% hint style="info" %}
Using an email building agent generates LLM API costs. The sample project includes a token counter to help you track usage.
{% endhint %}

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Clone and run from the [Beefree SDK MCP v2 example demo repository](https://github.com/BeefreeSDK/beefree-sdk-mcp-v2-example-demo).

### Beefree SDK MCP Server & AI Agent Responsibilities

In the MCP architecture, responsibilities are split so that AI models can access data and tools without custom code for every integration.

The **Beefree SDK MCP Server** acts as the "Hands" and "Manual": it exposes tools that allow creating and editing emails in the Beefree SDK. The AI Agent acts as the "Brain": it knows what the user wants and which tools to call to achieve that goal.

|                 | MCP Server                                                                          | AI Agent                                                                                      |
| --------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| Primary Role    | The connector that exposes tools and prompts                                        | The host application that manages the user session and the LLM                                |
| Initiation      | Waits for requests. Responds with a list of available tools, resources, and prompts | Starts the connection. Discovers capabilities via a handshake                                 |
| Logic Execution | Executes the work. Performs the actual API call, database query, or file read/write | Orchestrates the workflow. Decides when to call a tool based on the model's intent            |
| Capabilities    | Provides Tools (actions) and Resources (data)                                       | Provides Sampling (allows server to use the host's LLM) and Roots (defines folder boundaries) |
| Security        | Defines scope. Implements the actual access logic and data filtering                | Enforces permissions. Asks the user for consent before a tool runs or a file is accessed      |
| Model Awareness | Model-agnostic. Doesn't care which LLM is calling it; just follows the protocol     | Knows which LLM is being used and formats data for its context window                         |
