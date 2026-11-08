# Web3D Audit

## Verified

- Three.js WebGL renderer with ACES tone mapping and PCF soft shadows.
- Procedural geometry for three product groups.
- OrbitControls with damping, zoom, pan, and polar limits.
- PBR-style `MeshPhysicalMaterial` on selected product surfaces.

## Gaps

- No WebGPU path or renderer fallback.
- No GLTF/GLB, texture, HDRI, compression, cache, instancing, or LOD pipeline.
- High segment counts and continuous rendering need profiling.
- No complete disposal lifecycle.
- Triangle counts, draw calls, FPS, and GPU memory are `UNKNOWN` until browser profiling is run.
