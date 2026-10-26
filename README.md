# AIready NZ — Model Context Protocol (MCP) Server

[![Website](https://img.shields.io/badge/Website-aiready.nz-dfff5c?style=flat-square)](https://aiready.nz)
[![MCP Endpoint](https://img.shields.io/badge/MCP-Remote%20Streamable%20HTTP-121212?style=flat-square&logo=cloudflare)](https://aiready.nz/mcp)
[![Auckland NZ](https://img.shields.io/badge/Region-Auckland%2C%20New%20Zealand-blue?style=flat-square)](https://aiready.nz)

The official **Model Context Protocol (MCP)** server for [AIready](https://aiready.nz), Auckland's AI visibility, Answer Engine Optimisation (AEO & GEO), and agentic commerce auditing service.

This server enables AI assistants (Claude, Cursor, Windsurf, ChatGPT) to audit websites for AI discoverability, quote Agentic Readiness checks, and retrieve customer reports directly through standardized tools.

---

## 🛠️ Available MCP Tools

| Tool | Description | Auth Required? |
| :--- | :--- | :--- |
| `scan_domain` | Runs a free, passive 30s scan of any public domain (AEO/GEO readiness, bot policies, structured data). | No (Free) |
| `prepare_readiness_order` | Calculates a pricing quote and generates a human-approval intake URL for an Agentic Readiness Check. | No (Quote only) |
| `list_my_reports` | Lists all completed readiness audit reports associated with the authenticated user. | Yes (OAuth / Sign-in) |
| `get_report` | Fetches full JSON audit findings and priority fixes for a specific report ID. | Yes (OAuth / Sign-in) |

---

## 🚀 Quick Start: Connect in Claude Desktop

Add this configuration to your Claude Desktop config file:

### Configuration (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "aiready": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-fetch",
        "https://aiready.nz/mcp"
      ]
    }
  }
}
