# LLMs Package - Instructions for Coding Assistants

LLM client (`@page-agent/llms`) with reflection-before-action mental model. Published to npm.

## Responsibilities

- `src/index.ts` — LLM class with retry logic
- `src/OpenAIClient.ts` — OpenAI-compatible client
- `src/types.ts` — `MacroToolInput`, `AgentBrain`, `LLMConfig` contracts
- `src/errors.ts` — typed error definitions
- `src/constants.ts`, `src/utils.ts` — shared constants and helpers

## Module Boundaries

- Zero dependency on other page-agent packages — must remain standalone
- The `MacroToolInput` contract is the API boundary consumed by `@page-agent/core`; treat changes to `src/types.ts` as breaking and update consumers

## Testing

This is the reference package for testing conventions in the monorepo:

- Vitest, co-located tests (`src/foo.test.ts` next to `src/foo.ts`)
- `vitest.config.ts` in the package plus a `"test": "vitest run"` script

```bash
npm test -w @page-agent/llms      # from root
cd packages/llms && npx vitest    # watch mode
```

## Conventions

- Explicit typing for exported/public APIs
- Never hide provider errors — wrap them with typed errors from `src/errors.ts` and keep them actionable
- No secrets in code or fixtures; API keys come from config at runtime
