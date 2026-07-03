# MCP Package - Instructions for Coding Assistants

MCP server (`@page-agent/mcp`) that lets AI clients (Claude Desktop, Copilot, etc.) control the browser via the Page Agent extension.

## Responsibilities

- `src/index.js` — MCP server entry (exposed as the `page-agent-mcp` bin)
- `src/hub-bridge.js` — WebSocket bridge between the MCP server and the extension hub
- `src/launcher.html` — launcher page

## Key Facts

- Plain JavaScript (no build step) — `files` ships `src/` directly, so code must run as-is on Node >= 20
- Runtime deps: `@modelcontextprotocol/sdk`, `ws`, `zod`
- Configuration comes from env vars (`LLM_BASE_URL`, `LLM_API_KEY`, `LLM_MODEL_NAME`) — never hard-code credentials
- Communicates with `packages/extension` (hub entrypoint) over WebSocket; keep the message protocol in sync with the extension when changing it

## Commands (from repo root)

```bash
npm run lint
node packages/mcp/src/index.js    # manual smoke run (requires extension + env vars)
```

## Conventions

- Validate all inbound messages with zod schemas
- Surface connection/protocol errors clearly — they are the main debugging signal for users
- Update `packages/mcp/README.md` when changing setup or configuration options
