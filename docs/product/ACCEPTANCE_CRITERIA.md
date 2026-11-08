# Acceptance Criteria

## Core showcase

- The page loads the scene over HTTP in a supported browser.
- Exactly one product group is visible after initialization and after every switch.
- Color changes affect only the active product's color materials.
- Product copy, specs, pressed states, and CTA update together.
- OrbitControls do not permit distances outside configured limits.

## Reliability additions

- WebGL failure presents an accessible fallback.
- CDN/module failure presents an actionable error state.
- Reduced motion disables or substantially reduces forced 3D rotation.
- Loading state is removed only after the first successful render.
