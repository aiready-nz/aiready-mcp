# AIready MCP server (aiready-nz)

Official Model Context Protocol (MCP) connector for **AIready** ([aiready.nz](https://aiready.nz)), an Auckland, New Zealand AEO, GEO and agentic-commerce audit service.

- **Endpoint:** `https://aiready.nz/mcp` (Streamable HTTP)
- **Sign-in:** OAuth. Every tool needs you to sign in to your AIready account and approve the connection.
- **Server name:** `aiready-nz` · **Display name:** AIready
- **Full setup guide:** https://aiready.nz/connect

> Not affiliated with ai-ready.nz, aiready.co.nz, getaiready.now, or the `getaiready` / `@aiready/mcp-server` code-analysis package.

## Tools

| Tool | What it does | Changes anything? |
|---|---|---|
| `scan_domain` | Free passive scan of a public website: 0–100 score, readiness level, findings and any warnings | No |
| `prepare_readiness_order` | Quotes an Agentic Readiness Check (NZ$19 incl. GST or 12 USDC) with a link for a human to review and pay | No. Creates no order and takes no payment |
| `list_my_reports` | Lists your own AIready reports, newest first (up to 50) | No |
| `get_report` | Reads one of your own reports by ID | No |

## Connect

**Claude Code**
```bash
claude mcp add --transport http aiready-nz https://aiready.nz/mcp
```
## Cursor (Settings → Tools & MCP → Add Custom MCP)
```
{
  "mcpServers": {
    "aiready-nz": { "url": "https://aiready.nz/mcp" }
  }
}
```
## Claude Desktop (claude_desktop_config.json)
```
{
  "mcpServers": {
    "aiready-nz": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://aiready.nz/mcp"]
    }
  }
}
```
ChatGPT and Claude.ai custom connectors: add https://aiready.nz/mcp and follow the sign-in prompt. See https://aiready.nz/connect.

## Security and privacy

OAuth only. No API keys and no shared passwords. Never paste a browser session token.
Your data only. Report tools return only reports owned by the signed-in account.
No spending. No tool creates orders or charges payments. A human always approves a purchase.
Passive scans. scan_domain makes only standard public requests (robots.txt, sitemap, homepage, llms.txt). It doesn't store who asked.
Discovery: server card · auth reference

## About AIready
AIready helps New Zealand businesses show up in ChatGPT, Claude, Gemini and Perplexity answers. Start with a free AI scan or an Agentic Readiness Check for NZ$19 incl. GST.

Contact: hello@aiready.nz

## License
This repository and MCP server configuration documentation are licensed under the MIT License.

---


