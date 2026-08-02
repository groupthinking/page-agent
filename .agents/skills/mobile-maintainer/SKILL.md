---
name: mobile-maintainer
description: 'Audit and fix mobile/responsive best practices on the website (packages/website). Use when: checking responsive layout, touch targets, viewport issues, mobile navigation, or when the user asks for a mobile audit or mobile fixes.'
argument-hint: 'Describe the scope, for example: homepage only, or docs layout'
---

# Mobile Maintainer

Keep `packages/website` mobile-friendly. Audit responsive behavior, then fix issues using the website conventions in `packages/website/AGENTS.md`.

## When to Use

- Audit a page for mobile/responsive best practices
- Fix layout breakage at small viewports
- Review new sections/pages for mobile readiness before merge

## Checklist

Audit each in-scope page against:

### Layout

- No horizontal overflow at 320px, 375px, and 768px widths
- Grids and flex rows collapse sensibly (`grid-cols-1 md:grid-cols-*`, `flex-col md:flex-row`)
- Fixed widths replaced by `max-w-*` + `w-full` patterns
- Images and code blocks constrained (`max-w-full`, `overflow-x-auto`)

### Typography

- Font sizes scale down on small screens (`text-3xl md:text-5xl` style patterns)
- Line lengths remain readable; headings don't wrap awkwardly

### Touch & Interaction

- Interactive targets at least 44x44px effective size
- Hover-only affordances have touch equivalents
- Mobile navigation is reachable (header menu works at small widths)

### Platform

- `viewport` meta tag present in `index.html`
- Dark mode (`dark:`) still correct at mobile breakpoints
- Docs sidebar (`src/pages/docs/Layout.tsx`) usable on mobile

## Procedure

1. Identify in-scope pages under `packages/website/src/pages/`
2. Grep for responsive utility usage (`md:`, `lg:`, `sm:`) to find components lacking breakpoints
3. Fix using Tailwind responsive classes only — follow `packages/website/AGENTS.md` (shadcn/ui first, no hand-editing `src/components/ui/`)
4. Verify with `npm start` (dev server) at narrow viewports, then `npm run typecheck` and `npm run lint`
5. Report findings as a table: page, issue, fix applied

## Rules

- Mobile-first: base styles for small screens, override with `md:`/`lg:`
- Never introduce custom CSS when a Tailwind utility exists
- Do not change desktop appearance unless it also violates the checklist
