# Family Week — Live Security-Header Verification Record

**Verification date:** September 3, 2026

**Target:** Current private, owner-only Family Week deployment

**Method:** Read-only HTTPS requests without a Google session or calendar access

**Claim boundary:** This is focused operating evidence, not a penetration test, TLS audit, ASVS verification, or certification.

The deployment address, account identity, temporary access value, request identifiers, and response bodies are intentionally excluded from this public-safe record.

## Results

| Check | Root page | Authentication-status API | Expected result |
| --- | --- | --- | --- |
| HTTPS response | Passed — 200 | Passed — 200 | Reachable through the existing private access boundary |
| Content Security Policy | Passed | Passed | Same-origin default, connection, font, and form sources; framing and objects denied; only documented image, style, script, and worker exceptions |
| HTTP Strict Transport Security | Passed | Passed | One-year policy with subdomains on HTTPS |
| Frame protection | Passed | Passed | `frame-ancestors 'none'` and `X-Frame-Options: DENY` |
| MIME sniffing protection | Passed | Passed | `X-Content-Type-Options: nosniff` |
| Referrer protection | Passed | Passed | `Referrer-Policy: no-referrer` |
| Cross-origin opener isolation | Passed | Passed | `Cross-Origin-Opener-Policy: same-origin` |
| Cross-origin resource policy | Passed | Passed | `Cross-Origin-Resource-Policy: same-origin` |
| Browser capability policy | Passed | Passed | Camera limited to self; microphone and geolocation disabled |
| API cache prevention | Not applicable to page | Passed | `Cache-Control: no-store` on the API response |

## Privacy and safety controls used

- The check used a temporary, site-scoped access mechanism and did not persist it in source, configuration, logs, or this record.
- No application cookies, Google credentials, OAuth tokens, calendar identifiers, event data, photos, or household information were supplied.
- Response bodies were not retained.
- Only expected header names, policy values, paths, and status codes were evaluated.
- Site access remained owner-only throughout the check.

## Limitations and follow-up

- The test covers the root page and one non-mutating API path; it does not prove every intermediary or error response behaves identically.
- It does not independently grade supported TLS versions, cipher suites, certificate-chain behavior, CDN configuration, or downgrade resistance.
- The policy still permits narrowly required inline styles, inline scripts, and WebAssembly evaluation; reducing those exceptions requires framework and OCR compatibility testing.
- Re-run this check after changes to hosting, routing, authentication, response middleware, CSP, or external integrations.
- Manual browser, assistive-technology, supported-device, and synthetic calendar testing remain pending.

## Result

The sampled private production responses matched the documented security-header policy. This evidence supports readiness only and does not establish compliance, conformance, certification, or absence of vulnerabilities.
