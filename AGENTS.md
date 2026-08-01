# AGENTS.md

## Goal

Help publish this application to a verifiable Render staging environment. Keep
changes small and explain which release requirement each change satisfies.

## Runtime and checks

- Node.js `>=24 <27`, pnpm `11.5.1`, JavaScript only.
- Replay is the required AI provider for this exercise.
- Run `pnpm check`, `pnpm test`, and `pnpm test:e2e` before pushing.
- Verify a deployed release with
  `pnpm verify:remote -- <base-url> <expected-commit>`.

## Boundaries

- Do not add secrets or live AI provider calls.
- Do not weaken GitHub Actions, tests, `/health`, or remote verification.
- Keep `/health` independent from SQLite and external services.
- Do not replace Replay or add a managed database.
- Treat local SQLite data as disposable in this deployment exercise.
- Stop and explain evidence before changing deployment configuration.
