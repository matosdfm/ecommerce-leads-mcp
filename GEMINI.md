# Ecommerce Leads

The `ecommerce-leads` MCP server returns data about ecommerce stores.

- `lookupStore` works without login. It takes one store domain or URL per call and returns
  estimated revenue, marketing budget, traffic, Google and Meta ad spend, ad counts, a
  Conversion Rate Score, buying signals, and social and ad-library links.
- All other tools need an Ecommerce Leads account. If a tool returns "This tool requires
  authentication", tell the user to run `/mcp auth ecommerce-leads` and log in, then retry.
- `revealStores` and `addToWatchlist` spend credits. Call `getRevealCost` first, tell the user
  the cost, and wait for the user to confirm before you call them.
- `deleteSignalSet` and `deleteWatchlist` cannot be undone. Ask the user to confirm first.
