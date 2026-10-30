# KMicro web frontend

The web shop and admin area for KMicro, built on the reworked kmicro-frontend code (React, Vite, TypeScript, Tailwind, shadcn/ui, Redux Toolkit with RTK Query). Later, a React Native app shares code with it through a pnpm workspace.

Status: not scaffolded yet. No commands exist yet. `/audit` fills those in after the project is set up.

## Source of truth

- `docs/design/frontend-design.md`: every locked decision for this repo (structure, BFF login, API layer, cart, checkout, search, money, admin, UI, security, supply chain, versions).
- `docs/design/backend-design.md`: the backend this app talks to (API conventions, flows, rules). Read it only when an API contract or a backend rule matters.
- The API contract is the backend's OpenAPI file; the client code is generated from it, never hand written.
- Read only the section you need, not the whole file.
- Decisions marked **Locked** are final. Do not reopen them. If work needs a decision the docs do not cover, stop and ask the owner. Do not assume.

## Workflow

Skills live in `.agents/skills/` (Claude Code reads them through the `.claude/skills` link).

- First time only: `/scope` (seed the scope from the design doc, matching the backend slices) → `/architect` (record the stack spec from the design doc) → set up the project → `/audit`.
- Per feature: `/architect` → `/develop` → `/check verify` → `/sync`.
- When `/check verify` finds wrong output: `/debug` → fix → one regression test for that bug.
- State lives in files (`docs/scope/`, `docs/specs/`, this file), so start a fresh session (`/clear`) between steps to keep context small.

## Rules

- Testing: no test driven development and no test suites written up front. Build the screen or flow, then check it in the browser against the local backend (`/check verify`). Write a test only when the output is wrong, as a regression test for that bug. Static checks (TypeScript strict, ESLint, Prettier) always run.
- Security: no tokens or personal data in `localStorage` or `sessionStorage`; nothing secret in `VITE_*` variables; no `dangerouslySetInnerHTML`; only same site redirects. Full list in the design doc, section 13.
- Dependencies: pnpm only. No new dependency, skill, MCP server or tool install without the owner's approval. Never run `npx skills add`. Exact versions, committed lockfile, no install scripts unless allow listed, versions published at least 7 days ago.
- Phase 1 scope only, unless the owner says otherwise.
- Write for the owner in short, simple English.

## Git

integration: on

- Work on a feature branch, never commit to `main` directly.
- Never push or open a PR without the owner's OK.
