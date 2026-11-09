# ADR-002: Production Dependency Delivery Strategy

## Status

Accepted for planning; production migration is not yet implemented.

## Context

The current application has no `package.json`, lockfile, bundler, CI workflow, or local Three.js copy. `index.html` loads Three.js `0.169.0` and `OrbitControls` through a jsDelivr Import Map.

## Options considered

| Option | Reproducibility | Availability | Integrity/update | Decision |
|---|---|---|---|---|
| Keep direct CDN Import Map | Low to medium | Depends on network/CDN | Version pinned, but no local artifact/SRI workflow | Prototype only |
| Vendor exact modules locally | High | High after deployment | Repository review and explicit upgrade commits | Production candidate |
| Package manager + local build | High | High after deployment | Lockfile, build audit, rollback artifact | Production candidate |

## Decision

Keep the pinned CDN Import Map for the current zero-build prototype. Before production release, adopt a reproducible local dependency strategy: preferably a package-managed local bundle with a lockfile, or vendored exact modules if zero-build operation remains a hard constraint.

No migration is included in TASK-004. A future implementation task must define the package manager/bundler, integrity checks, CI verification, deployment artifact, update cadence, and rollback procedure.

## Consequences

- The prototype remains simple and unchanged.
- CDN availability and supply-chain risk remain open for the prototype.
- Production readiness is blocked until a local/reproducible delivery path is implemented and verified.
