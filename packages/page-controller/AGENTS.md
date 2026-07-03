# Page Controller Package - Instructions for Coding Assistants

DOM operations and visual feedback (`@page-agent/page-controller`). Independent of any LLM.

## Responsibilities

- `src/PageController.ts` — main controller class with optional mask support
- `src/actions.ts` — element interactions (click, input, scroll)
- `src/dom/dom_tree/index.js` — core DOM extraction engine (live DOM → `FlatDomTree`)
- `src/dom/getPageInfo.ts` — page metadata extraction
- `src/mask/` — SimulatorMask visual overlay blocking user interaction during automation
- `src/patches/` — DOM/environment patches

## Module Boundaries

- Zero LLM dependency — must never import from `@page-agent/llms` or `@page-agent/core`
- All public methods are async; consumers (PageAgentCore) call by element index
- Mask is opt-in via `enableMask: true` config

## Adding a New Action

1. Implement in `src/actions.ts`
2. Expose via an async method on `PageController.ts`
3. Export from `src/index.ts`
4. Then add the corresponding agent tool in `packages/core/src/tools/index.ts`

## Commands (from repo root)

```bash
npm test -w @page-agent/page-controller
npm run typecheck && npm run lint
```

## Conventions

- Explicit typing for exported/public APIs (note: `dom_tree` engine is JS)
- Tests co-located (Vitest): `src/PageController.test.ts`
- DOM operations must be robust to arbitrary host pages — avoid assumptions about frameworks or page structure
