# AIready MCP Server (`aiready-nz`)

[![MCP](https://img.shields.io/badge/MCP-1.0-brightgreen.svg)](https://modelcontextprotocol.io/)
[![OAuth 2.0](https://img.shields.io/badge/Auth-OAuth%202.0-blue.svg)](https://aiready.nz/connect)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status](https://img.shields.io/badge/Status-Live-success.svg)](https://aiready.nz/mcp)

The official [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server for **[AIready](https://aiready.nz)**. 

This server allows AI assistants (Claude Desktop, Cursor, ChatGPT, and custom autonomous agents) to scan New Zealand websites for AI readiness (AEO, GEO, agentic commerce), retrieve previous audits, and prepare readiness orders.

- **Server ID:** `aiready-nz`
- **MCP Endpoint:** `https://aiready.nz/mcp`
- **Transport:** Streamable HTTP (SSE)
- **Authentication:** OAuth 2.0 Protected Resource (Customer-scoped)

---

## Available Tools

| Tool | Access | Description |
| :--- | :--- | :--- |
| `scan_domain` | **Public** | Runs a live, passive AI readiness check on any domain and returns a score (0–100), letter grade (A–F), and category breakdowns. |
| `prepare_readiness_order` | **OAuth Required** | Prepares a formal readiness check order for customer intake (`NZ$195 incl. GST` or `1 USDC` test). Does **not** charge cards or spend funds automatically. |
| `list_my_reports` | **OAuth Required** | Lists all previous audit reports owned by the authenticated user. Protected by Row-Level Security (RLS). |
| `get_report` | **OAuth Required** | Retrieves the full structured JSON findings for a specific report owned by the authenticated caller. |

---

## Quick Setup

### 1. Claude Desktop

Add `aiready-nz` to your Claude Desktop configuration file:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "aiready": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://aiready.nz/mcp"
      ]
    }
  }
}
```
*Restart Claude Desktop. When you start a chat, you will see the hammer icon with `aiready` tools available.*

---

### 2. Cursor IDE

In Cursor:
1. Open **Settings** (`Cmd+,` or `Ctrl+,`) → **Features** → **MCP**.
2. Click **+ Add New MCP Server**.
3. Fill in:
   - **Name:** `aiready`
   - **Type:** `command`
   - **Command:** `npx -y mcp-remote https://aiready.nz/mcp`
4. Refresh the server list.

---

## Security & Privacy Guarantees

AIready follows strict zero-trust standards for agentic connections:

1. **Zero Autonomous Spending:** `prepare_readiness_order` creates a draft order requiring explicit human intake approval and Stripe/Solana customer signature. The AI cannot charge cards or move crypto funds on its own.
2. **Customer-Scoped Data:** Private reports are protected by Row-Level Security (RLS). An agent with OAuth token A can **never** see or list reports belonging to token B.
3. **Passive Scanning Only:** `scan_domain` only makes standard passive HTTP requests to publicly visible endpoints (`robots.txt`, `llms.txt`, DNSSEC, sitemaps). It never runs vulnerability probes, penetration tests, or intrusive scans.
4. **No Master Keys:** The MCP server never uses or exposes service-role database keys. All queries run strictly within the caller's authorized permissions.

---

## About AIready

[AIready](https://aiready.nz) is an Auckland-based agency helping New Zealand businesses prepare for:

- **AEO (Answer Engine Optimisation):** Ranking in Perplexity, ChatGPT Search, and Copilot.
- **GEO (Generative Engine Optimisation):** Structured data and authority citations for AI summary engines.
- **Agentic Commerce:** Machine-readable product discovery, MCP servers, and agent-ready checkout systems.

### Free Resources
- [Free Instant AI Readiness Scan](https://aiready.nz/)
- [Agent Discovery Manifest (`llms.txt`)](https://aiready.nz/llms.txt)
- [OAuth Discovery Details](https://aiready.nz/connect)

---

## License

This repository and MCP server configuration documentation are licensed under the [MIT License](https://opensource.org/licenses/MIT).
