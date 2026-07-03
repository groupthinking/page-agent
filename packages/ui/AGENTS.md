# UI Package - Instructions for Coding Assistants

Panel and i18n (`@page-agent/ui`). Decoupled from PageAgent.

## Responsibilities

- `src/panel/Panel.ts` — floating panel component (+ `Panel.module.css`, `cards.ts`)
- `src/panel/types.ts` — `PanelAgentAdapter` interface (the decoupling contract)
- `src/i18n/` — internationalization (`locales.ts`)
- `src/motion-css/` — animation styles

## Module Boundaries

- Must NOT import from `page-agent`, `@page-agent/core`, or `@page-agent/llms`
- Communicates with the agent only through the `PanelAgentAdapter` interface — extend the adapter rather than importing agent types
- This UI is injected into arbitrary host pages: keep styles scoped (CSS modules), avoid global style leakage, and mind z-index/stacking against unknown page CSS

## i18n

- All user-facing strings go through `src/i18n/locales.ts` — never hard-code display text in components
- Add new keys to every locale when introducing strings

## Commands (from repo root)

```bash
npm run typecheck && npm run lint
```

## Conventions

- Explicit typing for exported/public APIs
- Vanilla TS + CSS modules (no React here — React is only used in extension/website)
