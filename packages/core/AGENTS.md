# Core Package - Instructions for Coding Assistants

Headless agent logic (`@page-agent/core`). No UI. Published to npm.

## Responsibilities

- `src/PageAgentCore.ts` — core agent class: task loop, LLM orchestration, tool dispatch
- `src/tools/index.ts` — agent tool definitions that call PageController methods
- `src/prompts/system_prompt.md` — system prompt template
- `src/config/` — configuration types and constants
- `src/utils/` — helpers, including `autoFixer.ts`

## Module Boundaries

- May import from `@page-agent/llms` and `@page-agent/page-controller` only
- Must NOT import from `@page-agent/ui` or `page-agent` — UI concerns live upstream
- Keep this package usable in headless contexts (extension background, MCP)

## Adding a New Agent Tool

1. If the tool needs DOM operations, add the method to PageController first (`packages/page-controller`)
2. Implement the tool in `src/tools/index.ts`, calling `this.pageController.methodName()`
3. Update `src/prompts/system_prompt.md` if the tool changes agent behavior expectations

## Commands (from repo root)

```bash
npm run typecheck                 # Typecheck all packages
npm test -w @page-agent/core      # Unit tests for this package
npm run lint                      # ESLint
```

## Conventions

- Explicit typing for exported/public APIs
- Tests are co-located: `src/foo.test.ts` next to `src/foo.ts` (Vitest)
- Surface errors — do not swallow them; traceability over success rate
