# MCP Server FAQs

#### What is the Beefree SDK MCP Server?

It's an adapter that lets AI agents (via the Model Context Protocol) create, modify, and validate email designs using the Beefree SDK ecosystem (Editor, Check API). It exposes a set of tools agents can call.

#### What is MCP in one sentence?

MCP is an open protocol (think "USB-C for AI") that standardizes how clients connect to servers, exposing tools, resources, and prompts over JSON-RPC.

#### What's the difference between an MCP Server and an Agent? Does Beefree provide both?

An MCP server exposes data or tools to AI models through a standardized interface — it provides capabilities but doesn’t make decisions. An AI agent, on the other hand, is a system that can autonomously perceive its environment, reason about goals, and take actions. Agents can use MCP servers to get information or perform tasks.

We provide the MCP Server that makes key Beefree SDK functionality accessible to AI agents. The host application is responsible for providing the agent. If you don't have your own agent yet, check out [our sample application using a PydanticAI agent](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo), which you can get up and running in under five minutes.

#### What is the purpose of the Beefree SDK MCP Server beta?

The beta lets you explore how AI agents can integrate directly with the Beefree SDK ecosystem — designing, customizing, and validating emails programmatically — while we gather feedback and continue to refine the experience. Your input directly shapes what we prioritize next.

#### Which plans can access the MCP?

The MCP Server is available to all paying customers as an open beta. No waitlist or CSM request is required. If you are on a free plan, you will need to upgrade to access it. Broader availability and plan-based entitlements will be communicated before general availability.

#### How do I get access?

Access is available directly to all paying customers with no application or approval needed. Sign in to your developer account and follow the [Installation & Setup](https://app.gitbook.com/o/2zoWGxtV7bjhbwBdjGPS/s/8c7XIQHfAtM23Dp3ozIC/~/diff/~/changes/579/mcp-server/installation-and-setup) guide to get started.

#### What are the two integration paths, and which one should I use?

The Beefree SDK MCP Server supports two ways to connect your AI agent to the editor:

* **API-managed session** — your host application creates and manages the session via the Headless API. Choose this if [co-editing](../other-customizations/collaborative-editing/) is enabled on your account and you want support for multiple concurrent users, per-change history, or persistent sessions.
* **Editor-managed session** — the editor creates a temporary session on demand via `bee.startMcpSession()`. Choose this if co-editing is not enabled, or if you want a simpler setup without backend session management.

Both paths use the same MCP endpoint and tools. See [Installation & Setup](mcp-server-installation-and-setup.md) for full details on each.

#### Who should use the MCP beta?

* Product teams exploring AI-driven content workflows
* Developers building MCP-capable clients (e.g., IDEs, agents, assistants)
* Teams that want to streamline design inside automated pipelines

#### Can I use Beefree SDK's MCP Server in production?

We recommend testing and prototyping during the beta. While the server is stable, APIs and access policies may change before general availability, and this version may differ from the final release.

#### Is the MCP feature complete? What are the current limitations?

The MCP integration is still evolving. While you can already perform many email builder operations, there are some limitations to be aware of:

* Not all content blocks are supported yet
* Some block properties and advanced configuration options are not covered
* Functionality may change as we iterate during the beta

We encourage you to explore the available tools and share feedback — your input helps us prioritize and close gaps.

#### What kind of feedback are you looking for?

All kinds, including:

* How easy it is to discover, understand, and use the tools in the MCP catalog — whether tool names are clear, arguments make sense, and the tool set feels complete for your workflow
* Coverage gaps (tools you need that aren't exposed yet)
* Performance of the Check API in real workflows
* Gaps in documentation or developer experience

Share feedback with your CSM or email [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io).

#### Does the MCP also support the Landing Page Builder or the Popup Builder?

The beta currently focuses on the Beefree SDK Email Builder. Support for the Landing Page and Popup builders is limited, but will be considered for future updates.

#### **What is the** applicable **use policy?**

During the beta, you may use the MCP Server and its tools for development, prototyping, and evaluation. Access is subject to Beefree SDK's standard Terms of Service. Abuse or production-scale misuse will result in suspension of access.

#### Is my data secure when using MCP?

Yes. MCP calls are authenticated with secure keys, tied to your session, and handled in accordance with Beefree SDK's security and data policies.

#### I have questions, feedback, or a bug to report. Who should I contact?

Contact your Beefree SDK Customer Success Manager or email [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io). We actively review feedback during the beta, and your input shapes product improvements.

#### Are the MCP calls free of charge?

Yes, during the open beta, MCP calls are free. However, please note that you will still be charged by your AI model provider for the agent model usage, as those costs are independent of Beefree's billing. Once the MCP Server reaches general availability, calls will be billed under your CSAPI entitlements. Pricing details will be communicated before that transition.

#### How do I balance speed, token usage, and output quality?

Model choice is the biggest lever. For token usage specifically, consider [Code Mode](mcp-server-installation-and-setup.md#code-mode-research-preview), now in open beta. Code mode is an experimental alternative that optimizes your interaction with the Beefree SDK MCP Server.

#### What is Code Mode?

Code Mode is an alternative way for interacting with the Beefree SDK MCP Server, currently in open beta. Instead of exposing 33 individual tools, each with a full parameter schema sent on every turn, Code Mode exposes a single tool that accepts a TypeScript script. Your agent writes one script that performs all operations in a single round trip: creating sections, adding content, and setting styles.

In internal benchmarks across five models and three email complexity levels, Code Mode reduced total token consumption by 68–96%, with most results in the 85–95% range.

#### When should I use Code Mode?

Use Code Mode when your agent makes many sequential tool calls to reduce API costs and latency. It's particularly effective if your use case involves complex email-generation workflows, where the repeated overhead of sending tool schemas on every turn becomes a significant cost driver.

Note that Code Mode requires your agent to generate valid TypeScript, so you should implement error handling to manage partial failures. Because this feature is in beta, behavior may change before general availability.
