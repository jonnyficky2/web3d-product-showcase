# Performance Audit

**Baseline date:** 2026-11-09
**Task:** TASK-006

## Test availability

No browser/device profiler is available in the current environment. The following values are source-verified or structural estimates; runtime FPS, frame time, actual draw calls, and GPU memory remain `UNKNOWN`.

## Source-verified configuration

| Metric | Current value | Evidence |
|---|---|---|
| Renderer | `THREE.WebGLRenderer({ antialias: true })` | `index.html:146` |
| Pixel ratio | `min(devicePixelRatio, 2)` | `index.html:151`, `300` |
| Shadow map | Enabled, `PCFSoftShadowMap`, 2048 × 2048 | `index.html:153-164` |
| Render loop | Continuous `requestAnimationFrame` | `index.html:306-314` |
| Product groups constructed | 3 at initialization | `index.html:250-254` |
| Local texture/model payload | None found | Repository discovery |

## Structural scene inventory

The source creates approximately 9 speaker meshes, 10 headphone meshes, and 16 watch meshes, plus one floor mesh. Only one product group is visible at a time, so the active scene is approximately 10–17 meshes including the floor. This is a source estimate, not a replacement for `renderer.info.render.calls`.

Geometry uses high segment counts: cylinders and toruses commonly use 64–96 radial segments, tubes use 64 tubular segments, and the floor uses 96 segments.

## Runtime measurement matrix

| Profile | Device/browser | Viewport/DPR | FPS | Frame time | Draw calls | GPU memory | Status |
|---|---|---|---:|---:|---:|---:|---|
| Low-tier mobile | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | PENDING browser access |
| Desktop comparison | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | PENDING browser access |

## Reproduction procedure

1. Serve the repository over HTTP and open the page in a browser.
2. Record device, browser version, viewport, DPR, and active product.
3. Use the browser Performance panel for a 30-second idle capture and a product-switch interaction capture.
4. Record `renderer.info.render.calls`, `renderer.info.render.triangles`, and `renderer.info.memory` from a temporary diagnostic run.
5. Repeat on a low-tier mobile profile and desktop comparison.

## Findings

- Renderer uses antialiasing, DPR capped at 2, a 2048² shadow map, and continuous rendering.
- Product geometry uses high segment counts, especially cylinders and toruses.
- Three product groups are constructed up front; only visibility changes at runtime.
- No adaptive DPR, LOD, GPU profiling, or renderer memory telemetry exists.
- No local texture/model payloads were found.

## Decision

TASK-006 is in `TESTING`: source baseline is documented, but device measurements are still pending. TASK-002 and TASK-007 must not be executed as if measured data exists.
