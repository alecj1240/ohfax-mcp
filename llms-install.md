# Install Oh Fax MCP

Oh Fax is a remote MCP server. Do not clone or build anything. Point the client at the URL.

MCP URL: https://app.ohfax.com/mcp
Transport: streamable HTTP
Auth: none for quote/send (pay per fax via Checkout link or MPP)

## Claude Code
```
claude mcp add --transport http ohfax https://app.ohfax.com/mcp
```

## Codex
```
codex mcp add ohfax --url https://app.ohfax.com/mcp
```

## Cursor / Windsurf / Claude Desktop / Cline
Add a server named `ohfax` with url `https://app.ohfax.com/mcp`.

## VS Code
Add a server named `ohfax` with type `http` and url `https://app.ohfax.com/mcp`.

## Verify
List tools. You should see quote_fax, send_fax, get_fax_status, get_fax_receipt.
