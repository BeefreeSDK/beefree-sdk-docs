# MCP Server FAQs

#### What is the Beefree SDK MCP Server?

It's an adapter that lets AI agents (via the Model Context Protocol) create, modify, and validate email designs using the Beefree SDK ecosystem (Editor, Check API). It exposes a set of tools agents can call.

#### What is MCP in one sentence?

MCP is an open protocol (think "USB-C for AI") that standardizes how clients connect to servers, exposing tools, resources, and prompts over JSON-RPC.

#### What's the difference between an MCP Server and an Agent? Does Beefree provide both?

An MCP server exposes data or tools to AI models through a standardized interface — it provides capabilities but doesn’t make decisions. An AI agent, on the other hand, is a system that can autonomously perceive its environment, reason about goals, and take actions. Agents can use MCP servers to get information or perform tasks.

We provide the MCP Server that makes key Beefree SDK functionality accessible to AI agents. The host application is responsible for providing the agent. If you don't have your own agent yet, check out [our sample application using a PydanticAI agent](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo), which you can get up and running in under five minutes.

#### Which plans can access the MCP?

The MCP Server is available on Essentials, Core, Superpowers, and Enteprise plans.

#### How do I get access?

Access is available directly to all paying customers with no application or approval needed. Sign in to your developer account and follow the [Installation & Setup](https://app.gitbook.com/o/2zoWGxtV7bjhbwBdjGPS/s/8c7XIQHfAtM23Dp3ozIC/~/diff/~/changes/579/mcp-server/installation-and-setup) guide to get started.

#### What are the two integration paths, and which one should I use?

The Beefree SDK MCP Server supports two ways to connect your AI agent to the editor:

* **API-managed session** — your host application creates and manages the session via the Headless API. Choose this if [co-editing](../../other-customizations/collaborative-editing/) is enabled on your account and you want support for multiple concurrent users, per-change history, or persistent sessions.
* **Editor-managed session** — the editor creates a temporary session on demand via `bee.startMcpSession()`. Choose this if co-editing is not enabled, or if you want a simpler setup without backend session management.

Both paths use the same MCP endpoint and tools. See [Installation & Setup](mcp-server-installation-and-setup.md) for full details on each.

#### Who should use the MCP Server?

* Product teams exploring AI-driven content workflows
* Developers building MCP-capable clients (e.g., IDEs, agents, assistants)
* Teams that want to streamline design inside automated pipelines

#### Is the MCP feature complete? What are the current limitations?

The MCP integration is still evolving. While you can already perform many email builder operations, there are some limitations to be aware of:

* Not all content blocks are supported yet
* Some block properties and advanced configuration options are not covered

We encourage you to explore the available tools and share feedback — your input helps us prioritize and close gaps.

#### Does the MCP also support the Landing Page Builder or the Popup Builder?

The MCP Server currently supports the Beefree SDK Email Builder. Support for the Landing Page and Popup builders is limited, but will be considered for future updates.

#### Is my data secure when using MCP?

Yes. MCP calls are authenticated with secure keys, tied to your session, and handled in accordance with Beefree SDK's security and data policies.

#### I have questions, feedback, or a bug to report. Who should I contact?

Contact your Beefree SDK Customer Success Manager or submit a request via our [Help Center](https://devportal.beefree.io/hc/en-us/requests/new). We actively review feedback, and your input shapes product improvements.

#### Are the MCP calls free of charge?

Calls are billed under your CSAPI entitlements.

#### How do I balance speed, token usage, and output quality?

Model choice is the biggest lever. For token usage specifically, consider [Code Mode](mcp-server-installation-and-setup.md#code-mode-research-preview), now in open beta. Code mode is an experimental alternative that optimizes your interaction with the Beefree SDK MCP Server.

#### What is Code Mode?

Code Mode is an alternative way for interacting with the Beefree SDK MCP Server, currently in open beta. Instead of exposing 33 individual tools, each with a full parameter schema sent on every turn, Code Mode exposes a single tool that accepts a TypeScript script. Your agent writes one script that performs all operations in a single round trip: creating sections, adding content, and setting styles.

In internal benchmarks across five models and three email complexity levels, Code Mode reduced total token consumption by 68–96%, with most results in the 85–95% range.

#### When should I use Code Mode?

Use Code Mode when your agent makes many sequential tool calls to reduce API costs and latency. It's particularly effective if your use case involves complex email-generation workflows, where the repeated overhead of sending tool schemas on every turn becomes a significant cost driver.

Note that Code Mode requires your agent to generate valid TypeScript, so you should implement error handling to manage partial failures. Because this feature is in beta, behavior may change before general availability.
