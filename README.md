<p align="center"><img src="assets/logo.png" width="96" alt="Ecommerce Leads logo"></p>

# Ecommerce Leads MCP Server

Remote MCP server for ecommerce store data. Look up any online store by domain and get
estimated revenue, marketing budget, traffic, Google and Meta ad spend, ad counts, a
Conversion Rate Score, buying signals, and social and ad-library links.

Log in with your [Ecommerce Leads](https://getecommerceleads.com) account (OAuth) to search
600,000+ stores, reveal decision-maker contacts, and manage signal sets and watchlists.

- **Endpoint:** `https://getecommerceleads.com/api/mcp`
- **Transport:** Streamable HTTP
- **Auth:** none for `lookupStore`; OAuth 2.1 (PKCE, dynamic client registration) for all other tools
- **Registry name:** `com.getecommerceleads/ecommerce-leads`
- **Docs:** https://getecommerceleads.com/docs

This repository holds the listing files only (`server.json`, `mcp.json`, `plugin.json`, logo).
The server is hosted. There is nothing to install.

## Connect

### Claude (claude.ai / Claude Desktop)

Settings → Connectors → Add custom connector → paste `https://getecommerceleads.com/api/mcp`.

### Claude Code

```bash
claude mcp add --transport http ecommerce-leads https://getecommerceleads.com/api/mcp
```

### Cursor / VS Code / any client with remote MCP

```json
{
  "mcpServers": {
    "ecommerce-leads": {
      "url": "https://getecommerceleads.com/api/mcp"
    }
  }
}
```

### Clients that only support stdio

```bash
npx -y mcp-remote https://getecommerceleads.com/api/mcp
```

The first call to a logged-in tool opens the OAuth login in your browser.

## Tools

No login needed:

| Tool | What it does |
|---|---|
| `lookupStore` | Metrics for one store by domain or URL: revenue, marketing budget, traffic, ad spend, ad counts, Conversion Rate Score, buying signals, socials. |

Login needed (OAuth). Read-only:

| Tool | What it does |
|---|---|
| `searchStores` | Search the store catalog with dashboard filters. 30 rows per page. |
| `getStoreChart` | Last 24 points of one metric for a store. |
| `listSignalSets` / `getSignalSet` | Your saved signal sets and their criteria. |
| `previewSignalSet` | Check if signal criteria match enough stores. Saves nothing. |
| `listWatchlists` / `getWatchlist` | Your watchlists and blacklist. |
| `getRevealCost` | Credit cost of a reveal. Charges nothing. |
| `getRevealStatus` | Status of contact searches and your credit balance. |

Login needed (OAuth). Write:

| Tool | What it does |
|---|---|
| `revealStores` | Reveal contacts and signals. **Spends credits**; the assistant must confirm the cost first. |
| `saveSignalSet` / `deleteSignalSet` | Create, update or delete a signal set. |
| `createWatchlist` / `renameWatchlist` / `deleteWatchlist` | Manage watchlists. |
| `addToWatchlist` / `removeFromWatchlist` | Add or remove domains. Adding spends 1 credit per new domain. |
| `updateOutreachStatus` | Set the outreach status of a revealed store. |
| `exportStores` | Export revealed stores as CSV (max 200 rows per call). |
| `sendFeedback` | Send a message to the Ecommerce Leads team. |

All tools declare `readOnlyHint`, `destructiveHint` and `openWorldHint` annotations.

## Example prompts

- "Look up the store metrics for gymshark.com"
- "Compare estimated revenue and ad spend for allbirds.com and gymshark.com"
- "Log in and search for Shopify apparel brands with growing traffic"
- "How many credits does it cost to reveal the CEO contact for gymshark.com?"

## Privacy and support

- Privacy policy: https://getecommerceleads.com/privacy-policy
- Terms: https://getecommerceleads.com/terms-of-service
- Support: diogo@getecommerceleads.com
