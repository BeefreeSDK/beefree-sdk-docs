# FAQ

#### What is the Beefree SDK MCP Server?

It's an adapter that lets AI agents (via the Model Context Protocol) create, modify, and validate email designs using the Beefree SDK ecosystem (Editor, Template Catalog API, Check API). It exposes a set of tools agents can call.

#### What is MCP in one sentence?

MCP is an open protocol (think "USB-C for AI") that standardizes how clients connect to servers, exposing tools, resources, and prompts over JSON-RPC.

#### **What's the difference between an MCP Server and an Agent? Does Beefree provide both?**

An MCP server exposes data or tools to AI models through a standardized interface — it provides capabilities but doesn’t make decisions. An AI agent, on the other hand, is a system that can autonomously perceive its environment, reason about goals, and take actions. Agents can use MCP servers to get information or perform tasks.

We’re providing access to the MCP Server that makes key Beefree SDK functionality accessible to AI agents. However, the host application is responsible for providing the agent. If you don’t have your own agent yet but would love to try out the MCP Server anyway, check out [our sample application using a PydanticAI agent](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo) that you can get up and running in under 5 minutes.

#### **What is the purpose of the Beefree SDK MCP Server beta?**

This will let teams explore how AI agents can integrate directly with the Beefree SDK ecosystem, designing, customizing, and validating emails programmatically, while we gather feedback and refine the experience.

#### **Which plans can access the MCP?**

At this stage, access to the MCP is invite-only as part of the early access beta. It's open to all plans, excluding free. Customers interested in joining can ask their Customer Success Manager (CSM) or fill out the waitlist form. We'll review requests and grant access to selected customers. Broader availability and plan-based access will be announced after the beta concludes.

#### **What happens to my access if I'm not selected for the beta?**

If you're not granted access right away, you'll remain on the waitlist, and we'll notify you as soon as spots open or the program expands.

#### **Who should participate in this beta?**

* Product teams exploring AI-driven content workflows&#x20;
* Developers building MCP-capable clients (e.g., IDEs, agents, assistants)&#x20;
* Teams that want to streamline design inside automated pipelines

#### **Can I use the Beefree SDK MCP in production?**

We recommend testing and prototyping only during the beta. While stable, APIs and access policies may change before general availability, and this version of the MCP server may differ from the final release.

#### **Is the MCP feature complete? What are the current limitations?**

The MCP integration is still a work in progress, and access is limited to selected customers in our early access program. While you can already use MCP to perform many email builder operations, there are some important limitations to keep in mind:

* Not all content blocks are supported yet
* Some block properties and advanced configuration options are not covered
* Functionality may change as we iterate during the beta

We encourage you to explore the available tools and share your feedback—your input will help us prioritize and close gaps as we continue to expand the MCP's capabilities.

#### **What kind of feedback are you looking for?**

We're looking for all sorts of feedback, including design capabilities and implementation:

* How easy it is to discover, understand, and use the tools available in the MCP catalog: For example, whether tool names are clear, the arguments make sense, and the set of tools feels complete for your workflow
* Coverage (are there tools you need that aren't exposed yet?)
* Performance of Template Catalog + Check API in real workflows
* Gaps in documentation or developer experience

If you have any feedback, please share it with your CSM or email beta-feedback@beefree.io.

#### **Does the MCP also support the Landing Page Builder or the Popup Builder?**

The beta currently focuses on the Beefree SDK Email Builder. Support for the Landing Page and Popup Builder is limited, but it will be considered for future updates.

#### **What is the applicable use policy?**

During the beta, you may use the MCP Server and its tools for development, prototyping, and evaluation. Access is subject to Beefree SDK's standard Terms of Service. Abuse or production-scale misuse will result in suspension of access.

#### **Is my data secure when using MCP?**

Yes. MCP calls are authenticated with secure keys, tied to your user/session, and handled in accordance with Beefree SDK's security and data policies.

#### **I have questions, feedback, or a bug to report. Who should I contact?**

Please contact your Beefree SDK Customer Success Manager (CSM) or email beta-feedback@beefree.io. We encourage feedback during beta, and your input directly shapes product improvements.

#### **Are the MCP calls free of charge?**

Yes. Calls to the MCP Server and temporary free access to the Template Catalog API and Check API are free of charge during the beta. After the beta period, normal pricing and entitlements may apply. Pricing information will be announced prior to general availability.
