# cursor.store listing — BugiaData MCP

Paste-ready metadata for [cursor.store](https://www.cursor.store) dashboard (claim repo → edit listing). All copy in **English**.

## Live listing (auto-indexed)

**https://www.cursor.store/mcp/lgpoliveira/bugiadata-mcp**

Sign in with GitHub at [cursor.store/dashboard/mcps](https://www.cursor.store/dashboard/mcps) to claim and enrich description, category, install snippet, and permission notes.

---

## Suggested fields

| Field | Value |
|-------|-------|
| **Name** | BugiaData — Relational Fake Data for MCP |
| **Slug** | `lgpoliveira/bugiadata-mcp` (auto) |
| **Category** | Data & APIs |
| **Tags** | mcp, fake-data, test-data, faker, relational, seed, cursor, claude |
| **Author** | lgpoliveira |
| **Repository** | https://github.com/lgpoliveira/bugiadata-mcp |
| **Docs / homepage** | https://bugiadata.com/mcp |
| **License** | MIT (docs repo) |
| **Permission level** | Medium |

### Short description

Generate linked multi-table test data from Cursor via MCP. Locales, foreign keys, one API key.

### Long description

BugiaData connects to Cursor and Claude over the Model Context Protocol (SSE). Ask your agent for realistic rows or full relational schemas—users, orders, posts with valid foreign keys—and get structured JSON without leaving the chat.

**Tools:** `ping`, `whoami`, `generate_data`, `generate_relational_data`

**Setup:** Sign up at [bugiadata.com](https://bugiadata.com/signup) → Dashboard → MCP → copy the config snippet.

Free tier: 10k tokens/month. Same quota as the REST API and Studio.

### Install snippet (Cursor `.cursor/mcp.json`)

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

### Security notes

- Hosted remote MCP at `https://mcp.bugiadata.com/sse`; no local shell or filesystem access.
- User provides their own BugiaData API key via `X-API-Key` header (from dashboard).
- Generation consumes the user's monthly token quota; no access to other users' data.
