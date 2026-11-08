# Threat Model

## Assets

The current app has no stored user data or credentials. Primary assets are product presentation, external dependency integrity, and user trust.

## Threats

- CDN compromise or outage.
- Future XSS if product data becomes remote and continues using `innerHTML`.
- Malicious external links or future mailto data injection.
- Denial of service through oversized future assets or unbounded scene creation.

## Mitigations

Pin and review dependencies, use CSP/SRI or local bundling, prefer text DOM APIs, validate remote data, and cap asset/resource budgets.
