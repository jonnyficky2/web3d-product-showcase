# Project Documentation Decision

## Decision

Adopt a scoped Markdown documentation system under `docs/` while preserving the existing root and legacy documents.

## Why

The repository is a small zero-build prototype. A full backend/API/database document set would otherwise imply systems that do not exist. Documents therefore describe verified behavior and explicitly label absent systems as `N/A`, `UNKNOWN`, or `PENDING`.

## Consequences

- `docs/project/PROJECT_STATE.md` is the operational source of truth.
- `DOCUMENTATION_INDEX.md` maps topics to authoritative documents.
- Existing application behavior is unchanged.
- Documentation must be updated when implementation status changes.
