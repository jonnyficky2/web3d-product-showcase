# Forma Agent Instructions

## Identity

Forma is a browser-only, zero-build Three.js r169 WebGL product showcase. The application source is `index.html`; there is no backend, database, authentication, package manifest, test runner, or deployment workflow.

## Read first

1. `DOCUMENTATION_INDEX.md`
2. `docs/project/PROJECT_STATE.md`
3. `docs/project/TASK_BOARD.md`
4. The complete task file for the requested `TASK-*` ID
5. Relevant requirements, architecture, testing, and audit documents

## Rules

- Verify the actual source before making claims.
- Do not assume Three.js features, APIs, assets, backend systems, or tests that are absent.
- Execute only the authorized task scope.
- Never mark a task `DONE` without implementation and verification evidence.
- Do not modify or delete unrelated user changes.
- Do not expose secrets or add credentials.
- Preserve the zero-build architecture unless an ADR authorizes a change.

## Synchronization

After meaningful work, update the task detail, `TASK_BOARD.md`, milestone progress, `PROJECT_STATE.md`, `SESSION_LOG.md`, and relevant technical/audit documents.

## Verification

Run available checks. If browser, device, build, or performance verification is unavailable, record `UNKNOWN` or `PENDING` rather than inventing results.

## Completion report

Report task ID, scope, modified files, acceptance criteria evidence, test commands/results, remaining risks, and next eligible tasks.
