# BugiaData MCP

**Relational fake data for AI editors** — locale-aware, foreign keys intact, one API key.

BugiaData is a **hosted remote MCP server**. You do not clone or run this repository to use the tools; it exists for **documentation and directory listings** (cursor.store, MCP Registry). The server runs at [bugiadata.com](https://bugiadata.com).

| | |
|---|---|
| **MCP endpoint** | `https://mcp.bugiadata.com/sse` |
| **Auth** | HTTP header `X-API-Key` (from your [dashboard](https://bugiadata.com/dashboard?tab=mcp)) |
| **Discovery** | [bugiadata.com/mcp](https://bugiadata.com/mcp) |
| **Signup** | [bugiadata.com/signup](https://bugiadata.com/signup) (free tier: 10k tokens/month) |

## Tools

| Tool | Description |
|------|-------------|
| `ping` | Health check; returns tier and key hint |
| `whoami` | Account tier and monthly token usage |
| `generate_data` | Single Faker type batch (e.g. `name`, `email`) — mirrors REST `POST /api/generate` |
| `generate_relational_data` | Multi-table JSON with `foreign_key` columns — mirrors REST `POST /api/generate/schema` |

Ask your agent in natural language; it should map the request to tool arguments before calling.

## Quick setup

1. [Sign up](https://bugiadata.com/signup) (or sign in).
2. Open **Dashboard → MCP** and copy your API key.
3. Add the config below for your client.
4. Restart the client and try: *"Use BugiaData to generate 5 users with pt_BR locale."*

### Cursor

Project: `.cursor/mcp.json` · Global: `~/.cursor/mcp.json` (Windows: `%USERPROFILE%\.cursor\mcp.json`)

```json
{
  "mcpServers": {
    "bugiadata": {
      "url": "https://mcp.bugiadata.com/sse",
      "headers": {
        "X-API-Key": "YOUR_API_KEY"
      }
    }
  }
}
```

See [examples/cursor-mcp.json](examples/cursor-mcp.json).

### Claude Desktop

Edit `claude_desktop_config.json` (same `mcpServers` block as above).

See [examples/claude-desktop.json](examples/claude-desktop.json).

### Claude Code

Edit `~/.claude/mcp.json` (same `mcpServers` block as above).

### Windsurf

Edit `~/.codeium/windsurf/mcp_config.json` (same `mcpServers` block as above).

See [examples/windsurf-mcp.json](examples/windsurf-mcp.json).

## Example prompts

- *"Ping BugiaData and show my quota."*
- *"Generate 20 emails and names with locale en_US."*
- *"Generate users and orders: orders.author_id must reference users.id, locale pl_PL."*

## Relational schema shape

`generate_relational_data` expects a table map. Simplified example:

```json
{
  "users": {
    "columns": {
      "id": { "type": "uuid" },
      "name": { "type": "name" },
      "email": { "type": "email" }
    }
  },
  "orders": {
    "columns": {
      "id": { "type": "uuid" },
      "user_id": { "type": "foreign_key", "reference": "users.id" },
      "total": { "type": "pydecimal", "left_digits": 3, "right_digits": 2 }
    }
  }
}
```

Full REST/MCP docs: [bugiadata.com/docs](https://bugiadata.com/docs)

## MCP Registry

This repo includes [`server.json`](server.json) for the [official MCP Registry](https://modelcontextprotocol.io/registry). Publishing is optional; see issue tracker on the private product repo.

## Security

- Never commit real API keys. Use placeholders in config files.
- Keys are created and rotated in the [BugiaData dashboard](https://bugiadata.com/dashboard?tab=mcp) only.
- Generation consumes your monthly token quota (same as the REST API).

## Links

- Product: https://bugiadata.com  
- MCP landing: https://bugiadata.com/mcp  
- JSON discovery: https://mcp.bugiadata.com/.well-known/mcp.json  

## License

MIT — applies to this documentation repository only. The BugiaData application and MCP server implementation are proprietary.
