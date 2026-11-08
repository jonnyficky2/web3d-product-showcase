# Product Requirements Document

## Product

Forma is an interactive 3D showcase for exploring a small collection of premium hardware products.

## Vision

Let a visitor inspect product form, switch variants, and initiate a product inquiry from one responsive browser experience.

## Scope

### Implemented requirements

- `FR-001`: Render a full-screen 3D product scene.
- `FR-002`: Provide three selectable procedural products.
- `FR-003`: Allow orbit, zoom, and pan interaction.
- `FR-004`: Allow three color selections for the active product.
- `FR-005`: Update product copy, specs, and CTA when switching products.
- `FR-006`: Open a mail client through a product-specific mailto subject.

### Planned requirements

- `FR-101`: Show a clear fallback when WebGL/module loading fails.
- `FR-102`: Provide a loading state before the scene is ready.
- `FR-103`: Support smooth camera transitions between products.
- `FR-104`: Export a PNG snapshot.
- `NFR-101`: Maintain acceptable frame rate on low-tier mobile devices.
- `NFR-102`: Respect `prefers-reduced-motion` in JavaScript animation.
- `NFR-103`: Provide reproducible dependency and release verification.

## Non-goals

Backend commerce, payment, authentication, user accounts, server-side order storage, CMS, and real product inventory are outside the verified current scope.

## Users

- Prospective customer inspecting product form and variants.
- Designer or stakeholder reviewing a product concept.
- Developer maintaining the showcase.

## Constraints

The current application is zero-build, uses CDN modules, and has no server-side system.

## Success measures

The current project does not include analytics or measured product KPIs. Performance and conversion targets are `PENDING` until instrumentation and device test methodology exist.
