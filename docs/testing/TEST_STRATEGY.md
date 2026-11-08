# Test Strategy

The current repository has no automated test framework. Testing should be layered as tooling is introduced:

- Static: HTML/JS syntax and Markdown link checks.
- Browser smoke: load, product switching, color switching, CTA URL, resize.
- Visual/manual: desktop, touch, reduced motion, WebGL disabled.
- Performance: FPS, frame time, draw calls, renderer memory, low-tier mobile.
- Security: dependency provenance, CSP, unsafe DOM sinks, external URL review.
