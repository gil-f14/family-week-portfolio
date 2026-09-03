# Family Week — Architecture One-Pager

## System purpose

Family Week is a review-first schedule ingestion and calendar display application. It deliberately separates uncertain recognition from trusted calendar mutation.

## Data flow

```text
Photo or pasted text
        |
        v
On-device OCR and bounded preprocessing
        |
        v
Local correction dictionary + structured event proposals
        |
        v
Human review, owner assignment, and time validation
        |
        v
Server checks every approved readable calendar for duplicates
        |
        v
Approved event is written only to the app-created calendar
        |
        v
Week / agenda display and safe app-owned deletion
```

## Trust boundaries

- **Browser boundary:** source photos, OCR text, drafts, and learned corrections remain local during the normal workflow.
- **Application boundary:** only reviewed structured events cross to the server.
- **Google boundary:** OAuth grants read access needed for calendar selection and duplicate checks; calendar mutation is restricted to the app-created calendar.
- **External forecast boundary:** weather is user-initiated in V2 and receives only the minimum event time and location required.
- **Public portfolio boundary:** documentation and examples are synthetic; the live application, deployment configuration, and production data remain private.

## Security and reliability decisions

- OAuth state and PKCE protect the authorization flow.
- Refresh credentials are sealed with authenticated encryption in a secure, HTTP-only cookie.
- A strict Content Security Policy limits browser network destinations and keeps OCR assets same-origin.
- The deployed-worker policy blocks framing, restricts cross-origin resource use, adds HTTPS transport protection, and prevents API-response caching.
- State-changing calendar and authenticated weather requests require an exact same-origin request and JSON content type.
- OCR dependencies and models are version-pinned and integrity-checked before build.
- One pinned package manager and lockfile define the build; the release preflight rejects dependency drift and competing lockfiles.
- Image type, size, edge length, and total pixels are bounded.
- All event batches are validated before the first write.
- Deterministic event identifiers and semantic duplicate checks make retries safer.
- Delete operations re-fetch the event, verify app ownership, compare revisions, and require two confirmations.

## Product architecture decisions

- **Human-in-the-loop over autonomous entry:** accuracy and trust outweigh maximum automation.
- **Local dictionary over cloud language model:** recurring corrections improve without sending schedules to another service.
- **One-hour visible default:** speeds manual entry while keeping inference obvious and editable.
- **Week plus agenda:** supports desktop scanning and narrow-screen readability.
- **Progressive external APIs:** weather is opt-in before automatic forecasts and place autocomplete are introduced.

## Technology profile

- TypeScript and React user interface.
- Next.js-compatible routing on a Cloudflare Worker-compatible runtime.
- Google Calendar API for OAuth, calendar reads, duplicate checks, and app-owned writes/deletes.
- Browser-based PaddleOCR with ONNX Runtime Web and self-hosted model assets.
- Node.js automated tests for domain rules, integrations, source guards, and rendered safety messages.
- A private CycloneDX SBOM and third-party inventory generated from the installed dependency graph.

## Known architecture gaps

- Device-local drafts and dictionary entries do not yet synchronize.
- Shared-device identity and recovery require a formal account design.
- Full telemetry is intentionally limited; privacy-safe service health measures need definition.
- A baseline threat model, ASVS Level 2 readiness map, and security-operations runbook are documented; independent review, penetration testing, and a sanitized exercise remain future controls.
- Software composition reporting is automated, but review-required license metadata must be resolved before application source or binary distribution.
- Live security-header evidence is recorded; manual accessibility, supported-device, synthetic calendar, and independent TLS testing remain release evidence gaps.
