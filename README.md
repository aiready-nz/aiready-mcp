# AIready MCP Server

Official Model Context Protocol (MCP) server for **AIready** ([aiready.nz](https://aiready.nz)). 

Connect your AI assistants (Claude Desktop, Cursor, Zed, Windsurf, or custom agent frameworks) directly to AIready's New Zealand business AI-readiness audit and optimization tools.

[![MCP Protocol](https://img.shields.io/badge/MCP-1.0-blue.svg)](https://modelcontextprotocol.io/)
[![Server Type](https://img.shields.io/badge/transport-Streamable%20HTTP-success)](https://aiready.nz/mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Origin](https://img.shields.io/badge/Made%20in-Auckland%2C%20New%20Zealand-red)](https://aiready.nz)

---

## What is AIready?

AIready helps New Zealand businesses get discovered, cited, and recommended by AI answer engines and autonomous agents (AEO, GEO, and Agentic Commerce). 

This MCP server provides a standardized interface for AI models to:
1. Passively inspect any website for AI crawler access, structured data, and agent readiness.
2. Prepare structured readiness audit orders for human review.
3. Access verified client audit reports via secure OAuth.

---

## Available Tools

| Tool Name | Access | Description |
|---|---|---|
| `scan_domain` | **Public** | Runs a live, passive audit of any domain against AI crawler rules, `llms.txt`, JSON-LD schemas, and DNS configuration. Returns a 0–100 score and priority fixes. |
| `prepare_readiness_order` | **Public** | Generates an uncommitted audit order quote (NZ$ or USDC) with checkout links for human approval. Zero autonomous charging. |
| `list_my_reports` | **Authenticated** | Lists completed AI Readiness audit reports belonging to the signed-in user. |
| `get_report` | **Authenticated** | Retrieves full audit findings and recommendations for a specific report ID. |

---

## Connection & Setup

This server is hosted as a **Streamable HTTP MCP Server** at:
https://aiready.nz/mcp

### 1. Claude Desktop Setup

Add the following to your `claude_desktop_config.json`:

- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`

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
