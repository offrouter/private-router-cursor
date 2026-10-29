# Changelog

## 0.3.0 - 2026-10-29

- Renamed to `offrouter-private-router` (OffRouter Private Router), in its own repository: github.com/offrouter/private-router-cursor

## 0.2.1 - 2026-10-29

Single-plugin repo in the Open Plugins layout, the one cursor.directory detects:

- Manifest at `.plugin/plugin.json`, with a Cursor copy at `.cursor-plugin/plugin.json`
- MCP config at `.mcp.json`, with a Cursor copy at `mcp.json`
- Logo is a PNG (`assets/logo.png`)

## 0.2.0 - 2026-10-29

- Connects to the hosted OffRouter MCP server at `https://offrouter.org/mcp`: nothing to install
- `ask` works without a key on the free demo; set `OFFROUTER_API_KEY` for every model, `compare` and `balance`
- New skill `private-swap`: quote, submit and follow a sealed token swap on Robinhood Chain, signed by your own wallet
- Skill `private-inference` and rule `offrouter` updated for the hosted server's tools
