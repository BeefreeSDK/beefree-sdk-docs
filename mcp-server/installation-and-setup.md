# Installation & Setup

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

{% hint style="info" %}
Since the Beefree SDK MCP Server relies on Beefree's CSAPI, it is subjected to the same rate limits. [Learn more here](https://docs.beefree.io/beefree-sdk/apis/content-services-api#rate-limits).
{% endhint %}

### Setup

This section discusses three key steps you need to take to successfully set up the Beefree SDK MCP Server.

These steps are:

1. [Enable the MCP editor client in the Beefree SDK Editor](installation-and-setup.md#step-1-enable-the-mcp-editor-client-in-the-beefree-sdk-editor)
2. [Plug the MCP Server into your agent](installation-and-setup.md#step-2-plug-the-mcp-server-into-your-agent)
3. [Route requests to the right editor instance](installation-and-setup.md#step-3-route-requests-to-the-right-editor-instance-uid-session)

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

Reference the [Content Services API MCP Endpoint section](installation-and-setup.md#content-services-api-mcp-endpoint) to learn more about initializing the MCP server through the API call.

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

This section discusses how to use the Content services API MCP endpoint to initalize your MCP connection. It provides additional information on how to perform [Step 2](installation-and-setup.md#step-2-plug-the-mcp-server-into-your-agent), which is plugging your agent into your MCP server, of the [Setup section](installation-and-setup.md#setup).&#x20;

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

**Sample Request**

```json
{"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{"sampling":{},"elicitation":{},"roots":{"listChanged":true}},"clientInfo":{"name":"inspector-client","version":"0.17.1"}},"jsonrpc":"2.0","id":0}
```

**Next Steps**

After successfully initializing the connection, you can:

1. List Available Tools
2. Execute Tool Calls
3. Build Your Agent

For a complete working example, see our [Sample Project](https://app.gitbook.com/o/2zoWGxtV7bjhbwBdjGPS/s/8c7XIQHfAtM23Dp3ozIC/~/preview/~/changes/506/mcp-server/beefree-sdk-mcp-server-beta).
