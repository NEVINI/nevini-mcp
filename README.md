# NEVINI Wines MCP server

Public [Model Context Protocol](https://modelcontextprotocol.io/) server of [NEVINI](https://nevini.wine/), a wine importer in Maastricht, the Netherlands. AI agents can search the wine range, read store information and prepare a Shopify cart. The customer completes the order and the payment in the checkout on shop.nevini.wine; the server never places orders or takes payments.

This repository only describes the hosted server. There is nothing to install or run.

## Endpoint

```
https://nevini.wine/api/mcp/
```

- Transport: Streamable HTTP (stateless, JSON responses). Keep the trailing slash.
- Authentication: none.
- Languages: every tool accepts `language: "nl"` (default) or `"en"`.

## Connect

- **Claude Code:** `claude mcp add --transport http nevini https://nevini.wine/api/mcp/`
- **claude.ai / Claude Desktop:** Customize > Connectors > "+ Add" > "Add custom connector", enter the URL above, authentication "No sign in".
- **ChatGPT (web):** Plugins > plus button > "Add custom MCP server", the URL above under Connection, "No authentication", then "Create as a plugin".
- **Cursor** (`~/.cursor/mcp.json` or `.cursor/mcp.json`):

  ```json
  { "mcpServers": { "nevini": { "url": "https://nevini.wine/api/mcp/" } } }
  ```

- **VS Code** (`.vscode/mcp.json`):

  ```json
  { "servers": { "nevini": { "type": "http", "url": "https://nevini.wine/api/mcp/" } } }
  ```

## Tools

| Tool | What it does |
|---|---|
| `search_wines` | Search and filter wines by text, type, country, region, grape, price, availability and dish (`food`). |
| `get_wine` | One wine with all taste notes, description, food pairing, bottle sizes, live prices and availability. |
| `get_catalog_overview` | Types, countries, categories, grapes and the top selection. |
| `get_store_info` | Company details, shipping, pickup, returns and the age requirement. |
| `create_cart` | New Shopify cart; returns a checkout link. |
| `add_to_cart` | Add lines to an existing cart. |
| `update_cart` | Change quantities or remove lines. |
| `get_cart` | Current contents and checkout link of a cart. |

Example prompts: "Find an Italian red wine under €30 that can be delivered in the Netherlands", "Recommend a white wine to go with seafood", "Welke witte wijn past bij vis of zeevruchten?".

## Ordering and age

NEVINI sells alcohol. The buyer and the recipient must be 18 or older (Dutch Alcohol Act). `create_cart` requires `buyer_is_18_or_older: true`, set only after the user confirms it. The agent hands over the checkout link; the customer completes the order and the payment on shop.nevini.wine.

## More

- Documentation: https://nevini.wine/en/mcp/ (Dutch: https://nevini.wine/mcp/)
- Official MCP Registry: [`wine.nevini/shop`](https://registry.modelcontextprotocol.io/v0.1/servers/wine.nevini%2Fshop/versions/latest) (the entry is `server.json` in this repository)
- Discovery: https://nevini.wine/.well-known/mcp.json, https://nevini.wine/.well-known/mcp/server-card.json, https://nevini.wine/.well-known/ard.json
- Agent Skill: https://nevini.wine/.well-known/agent-skills/order-nevini-wine/SKILL.md
- Questions: info@nevini.wine
