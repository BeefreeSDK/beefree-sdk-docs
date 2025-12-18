# Beefree SDK MCP Server (Beta)

{% hint style="warning" %}
**Join the Beta program and get early access to the Beefree SDK MCP Server**

Our MCP Server is currently in Beta and only accessible to a selected number of early access customers. If you're interested in joining the Beta, or if you'd like us to notify you when the tool is available to everyone, [**please let us know**](https://growens.typeform.com/to/gyH0gVgp#source=docs).

[**I'd love to join the Beta →**](https://growens.typeform.com/to/gyH0gVgp#source=docs) \
\
&#xNAN;_&#x42;eefree SDK Team_
{% endhint %}

## Introduction

The Beefree SDK MCP Server allows you to connect your AI Agents with the Beefree SDK. It makes key functionality of the Beefree SDK — the [Editor](/broken/pages/OHBhoQNH2Zk7nqbwr3I3), our [Templates,](../apis/template-catalog-api/) or the [Check API](../apis/content-services-api/check.md) — accessible for AI agents, opening up new ways to bring agentic design directly into your application. For example, you can build agents to…<br>

* Create designs from scratch (so your users don’t have to)
* Edit and improve existing designs with the power of AI
* Build AI-powered QA workflows

…and so much more!

{% hint style="info" %}
**Important**:&#x20;

* The MCP requires a live and correctly configured editor session to function properly. Ensure your Beefree SDK editor is running with MCP enabled before attempting to use any tools.
* We’re providing access to the MCP server that makes key Beefree SDK functionality accessible to AI agents. However, providing the _agent_ is the responsibility of the Host Application. If you don’t have your own agent yet, consider this [sample application](beefree-sdk-mcp-server-beta.md#reference-sample-project) using a [PydanticAI](https://ai.pydantic.dev/) agent that you can get up and running in under 5 minutes.&#x20;
{% endhint %}

### How MCP Works

[Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro) is an open protocol that standardizes how clients (like IDEs and agent runtimes) connect to servers that expose "tools," "resources," and "prompts." Think of it as a USB-C for AI: one way to plug many tools into many agents without bespoke integrations.

At a protocol level:

* **Base protocol & lifecycle.** Clients and servers speak JSON-RPC 2.0, negotiate capabilities, and then exchange requests until shutdown. Initialization (initialize → initialized) must happen first.
* **Tools.** Servers list tools via tools/list and invoke them via tools/call. Each tool has a name and JSON Schema for inputs (and optionally outputs).
* **Metadata (\_meta).** A reserved envelope for passing extra routing/context (not tool args), namespaced as the spec requires. We'll use it to pass Beefree session routing when not using HTTP headers.
* **HTTP transport & auth.** MCP commonly runs over Streamable HTTP; authorization (when used) relies on standard HTTP bearer tokens (OAuth-style). Clients must send Authorization: Bearer and may also send the negotiated MCP-Protocol-Version header; SDKs typically handle this for you.

### Core Architecture and Components

* **CSAPI** – Public API entry point for agents. Authorizes requests and forwards them to the MCP server.
* **MCP Server** – Implements MCP and exposes tools that operate on SDK editor instances.
* **Beefree SDK Ecosystem** – Editor, Template Catalog API, Check API.

### Technical Diagram

```
AI Agent → MCP Client → CSAPI → MCP Server → Beefree SDK Ecosystem
    ↓           ↓         ↓         ↓              ↓
  Natural    JSON-RPC   Auth &   Tool Calls    Editor
 Language   Protocol   Routing   Processing   Instance
```

### Key Capabilities

The Beefree SDK MCP Server provides dozens of tools that are divided into different categories. These tools allow agents to build, modify, and validate email designs in Beefree.

#### Structure and Layout Tools

These tools control the foundational architecture of your email, allowing you to create sections, manage layouts, configure columns, and set global styles.

* `beefree_add_section` - Add new email sections with column structure
* `beefree_delete_element` - Delete elements from email templates
* `beefree_update_section_style` - Modify section styling
* `beefree_update_column_style` - Modify column styling
* `beefree_get_content_hierarchy` - Retrieve design structure
* `beefree_get_element_details` - Get element information
* `beefree_get_selected` - Get currently selected element
* `beefree_set_email_metadata` - Set email subject and preheader
* `beefree_set_email_default_styles` - Set default email styles

#### Content Block Tools

These tools add and modify individual content elements within your email, including text, images, buttons, and other interactive components.

* Text blocks: `beefree_add_title`, `beefree_add_paragraph`, `beefree_add_list`
* Media blocks: `beefree_add_image`, `beefree_add_icon`
* Interactive blocks: `beefree_add_button`, `beefree_add_social`
* Structural blocks: `beefree_add_spacer`, `beefree_add_divider`
* Each with corresponding update tools

#### Template Catalog

These tools provide access to Beefree's library of 1,500+ pre-built email templates, enabling you to browse, search, and clone professional designs as starting points.

* `beefree_list_templates` - Search and filter templates
* `beefree_retrieve_template_facets` - Get template categories and tags
* `beefree_clone_template` - Clone existing templates

#### Validation & QA Tools (Checker)

These tools verify email quality by checking for accessibility issues, missing alt text, color contrast problems, broken links, and other best practice violations.

* `beefree_check_template` - Template validation
* `beefree_check_section` - Section validation

#### External Services

These tools integrate with third-party services to enhance your email designs with external resources and assets.

The Beefree SDK MCP server uses the [Pexels API](https://www.pexels.com/api/).

* `beefree_search_stock_images` - Retrieve stock images via Pexels API integration. Search for high-quality, royalty-free images to use in your email designs. Returns image URLs, descriptions, and attribution information.

With each of the tools in the categories above, agents can build complete workflows: from inserting content, to structuring layouts, to validating designs against accessibility and best practices.

### Reference Sample Project

Reference the following sample implementation we made showcasing an mcp agent example. You can use this for inspirational and implementation purposes. The following image shows the UI of the sample project when you run it locally.

<figure><img src="../.gitbook/assets/CleanShot 2025-10-06 at 15.14.28.png" alt=""><figcaption></figcaption></figure>

Reference the [Beefree SDK MCP example demo repository](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo) to clone and run the sample project. A complete working implementation is available in this repository. The sample showcases:

* [PydanticAI](https://ai.pydantic.dev/) agent integration with MCP
* Real-time streaming chat interface
* Beefree SDK editor with MCP enabled
* WebSocket-based communication

See the project's [README.md](https://github.com/BeefreeSDK/beefree-sdk-mcp-example-demo/blob/main/README.md) for setup instructions and implementation details.

### Setup

This section discusses three key steps you need to take to successfully set up the Beefree SDK MCP Server.

These steps are:

1. [Enable the MCP editor client in the Beefree SDK Editor](beefree-sdk-mcp-server-beta.md#step-1-enable-the-mcp-editor-client-in-the-beefree-sdk-editor)
2. [Plug the MCP Server into your agent](beefree-sdk-mcp-server-beta.md#step-2-plug-the-mcp-server-into-your-agent)
3. [Route requests to the right editor instance](beefree-sdk-mcp-server-beta.md#step-3-route-requests-to-the-right-editor-instance-uid-session)

#### Step 1: Enable the MCP editor client in the Beefree SDK Editor

**What this is**: A configuration step in your host app that initializes a Beefree SDK editor instance with MCP enabled.

**How it works**: The editor exposes itself to the MCP server by setting `mcpEditorClient.enabled = true`. Optionally, `sessionId` helps distinguish multiple editor instances for the same user.

**How to use**: Add `mcpEditorClient` to your existing beeConfig object before mounting the editor.

```javascript
// Beefree SDK Editor configuration
const beeConfig = {
  container: "beefree-sdk-editor",
  mcpEditorClient: {
    enabled: true,                 // Must be true to enable MCP
    sessionId: "custom_session_id" // default: "default_session_id"
  }
};
```

{% hint style="info" %}
**Tip**: Every editor instance is identified by the Client\_id and UID pair. Use `sessionId` to ensure the right editor instance receives tool calls when the same user has multiple editor instances open (for example, you could have two editor instances tied to the same UID and Client ID but on two different browsers or PCs).
{% endhint %}

#### Step 2: Plug the MCP Server into your Agent

**What this is**: Point your MCP-capable client at the Beefree MCP endpoint with valid auth.

**How it works**: Your client performs MCP's initialize/initialized handshake over HTTP, then calls tools.

**How to use**: Send requests to the endpoint below; ensure you use an MCP-compatible CSAPI key.

```
https://api.getbee.io/v1/sdk/mcp
```

Use the HTTP header:

```
Authorization: Bearer <MCP-compatible CSAPI key>
```

{% hint style="info" %}
**Note**: A normal CSAPI key will not work. There won't be any self-service for the duration of the closed beta, so the only way to get access is to ask us to enable MCP access on an existing key or to give you a new MCP-enabled one.
{% endhint %}

Reference the [Content Services API MCP Endpoint section](beefree-sdk-mcp-server-beta.md#content-services-api-mcp-endpoint) to learn more about initializing the MCP server through the API call.

#### Step 3: Route requests to the right editor instance (UID/session)

**What this is**: Targeting information so the server knows which user's editor session to control.

**How it works**: Provide UID (required) and sessionId (optional) either via HTTP headers or in the MCP \_meta envelope.

**How to use**: Pick one of the two options below.

**Option A — HTTP headers**

```
x-bee-uid: <USER_UID>
x-bee-mcp-session-id: <SESSION_ID> (optional)
```

**Option B — \_meta object in the tool call**

```json
{
  "_meta": {
    "x-bee-uid": "<USER_UID>",
    "x-bee-mcp-session-id": "<SESSION_ID>"
  }
}
```

{% hint style="info" %}
**Note**: Use \_meta strictly for metadata/routing, not for tool arguments.
{% endhint %}

### What the MCP Actually Does

This section discusses what the MCP actually does, and provides a deeper look into what it looks like under the hood.

* **Initialize** – sends initialize with its protocol version and capabilities; server responds with its capabilities. Client then emits notifications/initialized.
* **Discover tools** – calls tools/list to see what the Beefree server offers (e.g., beefree\_add\_section, beefree\_list\_templates).
* **Call tools** – uses tools/call { name, arguments } to perform an operation. Results return as text/structured content per spec.
* **Auth and headers** – keeps the Bearer token on each request; Beefree SDK may add MCP-Protocol-Version automatically.

### Security and Requirements Recap

* **Endpoint**: https://api.getbee.io/v1/sdk/mcp
* **Auth**: Bearer token (MCP-compatible CSAPI key) in Authorization header. Tokens must be sent on every HTTP request.
* **Routing**: Provide x-bee-uid and optional x-bee-mcp-session-id either as headers or inside \_meta. Use \_meta only for metadata.
* **Editor setup**: mcpEditorClient.enabled = true (and optional sessionId).
* **MCP handshake**: Clients must complete initialize/initialized before calling tools; clients handle capability negotiation and protocol versioning.
* **Tool calls**: Use tools/call with the Beefree tool name + arguments (per tool schema).

## Content Services API MCP Endpoint

This section discusses how to use the Content services API MCP endpoint to initalize your MCP connection. It provides additional information on how to perform [Step 2](beefree-sdk-mcp-server-beta.md#step-2-plug-the-mcp-server-into-your-agent), which is plugging your agent into your MCP server, of the [Setup section](beefree-sdk-mcp-server-beta.md#setup).&#x20;

#### Initialize MCP Connection

**Method:** `POST`

**Endpoint:** `https://api.getbee.io/v1/sdk/mcp`

This endpoint allows you to establish a connection to the Beefree SDK MCP Server. This is the first call you need to make to validate your credentials and begin interacting with the MCP. A successful initialization confirms your authentication is valid and returns the server's capabilities.

**Authentication**

**Type:** Bearer Token\
**Header:** `Authorization: Bearer YOUR_MCP_COMPATIBLE_KEY`

{% hint style="info" %}
**Note:** You must use an MCP-compatible CSAPI key. Standard CSAPI keys will not work. Complete the [beta survey](https://growens.typeform.com/to/gyH0gVgp#source=docs) to request access.
{% endhint %}

**Headers**

| Header                 | Type   | Required     | Description                                                                       |
| ---------------------- | ------ | ------------ | --------------------------------------------------------------------------------- |
| `Authorization`        | string | **Required** | Bearer token with your MCP-compatible CSAPI key                                   |
| `x-bee-uid`            | string | **Required** | User identifier for routing requests to the correct editor instance               |
| `x-bee-mcp-session-id` | string | Optional     | Session identifier for distinguishing multiple editor instances for the same user |
| `Content-Type`         | string | **Required** | Must be `application/json`                                                        |

**Request Body Parameters**

The request body must be a valid JSON-RPC 2.0 request with the following structure:

**Top-level Parameters:**

| Parameter | Type    | Required     | Example Value  | Description               |
| --------- | ------- | ------------ | -------------- | ------------------------- |
| `method`  | string  | **Required** | `"initialize"` | The MCP method to call    |
| `jsonrpc` | string  | **Required** | `"2.0"`        | JSON-RPC protocol version |
| `id`      | integer | **Required** | `0`            | Request identifier        |
| `params`  | object  | **Required** | (see below)    | Initialization parameters |

**`params` Object:**

| Parameter         | Type   | Required     | Example Value  | Description          |
| ----------------- | ------ | ------------ | -------------- | -------------------- |
| `protocolVersion` | string | **Required** | `"2025-06-18"` | MCP protocol version |
| `capabilities`    | object | **Required** | (see below)    | Client capabilities  |
| `clientInfo`      | object | **Required** | (see below)    | Client information   |

**`params.capabilities` Object:**

| Parameter     | Type   | Required     | Example Value | Description                             |
| ------------- | ------ | ------------ | ------------- | --------------------------------------- |
| `sampling`    | object | **Required** | `{}`          | Sampling capabilities (empty object)    |
| `elicitation` | object | **Required** | `{}`          | Elicitation capabilities (empty object) |
| `roots`       | object | **Required** | (see below)   | Roots configuration                     |

**`params.capabilities.roots` Object:**

| Parameter     | Type    | Required     | Example Value | Description                           |
| ------------- | ------- | ------------ | ------------- | ------------------------------------- |
| `listChanged` | boolean | **Required** | `true`        | Indicates if the root list can change |

**`params.clientInfo` Object:**

| Parameter | Type   | Required     | Example Value        | Description                     |
| --------- | ------ | ------------ | -------------------- | ------------------------------- |
| `name`    | string | **Required** | `"inspector-client"` | Your client application name    |
| `version` | string | **Required** | `"0.17.1"`           | Your client application version |

**Sample Request**

```json
{"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{"sampling":{},"elicitation":{},"roots":{"listChanged":true}},"clientInfo":{"name":"inspector-client","version":"0.17.1"}},"jsonrpc":"2.0","id":0}
```

**Response**

**Success Response (200 OK)**

A successful initialization returns a JSON-RPC 2.0 response with server information and capabilities.

**Response Body Parameters:**

| Parameter | Type    | Description                                                   |
| --------- | ------- | ------------------------------------------------------------- |
| `jsonrpc` | string  | JSON-RPC protocol version (always `"2.0"`)                    |
| `id`      | integer | Matches the request ID                                        |
| `result`  | object  | Initialization result containing server info and capabilities |

**`result` Object:**

| Parameter         | Type   | Description                      |
| ----------------- | ------ | -------------------------------- |
| `protocolVersion` | string | Confirmed MCP protocol version   |
| `capabilities`    | object | Server capabilities              |
| `serverInfo`      | object | Information about the MCP server |

**`result.capabilities` Object:**

| Parameter | Type   | Description                    |
| --------- | ------ | ------------------------------ |
| `tools`   | object | Tools capability configuration |

**`result.capabilities.tools` Object:**

| Parameter     | Type    | Description                                  |
| ------------- | ------- | -------------------------------------------- |
| `listChanged` | boolean | Whether the tool list can change dynamically |

**`result.serverInfo` Object:**

| Parameter | Type   | Description               |
| --------- | ------ | ------------------------- |
| `name`    | string | Name of the MCP server    |
| `version` | string | Version of the MCP server |

**Sample Success Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 0,
  "result": {
    "protocolVersion": "2025-06-18",
    "capabilities": {
      "tools": {
        "listChanged": true
      }
    },
    "serverInfo": {
      "name": "Beefree SDK MCP Server",
      "version": "1.0.0"
    }
  }
}
```

**Error Responses**&#x20;

* **400 Bad Request - Invalid JSON-RPC Request:** Returned when the request body is malformed or doesn't follow JSON-RPC 2.0 specification.
* **401 Unauthorized - Invalid or Missing Authentication:** Returned when the Bearer token is missing, invalid, or not MCP-compatible.
* **403 Forbidden - Insufficient Permissions:** Returned when the authenticated user lacks permissions to access the MCP.
* **404 Not Found - Editor Instance Not Found:** Returned when the specified `x-bee-uid` doesn't correspond to an active editor instance.
* **500 Internal Server Error:** Returned when an unexpected server error occurs.

**Next Steps**

After successfully initializing the connection, you can:

1. List Available Tools
2. Execute Tool Calls
3. Build Your Agent

For a complete working example, see our [Reference Sample Project section](beefree-sdk-mcp-server-beta.md#reference-sample-project) above.

## Beefree SDK MCP - Frequently Asked Questions

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
