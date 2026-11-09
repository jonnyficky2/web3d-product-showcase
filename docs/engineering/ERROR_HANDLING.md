# Error Handling

## Current behavior

Renderer creation now has an explicit WebGL guard, and a classic script registers module-load and relevant unhandled-rejection fallback handlers. First-render failures beyond initialization still require additional handling.

## Required future behavior

- Catch module/renderer initialization failures.
- Show a visible and screen-reader-readable fallback.
- Keep the DOM product summary usable when 3D is unavailable.
- Log actionable diagnostic details without exposing secrets.

## Current implementation

`index.html` exposes `window.showFormaFallback`, renders an accessible `role="alert"`, catches renderer initialization failures, and reports module/CDN failures with actionable browser guidance.
