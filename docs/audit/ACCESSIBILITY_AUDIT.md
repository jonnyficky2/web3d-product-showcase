# Accessibility Audit

## Strengths

- Semantic regions and labeled navigation exist.
- Product tabs and color controls expose `aria-label` and `aria-pressed`.
- Reduced-motion CSS exists for UI transitions.

## Findings

- WebGL failure has no accessible fallback.
- JavaScript auto-rotation ignores reduced-motion preference.
- Canvas has no dedicated accessible description or keyboard 3D interaction model.
- The `Support` navigation target does not exist.
