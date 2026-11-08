# Performance Audit

- Renderer uses antialiasing, DPR capped at 2, a 2048² shadow map, and continuous rendering.
- Product geometry uses high segment counts, especially cylinders and toruses.
- Three product groups are constructed up front; only visibility changes at runtime.
- No adaptive DPR, LOD, GPU profiling, or renderer memory telemetry exists.
- No local texture/model payloads were found.

Measured FPS and draw-call values are `UNKNOWN` because no browser profiling harness was available.
