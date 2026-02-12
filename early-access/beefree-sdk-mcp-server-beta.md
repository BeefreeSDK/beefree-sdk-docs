# Getting Started

{% hint style="warning" %}
**Join the Beta program and get early access to the Beefree SDK MCP Server**

Our MCP Server is currently in Beta and only accessible to a selected number of early access customers. If you're interested in joining the Beta, or if you'd like us to notify you when the tool is available to everyone, [**please let us know**](https://growens.typeform.com/to/gyH0gVgp#source=docs).

[**I'd love to join the Beta →**](https://growens.typeform.com/to/gyH0gVgp#source=docs) \
\
&#xNAN;_&#x42;eefree SDK Team_
{% endhint %}

## Introduction

The Beefree SDK MCP Server allows you to connect your AI Agents and clients with the Beefree SDK. It makes key functionality of the Beefree SDK — the [Editor](/broken/pages/OHBhoQNH2Zk7nqbwr3I3), our [Templates,](../apis/template-catalog-api/) or the [Check API](../apis/content-services-api/check.md) — accessible for AI agents, opening up new ways to bring agentic design directly into your application.&#x20;

{% hint style="info" %}
**Important**:&#x20;

* The MCP currently requires a live and correctly configured editor session to function properly. Ensure your Beefree SDK editor is running with MCP enabled before attempting to use any tools.
* We are also exploring a headless MCP version. Does it sound interesting for your use cases? [Let us know](https://devportal.beefree.io/hc/en-us/requests/new).
* We’re providing access to the MCP server that makes key Beefree SDK functionality accessible to AI agents and clients. However, providing the _agent_ is the responsibility of the Host Application. If you don’t have your own agent yet, consider this [sample application](beefree-sdk-mcp-server-beta.md#reference-sample-project) using a [PydanticAI](https://ai.pydantic.dev/) agent that you can get up and running in under 5 minutes.&#x20;
{% endhint %}

### What can you do with the Beefree MCP Server?

The Beefree MCP server empowers your product team to **seamlessly and quickly integrate AI-driven design processes** into your Beefree SDK-enabled software. This in turn lets your end users  leverage AI in creating, editing, and optimizing their email designs, reducing friction between idea and execution.

By replacing expensive custom integrations with an universal standard allowing instantaneous AI connection, the Beefree MCP server delivers:

1. **Drastic reduction in** **time-to-market**: you can deploy AI-powered features in hours instead of weeks or months for your embedded email builder.
2. **A Future-proof** **AI strategy**: MCP decouples your application and data from the specific AI model you are using for your project, so you can swap AI providers without rebuilding the infrastructure.
3. "**Magic" end-user experience**: the deep integration supercharges AI capabilities, with your users achieving professional results in seconds with zero learning curve.&#x20;

### Use Cases

Possible **use cases** empowered by the Beefree MPC Server include:

#### **Prompt to design**

Create complete, high-quality email designs from scratch with a single prompt.

{% embed url="https://www.youtube.com/watch?v=XNRL9bcJUPE" %}

#### **Instant rebranding**

Editing existing email designs by applying a different brand identity or color palette via AI.

{% embed url="https://www.youtube.com/watch?v=5oRqr1jA95E" %}

#### **Content iteration**

Generate content variations while maintaining  your core brand elements.

{% embed url="https://www.youtube.com/watch?v=bxQuCAr-Qic" %}

…and many more! Feel free to reach out to our team [talk about your use case](mailto:beta-feedback@beefree.io)!

### Try the MCP Server with our Sample Project

Here is a sample implementation of an MCP agent that you can use as a reference. You can draw inspiration and guidance from this example and choose your preferred LLM provider among Gemini, OpenAI, or Anthropic.

<figure><img src="../.gitbook/assets/CleanShot 2025-10-06 at 15.14.28.png" alt=""><figcaption></figcaption></figure>

You can reference the [Beefree SDK MCP example demo repository](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo) to clone and run the sample project. A complete working implementation is available in this repository. The sample showcases:

* [PydanticAI](https://ai.pydantic.dev/) agent integration with MCP
* Real-time streaming chat interface
* Beefree SDK editor with MCP enabled
* WebSocket-based communication

See the project's [README.md](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo/blob/main/README.md) for setup instructions and implementation details.

### Beefree SDK MCP Server & AI Agent Responsibilities

In the MCP architecture, **responsibilities are split** to ensure that AI models can access data and tools without needing custom code for every single integration.

The **Beefree SDK MCP Server** acts as the "Hands" and "Manual”: it uses a series of tools that  allow creating and editing an email in the Beefree SDK. The AI Agent acts as the "Brain": it knows what the user wants, based on the prompt, and which tools to call to achieve that goal.

|                     | MCP Server                                                                           | AI Agent                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| **Primary Role**    | The Connector that exposes tools and prompts                                         | The Host application (e.g. AI Agent) that manages the user session and the LLM.                |
| **Initiation**      | Waits for requests. Responds with a list of available tools, resources, and prompts. | Starts the connection. Discovers what the server is capable of via a handshake.                |
| **Logic Execution** | Executes the work. Performs the actual API call, database query, or file read/write. | Orchestrates the workflow. Decides _when_ to call a tool based on the model's intent.          |
| **Capabilities**    | Provides Tools (actions) and Resources (data).                                       | Provides Sampling (allows server to use the host's LLM) and Roots (defines folder boundaries). |
| **Security**        | Defines scope. Implements the actual access logic and data filtering.                | Enforces permissions. Asks the user for consent before a tool runs or a file is accessed.      |
| **Model Awareness** | Model-agnostic. Doesn't care which LLM is calling it; just follows the protocol.     | Knows which LLM is being used  and formats data for its context window.                        |
