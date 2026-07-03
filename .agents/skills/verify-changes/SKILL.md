---
name: verify-changes
description: 'Run the full local verification pipeline (lint, typecheck, tests, builds) for the monorepo or an affected package. Use when: validating changes before commit/PR, reproducing CI locally, or when the user asks to verify, validate, or check the build.'
argument-hint: 'Optionally name the affected package, for example: @page-agent/core'
---

# Verify Changes

Run the same checks as CI locally, scoped to what changed.

## When to Use

- Before committing or opening a PR
- After refactors that cross package boundaries
- To reproduce a CI failure locally

## Procedure

### 1. Determine scope

```bash
git status --short
git diff --name-only HEAD
```

Map changed files to packages (`packages/<name>/`). Root config changes (eslint, tsconfig, scripts) mean full-repo scope.

### 2. Run checks (fast to slow)

```bash
npm run lint                          # ESLint, whole repo
npm run typecheck                     # All packages incl. extension
npm test                              # All workspaces with a test script
# or scoped: npm test -w @page-agent/llms
```

### 3. Build only when needed

Build if changes touch package exports, build scripts, or publish config:

```bash
npm run build:libs                    # All libraries
npm run build:website                 # Website only
npm run build:ext                     # Extension zip
```

The full CI pipeline is `node scripts/ci.js`.

## Reporting

- Report each step as pass/fail with the exact command used
- On failure, show the relevant error excerpt, not the full log
- Distinguish pre-existing failures (present before your changes) from new ones — only new failures block

## Rules

- Never edit unrelated tests to make them pass
- Never skip a failing step silently — surface it and explain
