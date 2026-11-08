# Error Handling

## Current behavior

There is no explicit error boundary around module loading, renderer creation, or first render. Failures are expected to surface as browser errors.

## Required future behavior

- Catch module/renderer initialization failures.
- Show a visible and screen-reader-readable fallback.
- Keep the DOM product summary usable when 3D is unavailable.
- Log actionable diagnostic details without exposing secrets.
