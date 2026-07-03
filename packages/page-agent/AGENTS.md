# Page Agent Package - Instructions for Coding Assistants

Main entry (`page-agent` on npm). PageAgentCore + built-in UI Panel.

## Responsibilities

- `src/PageAgent.ts` — main class with UI, extends `PageAgentCore` and wires in the Panel
- `src/demo.ts` — IIFE demo entry (auto-init with demo API)

## Module Boundaries

- Imports from `@page-agent/core` and `@page-agent/ui`
- Agent logic belongs in `@page-agent/core`; UI components belong in `@page-agent/ui`. This package should stay a thin integration layer — resist adding logic here that fits a lower-level package

## Publishing Notes

- Source-first: `package.json` exports point to `src/*.ts` in development; `scripts/pre-publish.js` swaps to `dist/` at publish time
- Demo build is produced alongside the library build (`npm run build:libs` from root)

## Commands (from repo root)

```bash
npm run dev:demo                  # Demo dev server
npm run build:libs                # Build all libraries incl. this one
npm run typecheck && npm run lint
```

## Conventions

- Explicit typing for exported/public APIs
- Keep the public `PageAgent` API stable — it is the primary npm-facing surface
