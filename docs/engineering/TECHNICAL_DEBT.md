# Technical Debt

| ID | Debt | Impact | Priority |
|---|---|---|---:|
| TD-001 | CDN-only runtime dependency | Availability/reproducibility | High |
| TD-002 | Runtime fallback lacks browser verification | Failure behavior may regress undetected | High |
| TD-003 | Continuous high-quality render loop | Mobile battery/GPU cost | High |
| TD-004 | No resource disposal lifecycle | Future memory leaks | Medium |
| TD-005 | Single-file application | Maintainability | Medium |
| TD-006 | No automated verification | Regression risk | Medium |
