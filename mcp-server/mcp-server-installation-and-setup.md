# MCP Server installation & setup

{% hint style="danger" %}
**MCP Server v1 is deprecated**

The v1 editor client approach (`mcpEditorClient.enabled = true` + <kbd>/v1/sdk/mcp</kbd> endpoint) is deprecated and will be removed on September 1, 2026. New integrations must use the v2 setup described on this page. If you are on v1, see [Migrating from v1](mcp-server-installation-and-setup.md#migrating-from-v1).
{% endhint %}

### Overview

[Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro) is an open protocol that standardizes how AI agents connect to services that expose tools, resources, and prompts — a universal interface that lets you plug any agent into any integration without bespoke code.

The Beefree SDK MCP Server exposes the editor, and Check API as callable tools. When the agent makes a change, it is pushed to the editor in real time — the user sees the template update live as the agent works, if the builder is open.

### Choose your integration path

{% hint style="info" %}
Beefree SDK's MCP Server support both in-editor and headless use-cases. If you are integrating the MCP in a headless setup, you can follow the [API-managed session](mcp-server-installation-and-setup.md#api-managed-session) path below skipping the third step "Connect the editor"
{% endhint %}

There are two ways to connect your agent to the editor. The right choice depends on whether [co-editing](../other-customizations/collaborative-editing/) is enabled on your account:

* [Co-editing](../other-customizations/collaborative-editing/) **not enabled** → [Editor-managed session](mcp-server-installation-and-setup.md#editor-managed-session): the editor creates a lightweight temporary session on demand via `bee.startMcpSession()`. No backend session management required.
* [Co-editing](../other-customizations/collaborative-editing/) **enabled** → [API-managed session](mcp-server-installation-and-setup.md#api-managed-session): your host application creates and manages the session lifecycle via the Headless API. Supports multiple concurrent users, presence indicators, per-change history, and persistent sessions.

Both paths use the same MCP endpoint and authentication. They differ only in how the session and templateId are created.

### Core architecture

```
AI Agent → MCP Client → CSAPI → MCP Server → Beefree SDK Ecosystem (optional)
    ↓           ↓         ↓          ↓               ↓
  Natural    JSON-RPC   Auth &   Tool Calls       Editor /
 Language   Protocol   Routing   Processing      Check API

```

* **CSAPI** — public API entry point for your agent. Authenticates requests and routes them to the MCP server.
* **MCP Server** — implements the MCP protocol and exposes tools that operate on Beefree SDK resources.
* **Beefree SDK Ecosystem** — the Editor, and Check API.

At a protocol level:

* **Base protocol & lifecycle.** Clients and servers speak JSON-RPC 2.0, negotiate capabilities, and then exchange requests until shutdown. Initialization (initialize → initialized) must happen first.
* **Tools.** Servers list tools via tools/list and invoke them via tools/call. Each tool has a name and JSON Schema for inputs (and optionally outputs).
* **Metadata (\_meta).** A reserved envelope for passing extra routing/context (not tool args), namespaced as the spec requires. We'll use it to pass Beefree session routing when not using HTTP headers.

{% hint style="info" %}
Since the Beefree SDK MCP Server relies on Beefree's CSAPI, it is subjected to the same rate limits. [Learn more here](../apis/content-services-api/).
{% endhint %}

### Prerequisites

#### Get an MCP-compatible CSAPI key

All requests to the MCP endpoint require a valid [CSAPI key](../apis/content-services-api/#overview-of-content-services-api). You can enable your CSAPI Key from your SDK Console.

Once you have a key, include it in every request:

```
Authorization: Bearer <YOUR_CONTENT_SERVICES_API_KEY>
```

#### MCP endpoint

All agent connections use the v2 endpoint:

```
https://api.getbee.io/v2/sdk/mcp
```

Your agent must complete the MCP `initialize/initialized` handshake before calling any tools. MCP clients (SDKs, runtimes) typically handle this automatically.

### Editor-managed session

{% hint style="warning" %}
Use this path when [**co-editing**](../other-customizations/collaborative-editing/) **is not enabled on your account**, or when you want a simpler setup where the editor manages the session lifecycle on your behalf.
{% endhint %}

The session is temporary and scoped to a single user and their agent(s). If you have the co-edit enabled, please refer to the API-managed session for the setup.

#### Step 1: Configure the editor

No additional editor configuration is required beyond your standard Beefree SDK setup. The relevant fields for MCP sessions are covered in [Editor Configuration](mcp-server-installation-and-setup.md#editor-configuration) below.

#### Step 2: Start a session

When the user is ready to involve the agent, your host application calls:

```javascript
const { templateId } = await bee.startMcpSession();
```

The editor creates an MCP session server-side and returns a `templateId`. Pass this to your agent(s).

#### Step 3: Connect your agent

Connect to the v2 MCP endpoint using the `templateId` from Step 2, exactly as in the API-managed path:

```
x-bee-template-id: <templateId>
```

The agent connects and can immediately begin editing the template.

#### Step 4: End the session

The session ends automatically when agent work is complete (see [When the Session Ends Automatically](mcp-server-installation-and-setup.md#when-the-session-ends-automatically))

Automatic stop means: history entry creation, connection teardown, and a `SESSION_ENDED` event.

#### Session participants

An editor-managed MCP session supports exactly one real user — the person using the editor — and any number of AI agents.

* The real user stays connected throughout the entire session.
* One or more agents join via the MCP server using the `templateId`.
* A second real (non-agent) user cannot join. If one does, the session stops automatically.

The automated disconnect logic relies on this model: once at least one agent has joined and then all agents leave, only the real user remains. The editor treats this as "all agents have finished their work" and automatically ends the session.

#### When the session ends automatically

The session ends automatically when any of the following occur:

* **All agents leave** (only the real user remains) — the editor treats this as agent work being complete.
* **The 10-minute client timeout expires** — a hard limit regardless of agent activity.
* **A second real user (non-agent) joins** the session.
* **A new template is loaded** into the editor.

#### History behavior

During an editor-managed MCP session, individual agent modifications are not tracked as separate history entries. Instead, the editor captures the full template state before the session starts and, upon the session end, creates a single history entry representing the diff between the original and final states.

This means users can undo the entire batch of agent changes as one unit, but cannot step through individual agent edits.

#### Session lifecycle

An editor-managed session is ephemeral. Once it ends — by timeout, automated-stop, or manual stop — it cannot be resumed. To start another agent pass on the same template, call `bee.startMcpSession()` again. Each call creates a fresh session with its own `templateId`, timeout and history entry.

#### Error handling

If `bee.startMcpSession()` fails, the error is returned in this shape:

```json
{
  "error": {
    "code": "<code>",
    "message": "<description>"
  }
}
```

Common failure scenarios:

* **Builder not ready** — the editor has not finished initializing.
* **API error** — the server-side session creation request failed.

### API-managed session

{% hint style="warning" %}
Use this path when [**co-editing**](../other-customizations/collaborative-editing/) **is enabled on your account**.
{% endhint %}

Your host application controls the full session lifecycle: you create the template, connect the agent, and optionally connect the editor — all independently.

#### Step 1: Create a template

Call the template creation endpoint to initialize a new editing session server-side. You receive a `templateId` that you will pass to the agent in the next step.

**Endpoint**

```
POST https://api.getbee.io/v2/sdk/mcp/template
```

**Request body**

| Field     | Type   | Description                                                 |
| --------- | ------ | ----------------------------------------------------------- |
| template  | object | Optional. The JSON template to initialize the session with. |
| mergeTags | object | Optional. Merge tags to be resolved within the template.    |

```json
{
  "template": { ... },
  "mergeTags": { ... }
}
```

**Response**

Returns a templateId. You must pass this as the `x-bee-template-id` header (or `_meta` field) when connecting to the MCP endpoint.

#### Step 2: Connect your agent

Point your MCP client at the v2 endpoint and provide the `templateId` you received in Step 1. You can pass it in one of two ways:

**Option A — HTTP header (recommended)**

<pre><code><strong>x-bee-template-id: &#x3C;templateId>
</strong></code></pre>

**Option B — `_meta` field in the MCP `initialize` request**

```json
{
  "method": "initialize",
  "params": {
    "_meta": {
      "x-bee-template-id": "<templateId>"
    }
  }
}
```

Use `_meta` strictly for routing metadata, not for tool arguments.

#### Step 3: Connect the editor (optional)

The editor can join the same session for [real-time collaboration](../other-customizations/collaborative-editing/) alongside the agent. To configure this, use the `join` method in the editor configuration.

```
bee.join(templateId);
```

#### Step 4: Retrieve the final template

After the agent has finished its work, fetch the modified template from the server:

```
GET https://api.getbee.io/v2/sdk/mcp/template/:templateId
```

This returns the current state of the template with all agent modifications applied.

#### Agent locking behavior

When an agent shares a session with human users, module locks — the mechanism that prevents two users from editing the same module simultaneously — interact with the agent differently depending on whether it has an assigned owner.

The agent's owner is determined by the `x-bee-user-handle` header passed when the agent connects to the MCP server. If that value matches an existing `userHandle` value in the session, that user becomes the agent's owner.

**Agent without an owner** (`x-bee-user-handle` is absent or does not match any session user):

* The agent ignores all locks and can override any module regardless of who is currently editing it.

**Agent with an owner** (`x-bee-user-handle` matches a session user's `userHandle`):

* The agent can replace locks held by its owner — it acts on behalf of that user.
* The agent honors locks held by other users and will not override modules they are editing.

Assigning an owner is recommended in sessions with multiple real users. It ensures the agent respects the collaborative editing boundaries of other participants.

#### Editor configuration

For the full `editorConfig` reference and co-editing setup, see the [Co-Editing Integration Guide](../other-customizations/collaborative-editing/).

The following fields are relevant to MCP sessions across both integration paths:

```
{
  "username": "Display name shown for this user in the editor",
  "userHandle": "Unique identifier for this user",
  "userColor": "#hex color for the user's presence indicator"
}
```

`userHandle` behavior

* If `userHandle` is provided, it is used as the user's identity in the co-editing session.
* If `userHandle` is omitted in an editor-managed session, the editor auto-generates one as `mcp-{randomUUID}`, ensuring a unique identity without requiring the host to manage it.
* In an API-managed session, `userHandle` is also used to match an agent's owner via the `x-bee-user-handle header` (see [Agent locking behavior](mcp-server-installation-and-setup.md#agent-locking-behavior)).

### Host callbacks: `onMcpSessionChange`

The **editor-managed session** exposes a set of callbacks that serve as the co-editing equivalents of `onSessionChange` and `onSessionStarted`.

<table data-header-hidden><thead><tr><th width="184">Event</th><th>Payload</th><th>When it fires</th></tr></thead><tbody><tr><td><code>SESSION_STARTED</code></td><td><code>{ type, templateId }</code></td><td>Connection successfully established</td></tr><tr><td><code>USER_JOINED</code></td><td><code>{ type, change, sessionData }</code></td><td>A new user enters the session</td></tr><tr><td><code>USER_LEFT</code></td><td><code>{ type, change, sessionData }</code></td><td>A user leaves the session</td></tr><tr><td><code>SESSION_ENDED</code></td><td><code>{ type, templateId }</code></td><td>The session stops</td></tr></tbody></table>

### Server-Side session TTL

These values define how long session data persists on the backend, independently of any client-side timeouts.

**API-managed session**

| Users still active              | 33h, reset on every keep-alive or write | Never, as long as keep-alives arrive |
| ------------------------------- | --------------------------------------- | ------------------------------------ |
| Last user leaves                | Set to 24h                              | 24h after last user disconnects      |
| Idle (no writes or keep-alives) | Last set value (up to 33h)              | At TTL expiry                        |

**Editor-managed session**

| Users still active              | 1h, reset on every keep-alive | Never, as long as keep-alives arrive |
| ------------------------------- | ----------------------------- | ------------------------------------ |
| Last user leaves                | Set to 5 min                  | 5 min after last user disconnects    |
| Idle (no writes or keep-alives) | Last set value (up to 1h)     | At TTL expiry                        |

{% hint style="info" %}
The editor-managed session also enforces a hard **10-minute client-side timeout** that disconnects the editor regardless of server-side TTL. This is the most common expiry path in practice.
{% endhint %}

### Security

* **Key protection**: Never expose your CSAPI keys in client-side code or public repositories.
* **Secure transport**: Always use the provided HTTPS gateway for all MCP interactions.
* **Validation**: Ensure your MCP client correctly handles the `_meta` field and authentication headers.

We strongly recommend reviewing the official [MCP Client documentation](https://modelcontextprotocol.io/docs/learn/client-concepts) for guidance on transport, lifecycle, and security.

### Code examples

In the [Beefree SDK MCP v2 demo repository](https://github.com/BeefreeSDK/beefree-sdk-mcp-v2-example-demo), you can find:

* An example of an editor-managed session
* An example of an API-managed session
* A Code Mode example

### Code mode

{% hint style="success" %}
**Try Code Mode for Beefree SDK's MCP Server**

Code Mode is currently in open beta and rolling out to all customers with Essentials, Core, Superpowers and Enterprise plans.&#x20;
{% endhint %}

Code Mode is an alternative way to interact with the Beefree SDK MCP Server that significantly **reduces token consumption**.

Instead of exposing 33 individual tools — each with a full parameter schema sent on every turn — Code Mode exposes a single tool that accepts a TypeScript script. Your agent writes one script that performs all operations in a single round trip: creating sections, adding content, and setting styles.

**Code mode endpoint**

```
https://api.getbee.io/v2/sdk/mcp/codemode
```

In internal benchmarks across five models and three email complexity levels, Code Mode reduced total token consumption by 68–96%, with most results in the 85–95% range ([learn more in our blogpost](https://developers.beefree.io/blog/ai-agents-email-saving-tokens#code-mode))

Use Code Mode when your agent makes many sequential tool calls to reduce API costs and latency.&#x20;

**Please note**: Code Mode requires your agent to generate valid TypeScript. Implement error handling to gracefully handle partial failures.

### Migrating from v1

The v1 approach used `mcpEditorClient.enabled = true` in the `beeConfig` object to expose the editor to the MCP server, combined with the `/v1/sdk/mcp` endpoint and `x-bee-uid / x-bee-mcp-session-id` headers for routing.

In the current MCP server version (v2), the session is identified by a `templateId` rather than a `uid` + session pair, and the endpoint has moved to `/v2/sdk/mcp`. The same CSAPI key credentials continue to work — no new credentials are required.

**Key changes**

|                  | v1 (deprecated)                                      | Current MCP (v2)                                                                                                                                                                                                   |
| ---------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Architecture     | Requires a running Beefree SDK Editor in the browser | Session can be created via the Headless API or by the editor via `startMcpSession()`                                                                                                                               |
| Session identity | `client_id` + `uid` + optional `session_id`          | `templateId`                                                                                                                                                                                                       |
| Endpoint         | `https://api.getbee.io/v1/sdk/mcp`                   | `https://api.getbee.io/v2/sdk/mcp`                                                                                                                                                                                 |
| Routing header   | `x-bee-uid, x-bee-mcp-session-id`                    | `x-bee-template-id`                                                                                                                                                                                                |
| Editor config    | `mcpEditorClient: { enabled: true }`                 | Not required for agent connection                                                                                                                                                                                  |
| Select element   | `beefree_get_selected`                               | `onSelectElement` callback ([more details here](https://app.gitbook.com/o/2zoWGxtV7bjhbwBdjGPS/s/8c7XIQHfAtM23Dp3ozIC/~/edit/~/changes/572/mcp-server/tools-and-capabilities#get-the-context-of-selected-element)) |

{% include "../.gitbook/includes/remove-the-mcpeditorclient-....md" %}
