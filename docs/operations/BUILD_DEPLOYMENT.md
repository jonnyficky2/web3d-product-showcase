# Build and Deployment

## Current state

No build system, package manifest, CI workflow, hosting configuration, or deployment script was found. The documented local mode serves static files over HTTP.

ADR-002 records the current policy: CDN delivery is prototype-only; production requires a reproducible local dependency artifact.

## Release requirements

Before production release, define dependency delivery, CSP/security headers, browser support, hosting path, cache policy, and rollback procedure.
