# Extension Package - Instructions for Coding Assistants

Browser extension (`@page-agent/ext`, private) built with WXT + React 19 + Tailwind CSS 4.

## Responsibilities

- `src/entrypoints/` — WXT entrypoints: `background.ts`, `content.ts`, `main-world.ts`, `sidepanel/`, `hub/`
- `src/agent/` — multi-page agent layer:
    - `MultiPageAgent.ts`, `useAgent.ts` — agent orchestration across tabs
    - `RemotePageController.*.ts` — controller proxied across background/content contexts
    - `TabsController*.ts`, `tabTools.ts` — tab management tools
    - `system_prompt.md` — extension-specific system prompt
- `src/components/` — React UI (shadcn-style components; see `components.json`)
- `wxt.config.js` — WXT/Vite configuration

## Key Facts

- The extension reuses `@page-agent/core` logic through `RemotePageController`, which splits PageController calls across the content script and background via messaging — any new PageController method used here needs its proxy wiring
- The `hub` entrypoint serves the WebSocket connection used by `packages/mcp`; keep the protocol in sync
- Typecheck uses this package's own `tsconfig.json` (wired into root `npm run typecheck`)
- `PRIVACY.md` must be kept accurate for Chrome Web Store listing when data handling changes

## Commands (from repo root)

```bash
npm run dev:ext                   # WXT dev mode (launches Chromium profile)
npm run build:ext                 # Build and zip the extension
npm run typecheck && npm run lint
```

## Conventions

- React function components + hooks; Tailwind for styling with `dark:` support
- Do not hand-edit generated shadcn-style UI primitives; add via the shadcn CLI
- All user-visible errors should be actionable (shown via sonner toasts)
