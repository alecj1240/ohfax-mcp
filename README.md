# Oh Fax MCP

Outbound fax for the United States and Canada. Quote a PDF + number, pay once, get a delivery receipt.

**MCP URL (no auth):** `https://app.ohfax.com/mcp`

- Product: [ohfax.com](https://ohfax.com)
- Fax a PDF (human): [ohfax.com/fax-pdf](https://ohfax.com/fax-pdf)
- Agent pay recipe: [ohfax.com/docs/agent-pay](https://ohfax.com/docs/agent-pay)
- Machine docs: [ohfax.com/llms.txt](https://ohfax.com/llms.txt)
- Official MCP Registry: `com.ohfax/ohfax`

**Price:** $2 per fax, up to 100 pages. Undeliverable faxes are refunded in full.

Agents need no Oh Fax account. Pay per send with a Stripe Checkout link or MPP (HTTP 402).

## Install

### Claude Code

```bash
claude mcp add --transport http ohfax https://app.ohfax.com/mcp
```

### Codex

```bash
codex mcp add ohfax --url https://app.ohfax.com/mcp
```

Manual: in `~/.codex/config.toml`:

```toml
[mcp_servers.ohfax]
url = "https://app.ohfax.com/mcp"
```

### Cursor

One-click: [Add Oh Fax to Cursor](https://cursor.com/link/mcp?name=ohfax&config=eyJ1cmwiOiJodHRwczovL2FwcC5vaGZheC5jb20vbWNwIn0=)

Or add to `.cursor/mcp.json` / Settings → MCP:

```json
{
  "mcpServers": {
    "ohfax": {
      "url": "https://app.ohfax.com/mcp"
    }
  }
}
```

### VS Code

One-click: [Add Oh Fax to VS Code](vscode:mcp/install?%7B%22name%22%3A%22ohfax%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A//app.ohfax.com/mcp%22%7D)

Or `.vscode/mcp.json`:

```json
{
  "servers": {
    "ohfax": {
      "type": "http",
      "url": "https://app.ohfax.com/mcp"
    }
  }
}
```

### Claude Desktop

Add to Claude Desktop MCP settings (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "ohfax": {
      "url": "https://app.ohfax.com/mcp"
    }
  }
}
```

### Windsurf

Add to Windsurf MCP config:

```json
{
  "mcpServers": {
    "ohfax": {
      "url": "https://app.ohfax.com/mcp"
    }
  }
}
```

### Cline

Add to Cline MCP settings:

```json
{
  "mcpServers": {
    "ohfax": {
      "url": "https://app.ohfax.com/mcp",
      "disabled": false
    }
  }
}
```

### Any MCP client

Remote URL: `https://app.ohfax.com/mcp` (streamable HTTP). No API key required for the pay-per-send path.

Example configs live in [`examples/`](./examples/).

## Tools (call in order)

| Tool | Purpose |
|------|---------|
| `quote_fax` | Free quote. Inputs: `to` (E.164), and `document_url` or `document_base64`. Returns `quote_id`, pages, amount. |
| `send_fax` | Get payment authorization for a `quote_id`. Does not charge by itself. |
| *(pay)* | Open the Checkout link or satisfy the MPP / HTTP 402 challenge. |
| `get_fax_status` | Poll delivery. |
| `get_fax_receipt` | Final receipt once the fax is final. |

Always quote before you send. The binding price is the quote / 402 challenge, not a guessed formula.

## Limits

- Destinations: US and Canada only
- PDF only, max 25 MB / 100 pages
- Outbound only (no inbound)
- Currency: USD

## Links

- [Home](https://ohfax.com)
- [Pricing](https://ohfax.com/pricing)
- [Compare](https://ohfax.com/compare)
- [OpenAPI](https://app.ohfax.com/openapi.json)
- [Glama connector](https://glama.ai/mcp/connectors/com.ohfax/ohfax)
