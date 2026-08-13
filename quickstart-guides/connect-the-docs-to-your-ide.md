---
description: >-
  Learn how to connect the Beefree docs to your IDE or favorite tools for
  AI-assisted developer workflows.
---

# Connect the docs to your IDE

{% hint style="warning" %}
**Important:** Are you looking for our MCP server that supports AI-generated email creation? Visit the [Beefree SDK MCP Server technical documentation](../ai-and-mcp/getting-started/), which explains how you can use our Beefree SDK MCP to create powerful email creation and editing experiences for your end users. Stay on this page if you'd like to configure the Docs MCP in your IDE for AI-assisted developer workflows.&#x20;
{% endhint %}

## Introduction

The Beefree SDK Docs MCP server exposes all the published tools and resources from our technical documentation. By connecting your IDE or assistant to this MCP server, you can:

* **Ask questions in natural language** directly from your IDE.
* **Generate code snippets** that are grounded in the Beefree SDK documentation.
* **Speed up SDK integration** by letting AI assistants pull accurate details (parameters, endpoints, setup steps) straight from the docs.
* **Reduce context-switching**—no more bouncing between browser tabs and your editor.

Overall, connecting the MCP server means you can build faster with Beefree SDK. It is useful in workflows that leverage AI-generated code based on the official Beefree SDK technical documentation.

Beefree SDK's MCP server URL is the following:

```
https://docs.beefree.io/beefree-sdk/~gitbook/mcp
```

{% hint style="info" %}
**Important:** Opening this in a browser shows an error—that’s expected. It’s for MCP clients only.
{% endhint %}

### Tool-by-Tool Setup

This section lists the most popular IDEs and tools for AI-assisted development workflows. For each tool, there are corresponding steps and code snippets on how you can connect to the Beefree SDK technical documentation MCP server using that tool.&#x20;

#### Cursor

This section lists the steps for connecting to the Beefree SDK tech docs MCP server in Cursor.

**Steps:**

1. Open **Settings → Features → MCP → + Add New MCP Server**.
2. Choose **SSE** as the transport.
3. Paste the server URL and save.
4. If needed, edit `~/.cursor/mcp.json` or project-level `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "beefree-docs": {
      "type": "sse",
      "url": "https://docs.beefree.io/beefree-sdk/~gitbook/mcp"
    }
  }
}
```

5. Restart Cursor and confirm tools appear under “beefree-docs.”

#### VS Code (GitHub Copilot)

This section lists the steps for connecting to the Beefree SDK tech docs MCP server in VS Code using GitHub Copilot.

**Steps:**

1. In your workspace, create `.vscode/mcp.json` (or configure globally via _MCP: Open User Configuration_).
2. Add the server:

```json
{
  "servers": {
    "beefree-docs": {
      "type": "http",
      "url": "https://docs.beefree.io/beefree-sdk/~gitbook/mcp"
    }
  }
}
```

3. If HTTP doesn’t connect, change `"type": "sse"`.
4. Run **MCP: Add Server** from the Command Palette if needed.

#### Claude (Desktop & Web)

This section lists the steps for connecting to the Beefree SDK tech docs MCP server using Claude.

**Steps:**

1. Open **claude.ai → Settings → Connectors** (or Claude Desktop → Settings → Connectors).
2. Click **Add remote MCP server**.
3.  Paste the server URL:

    ```
    https://docs.beefree.io/beefree-sdk/~gitbook/mcp
    ```
4. Save, then enable the tools in a chat.

#### Continue (VS Code / JetBrains)

This section lists the steps for connecting to the Beefree SDK tech docs MCP server using Continue.

**Steps (Option A – global):**

1. Open `~/.continue/config.yaml`.
2. Add:

```yaml
mcpServers:
  - name: beefree-docs
    type: sse
    url: https://docs.beefree.io/beefree-sdk/~gitbook/mcp
```

**Steps (Option B – per-workspace):**

1. Create `.continue/mcpServers/beefree-docs.yaml`.
2. Paste:

```yaml
name: Beefree Docs
version: 0.0.1
schema: v1
mcpServers:
  - name: beefree-docs
    type: sse
    url: https://docs.beefree.io/beefree-sdk/~gitbook/mcp
```

3. Restart Continue and select the Beefree Docs tools in Agent mode.

#### Cline (VS Code Extension)

This section lists the steps for connecting to the Beefree SDK tech docs MCP server using Cline

**Steps:**

1. Open **Cline → MCP Servers → Configure MCP Servers**.
2. Add this JSON:

```json
{
  "mcpServers": {
    "beefree-docs": {
      "url": "https://docs.beefree.io/beefree-sdk/~gitbook/mcp",
      "disabled": false,
      "alwaysAllow": []
    }
  }
}
```

3. For private docs, include headers:

```json
"headers": { "Authorization": "Bearer <token>" }
```

#### Zed

This section lists the steps for connecting to the Beefree SDK tech docs MCP server using Zed.

**Steps:**

1.  Install a proxy to bridge SSE/HTTP to stdio:

    ```bash
    pipx install mcp-proxy
    ```
2. Open `settings.json` in Zed.
3. Add:

```json
{
  "context_servers": {
    "beefree-docs": {
      "source": "custom",
      "command": "mcp-proxy",
      "args": [
        "https://docs.beefree.io/beefree-sdk/~gitbook/mcp",
        "--transport=streamablehttp"
      ],
      "env": {}
    }
  }
}
```

4. Restart Zed and confirm the tools are visible.

### Quick Verification

Once connected, test with a prompt like:

> “Generate a code snippet to authenticate with the Beefree SDK.”

Your IDE’s agent will pull instructions from the Beefree SDK docs and produce an AI-generated snippet aligned with the official documentation.

### Troubleshooting

* **No tools appear / “client closed”** → Restart your editor and reopen the MCP view.
* **VS Code transport issues** → Use `"http"` first, fallback to `"sse"`.
* **Zed** → Must use a proxy (`mcp-proxy`) to connect.

### References

* [Beefree SDK Docs MCP Server URL](https://docs.beefree.io/beefree-sdk/~gitbook/mcp)
* [Visual Studio Code MCP Documentation](https://code.visualstudio.com/)
* [Cursor Community Forum (MCP Config)](https://cursor.directory/)
* [Claude Connectors Documentation](https://support.anthropic.com/)
* [Continue Documentation](https://continue.dev/)
* [Cline Documentation](https://marketplace.visualstudio.com/items?itemName=cline)
* [Zed Documentation](https://zed.dev/)
* [mcp-proxy on PyPI](https://pypi.org/project/mcp-proxy)
