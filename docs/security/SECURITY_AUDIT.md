# Security Audit

| ID | Severity | Finding | Evidence | Status |
|---|---|---|---|---|
| SEC-001 | High | CDN-only dependency has supply-chain/availability risk | `index.html:99-104` | Open |
| SEC-002 | Medium | Dynamic UI uses `innerHTML` | `index.html:239,242` | Low risk while data is static; open |
| SEC-003 | Medium | No CSP/security-header configuration | No deployment config found | Open |
| SEC-004 | Info | No secrets, auth, uploads, or backend endpoints found | Repository-wide discovery | Clear |

No actual credentials or secrets are included in this document.
