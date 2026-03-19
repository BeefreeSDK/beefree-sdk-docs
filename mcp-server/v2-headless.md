# MCP Server v2 | Headless

The new Beefree SDK MCP Server v2 introduces a **fully headless architecture**. While v1 relies on an active browser-based editor session, v2 handles operations entirely server-side. By removing the dependency on a live editor instance, v2 enables more robust, automated workflows.

The MCP Server v2 is at the moment optimized only for headless use cases. For any implementations requiring a frontend, browser-based editor UI, please continue to use the [MCP Server v1](https://docs.beefree.io/beefree-sdk/mcp-server/getting-started). We are actively developing v2 to support all use cases—including frontend integrations—in the near future.

{% hint style="warning" %}
Beefree SDK MCP v2 is currently in an invite-only Closed Beta. Access is restricted to selected partners at this time. If you are interested in joining the waitlist or learning more about the roadmap, please [fill in this form](https://growens.typeform.com/to/gyH0gVgp#source=docs) or reach out to your CSM.
{% endhint %}

## Use Cases <a href="#comparison-v1-vs-v2" id="comparison-v1-vs-v2"></a>

By shifting to a server-side, headless architecture, Beefree SDK MCP v2 enables **high-scale automation** and **seamless integration** with your existing DevOps or marketing stack. Key use cases include:

* **Bulk Generation**: Programmatically generate unique email variants simultaneously. This is ideal for large-scale campaigns where manual intervention in a browser is not feasible.
* **Iterative Variation**: Automatically produce a series of design or layout variations based on a single master template. This allows for rapid A/B testing or content experimentation powered entirely by backend scripts or AI agents.
* **External Ecosystems**: Seamlessly trigger template modifications via third-party automation platforms. By removing the frontend dependency, you can now integrate Beefree SDK actions directly into workflows in tools like n8n, Zapier, Make, Retool, Tines and others.

### Try the MCP Server v2 with our Sample Project <a href="#try-the-mcp-server-with-our-sample-project" id="try-the-mcp-server-with-our-sample-project"></a>

See yourself a real-world, fully functioning example with this Beefree SDK MCP v2 sample agent. Simply plug in your preferred provider whether you're team Gemini, OpenAI, or Anthropic, and test 5 different use cases.

{% hint style="warning" %}
Using an email building agent can generate LLM API costs, and it's important to be aware of this. We've included a token counter in the sample project to help you keep track of usage and spending.
{% endhint %}

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

You can visit the [Beefree SDK MCP v2 example demo GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-mcp-v2-example-demo) to clone and run the sample project.

## Comparison v1 vs v2 <a href="#comparison-v1-vs-v2" id="comparison-v1-vs-v2"></a>

|                            | v1 (Front-End Editor)                                | v2 (Headless)                                           |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------- |
| **Architecture**           | Requires a running Beefree SDK Editor in the browser | Fully server-side, doesn't require a running SDK Editor |
| **Session initialization** | Editor connects via `mcpEditorClient` in bee config  | Host application provides the Template ID               |
| **Session identity**       | `client_id` + `uid` + optional `session_id`          | Template ID                                             |
| **Required client params** | `client_id`, `uid` (from CSAPI key + headers)        | Template ID (`x-bee-template-id`)                       |
| **Endpoint**               | `<https://api.getbee.io/v1/editor/mcp>`              | `<https://api.getbee.io/v2/sdk/mcp>`                    |
| **Transport**              | Streamable HTTP (stateless)                          | Streamable HTTP (stateful, with session management)     |
| **Total tools**            | 40                                                   | 33                                                      |

## Installation & Setup

### CSAPI Integration

MCP v2 continues to use CSAPI as the public API layer for all host application connections. To ensure a seamless transition, the API keys for the MCP v2 endpoint are identical to those used in v1. No action is required from existing beta participants to update or replace their current credentials.

{% hint style="info" %}
Since the Beefree SDK MCP Server relies on Beefree's CSAPI, it is subjected to the same rate limits. [Learn more here](https://docs.beefree.io/beefree-sdk/apis/content-services-api#rate-limits).
{% endhint %}

### Getting Started

#### **Authentication**

Authentication is handled at the API gateway layer. All requests to the MCP v2 endpoints must include a valid CSAPI key in the authorization header.

#### Template Management <a href="#template" id="template"></a>

Before connecting to the MCP, clients need to create a template and obtain a `template` ID. You can use two endpoints for template lifecycle management:

**Create Template Endpoint**

`POST https://api.getbee.io/v2/sdk/mcp/template`

**Request body:**

```javascript
{
  "template": { ... },
  "mergeTags": { ... }
}
```

<table data-header-hidden><thead><tr><th>Field</th><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>template</code></td><td>object</td><td><em>Optional.</em> The JSON template to initialize the editing session.</td></tr><tr><td><code>mergeTags</code></td><td>object</td><td><em>Optional</em>. Merge tags to be resolved within the template.</td></tr></tbody></table>

**Response:** Returns a `templateId`  in the response payload. You must pass this as the `x-bee-template-id` parameter when connecting to the MCP headless endpoint.

**Retrieve Template Endpoint**

Fetches the current state of the template. Call this after the MCP session to get the final template with all modifications applied by the AI agent.

```
GET https://api.getbee.io/v2/sdk/mcp/template/:templateId
```

### MCP Server Implementation

#### MCP Endpoint

The Beefree SDK MCP v2 server utilizes a Streamable HTTP transport and is accessible via the Beefree API Gateway at:

```
https://api.getbee.io/v2/sdk/mcp
```

#### Required Parameters

To successfully initialize a session, the client must provide a `templateId`. You can provide the `templateId` in one of two ways:

1\. **HTTP Header** (recommended)

```
x-bee-template-id: <template-id>
```

2\. `_meta` field in the MCP `initialize` request:

```javascript
{
  "method": "initialize",
  "params": {
    "_meta": {
      "x-bee-template-id": "<template-id>"
    }
  }
}
```

### End-to-End Workflow <a href="#typical-workflow" id="typical-workflow"></a>

1. **Create** a template via `POST /v2/sdk/mcp/template` and receive a `templateId`
2. **Connect** to the MCP at `/v2/sdk/mcp` passing the `templateId` via `x-bee-template-id`
3. **Use MCP tools** to modify the template through the agent
4. **Retrieve** the final template via `GET /v2/sdk/mcp/template/:templateId`

### Client Compatibility & Security

To ensure a stable and secure connection with the Beefree SDK MCP v2 server, we suggest you use use a supported MCP client.&#x20;

{% hint style="info" %}
We strongly recommend reviewing the official [MCP Client](https://modelcontextprotocol.io/docs/learn/client-concepts) documentation to understand how clients manage transport, lifecycle, and security.
{% endhint %}

Security Best Practices:

* **Key Protection**: Never expose your CSAPI keys in client-side code or public repositories.
* **Secure Transport**: Always use the provided HTTPS gateway for all MCP interactions to ensure end-to-end encryption.
* **Validation**: Ensure your chosen client correctly handles the `_meta` field and authentication headers.

### Available Tools <a href="#available-tools" id="available-tools"></a>

<table><thead><tr><th width="297">Tool</th><th width="204">Category</th><th width="63">v1</th><th>v2</th></tr></thead><tbody><tr><td><code>beefree_add_section</code></td><td>Layout &#x26; Structure</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_delete_element</code></td><td>Layout &#x26; Structure</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_section_style</code></td><td>Layout &#x26; Structure</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_column_style</code></td><td>Layout &#x26; Structure</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_get_selected</code></td><td>Editor Sync</td><td>✅</td><td>replaced*</td></tr><tr><td><code>beefree_get_content_hierarchy</code></td><td>Content Analysis</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_get_element_details</code></td><td>Content Analysis</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_paragraph</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_paragraph</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_title</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_title</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_list</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_list</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_menu</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_menu</code></td><td>Text Content</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_image</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_image</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_button</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_button</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_social</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_social</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_icon</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_icon</code></td><td>Media &#x26; Interactive</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_spacer</code></td><td>Separators</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_spacer</code></td><td>Separators</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_divider</code></td><td>Separators</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_divider</code></td><td>Separators</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_add_table</code></td><td>Tables</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_update_table</code></td><td>Tables</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_set_email_metadata</code></td><td>Email Settings</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_set_email_default_styles</code></td><td>Email Settings</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_check_template</code></td><td>Validation &#x26; QA</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_check_section</code></td><td>Validation &#x26; QA</td><td>✅</td><td>✅</td></tr><tr><td><code>beefree_retrieve_template_facets</code></td><td>Template Catalog</td><td>✅</td><td>deprecated</td></tr><tr><td><code>beefree_list_templates</code></td><td>Template Catalog</td><td>✅</td><td>deprecated</td></tr><tr><td><code>beefree_clone_template</code></td><td>Template Catalog</td><td>✅</td><td>deprecated</td></tr><tr><td><code>beefree_search_stock_images</code></td><td>External Services</td><td>✅</td><td>✅</td></tr></tbody></table>

\*The `beefree_get_selected` tool has been replaced by a new event callback `onSelectElement`. This callback is triggered when a user selects either a row or a module in the SDK interface. It is called with an object parameter that contains:

* a `type` field, which can be either `module` or `row`
* a `uuid` field, which contains the ID of the selected element

This information is meant to be forwarded to your AI Agent that can proactively leverage them in MCP-powered content creation.
