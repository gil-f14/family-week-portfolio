# Family Week — Security Threat Model

**Status:** Baseline design threat model  
**Scope:** Private Family Week web application and its documented integrations  
**Data rule:** Synthetic examples only; no household, account, calendar, deployment, or credential data is included  
**Assurance boundary:** This is an engineering risk assessment, not a penetration test, certification, or compliance attestation.

## Security objectives

1. Prevent unauthorized calendar reads, writes, and deletes.
2. Keep source photographs, OCR output, drafts, and family vocabulary on the user's device wherever possible.
3. Ensure uncertain OCR never causes an autonomous calendar mutation.
4. Limit a compromised component to the smallest practical data and permission boundary.
5. Make interrupted or repeated operations safe to retry.
6. Preserve a reviewable audit trail without logging sensitive event content.

## Assets and sensitivity

| Asset | Sensitivity | Required protection |
| --- | --- | --- |
| OAuth refresh credential and sealed session | Critical | Confidentiality, integrity, short exposure paths, revocation capability |
| Calendar metadata and event details | High | Least privilege, purpose limitation, no sensitive logging |
| Source schedule photograph and OCR text | High | Device-local processing, bounded retention, explicit user control |
| Reviewed event proposal | High | Validation, integrity, explicit approval before mutation |
| Family Dictionary and local draft | Moderate to high | Device-local storage, strict size limits, clear-device recovery guidance |
| Application source and deployment configuration | High | Private repository, restricted deployment access, secret scanning |
| Sanitized portfolio documents | Public | Release-gate review and exclusion of operational identifiers |

## Trust boundaries and data flows

```text
Untrusted photo or pasted text
        |
        v
Browser sandbox: validation, OCR, correction dictionary, human review
        |
        | reviewed and bounded event fields only
        v
Private application service: authorization, validation, duplicate checks
        |
        +----> Google Calendar API: approved reads and app-calendar mutations
        |
        +----> Government weather services: user-initiated minimum lookup data
```

The browser, application service, identity provider, calendar provider, forecast providers, software supply chain, and public documentation repository are separate trust boundaries. A control in one boundary is not assumed to protect another.

## Risk-rating method

Residual priority is a qualitative engineering judgment after considering the controls documented here. Likelihood uses **unlikely**, **possible**, or **likely**; impact uses **moderate**, **major**, or **severe**. A high priority means release or distribution evidence is still required, not that an incident is known to have occurred. This is not an organizational risk acceptance or a formal quantitative assessment.

## Prioritized risk register

| ID | Risk scenario and boundary | Likelihood | Impact | Residual priority | Current treatment | Required closeout evidence |
| --- | --- | --- | --- | --- | --- | --- |
| TM-01 | A forged, malformed, or confused-deputy request mutates an unauthorized calendar | Unlikely | Severe | High | State, PKCE, same-origin mutation checks, bounded identifiers, and app-calendar-only writes/deletes | Manual OAuth scope review plus approved synthetic wrong-target and revocation tests |
| TM-02 | Incorrect OCR or ambiguous time becomes a wrong event | Possible | Major | Medium | Confidence gating, explicit review, complete-batch validation, and duplicate checks | Representative synthetic OCR evaluation and approved end-to-end review test |
| TM-03 | An unlocked shared device exposes local drafts or learned vocabulary | Possible | Major | High | Seven-day draft expiry and two-step app-scoped device clearing | Supported-device verification and household operating guidance |
| TM-04 | A session credential is stolen, replayed, or retained beyond need | Unlikely | Severe | High | Authenticated encryption, secure HTTP-only cookie, expiry validation, and disconnect path | Manual expiry, disconnect, provider-revocation, and recovery evidence |
| TM-05 | A compromised or mislicensed dependency affects the browser or distributed artifact | Possible | Severe | High | Locked dependencies, integrity-pinned OCR assets, SBOM, inventory, build scan, and closed distribution gate | Independent security review plus qualified resolution of all license-review rows |
| TM-06 | Public portfolio history reveals personal, credential, or operational information | Unlikely | Severe | Medium | Documentation-only allowlist, synthetic examples, new history, and automated secret/PII checks | Human pre-publication review after every new artifact or media type |
| TM-07 | Adversarial input or excessive reads exhaust browser or provider resources | Possible | Moderate | Medium | Image bounds, confidence limits, readable-calendar cap, and fail-closed errors | Measured performance budgets and provider-side throttling review |
| TM-08 | A keyboard, screen-reader, zoom, motion, or touch user cannot safely review an action | Possible | Major | High | Dialog semantics, focus controls, responsive containment, contrast checks, reduced-motion handling, and explicit review states | Complete the documented manual accessibility and supported-device matrix |

No high-priority row is accepted or closed by this document. The private pilot remains gated by its stated manual checks, and application-source or binary distribution remains blocked separately by the license review.

## Threat actors and assumptions

- An unauthenticated internet user attempting to reach the private application.
- An authenticated user making an accidental, repeated, or malformed request.
- Malicious text or image input designed to exhaust resources or manipulate parsing.
- A script-injection or dependency compromise attempting to access browser or session data.
- An attacker with access to a lost, shared, or unlocked device.
- A repository observer searching public history for credentials or personal information.
- A compromised external service returning malicious or unexpected data.

The model assumes the hosting and identity providers enforce their documented platform controls, TLS is correctly implemented, the user's endpoint is not fully compromised, and provider credentials can be revoked. These assumptions require periodic validation.

## STRIDE assessment

| Category | Primary threat | Existing preventive or detective controls | Residual risk and next control |
| --- | --- | --- | --- |
| Spoofing | Forged login or OAuth callback | Provider authentication, OAuth state, PKCE, sealed session, secure HTTP-only cookie | Validate session expiry and revocation during manual end-to-end testing |
| Spoofing | User selects an unauthorized write target | Server-side calendar allowlist and app-created-calendar ownership check | Independently test scope and confused-deputy failure cases |
| Tampering | Event fields or identifiers changed after review | Server validation, bounded fields, reviewed-event requirement, safe identifier validation | Add structured security-event logging without event content |
| Tampering | Delete races with a later calendar edit | Re-fetch, app-ownership verification, revision comparison, two confirmations | Complete live synthetic concurrency test |
| Repudiation | Calendar mutation cannot be reconstructed | Deterministic identifiers and explicit review flow | Define content-free audit events, retention, access, and deletion policy |
| Information disclosure | Photograph or OCR text remains on a shared device | Browser-based OCR, no photo upload, bounded local draft, and a two-step app-scoped device reset | Verify the reset on supported devices and educate shared-device users to run it |
| Information disclosure | OAuth credential or calendar content reaches logs or public source | Sealed credential, private source, no-sensitive-logging rule, history scans, public release gate | Add automated log-field tests and an incident response exercise |
| Information disclosure | Public portfolio reveals operational details | Documentation-only allowlist, synthetic content, PII and secret scans, separate Git history | Re-run the release gate before every new media or source addition |
| Denial of service | Oversized or adversarial image exhausts browser resources | File-size, edge-length, pixel-count, and OCR confidence limits | Add measured performance budgets and service-side request throttling where supported |
| Denial of service | Excessive calendar overlay or duplicate reads | Unique readable-calendar selection and strict selection cap | Add privacy-safe latency and failure-rate monitoring |
| Elevation of privilege | Read access becomes broad write access | Read scopes for duplicate checks; writes and deletes restricted to the dedicated app calendar | Perform a formal OAuth scope review and provider-console evidence capture |
| Elevation of privilege | Script injection accesses application state | React output encoding, restrictive Content Security Policy, same-origin assets, no arbitrary forecast host | Run an independent ASVS-oriented application review and penetration test |

## Misuse and safety cases

| Scenario | Expected safe behavior |
| --- | --- |
| OCR is low confidence | Show uncertainty and require correction; do not create an event |
| A time is ambiguous | Require user review rather than guessing AM or PM |
| Submission is repeated after interruption | Detect the existing event and avoid a duplicate |
| A delete targets a read-only or unrelated event | Refuse the mutation and offer the provider link when available |
| A forecast service returns an unexpected host | Reject the response rather than following the URL |
| Local storage is malformed or oversized | Normalize, bound, or discard it without sending it elsewhere |
| A public-document scan detects sensitive data | Stop publication, contain access, rotate credentials if needed, and clean history before republishing |

## Highest residual risks

1. **TM-01 and TM-04:** OAuth scope, revocation, recovery, and wrong-target behavior still need approved manual evidence.
2. **TM-03:** a lost or shared unlocked device can expose device-local drafts and dictionary entries until the user runs the available clear-device control.
3. **TM-08:** manual accessibility and supported-device testing has not been completed.
4. **TM-02:** live create, duplicate, retry, revision-conflict, and delete behavior still requires an approved synthetic end-to-end test.
5. **TM-05:** an independent penetration test, requirement-by-requirement OWASP ASVS review, and qualified distribution-license review have not been performed.
6. Privacy-safe operational monitoring and audit retention are not fully defined.

## Verification plan

- Run the production build, lint, automated tests, dependency audit, and complete-history secret scan before a release.
- Test OAuth expiry, disconnect, revocation, and callback failure without exposing tokens.
- Use a disposable synthetic event to test create, duplicate detection, interrupted retry, update conflict, and two-stage delete.
- Test keyboard-only operation, screen readers, zoom/reflow, orientation, contrast, reduced motion, and touch targets on supported devices.
- Verify the application remains private and that only the dedicated calendar accepts mutations.
- Revisit this model after any authentication, storage, telemetry, synchronization, weather, place-search, or sharing change.

## Standards traceability

- [NIST Cybersecurity Framework 2.0](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20): Govern, Identify, Protect, Detect, Respond, and Recover are used as risk-management outcomes.
- [NIST SP 800-218 SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final): secure design, dependency management, verification, and release evidence guide the development controls.
- [NIST SP 800-122](https://csrc.nist.gov/pubs/sp/800/122/final): data minimization and contextual PII protection inform the privacy boundary.
- [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/): future independent verification baseline; no ASVS verification claim is made.
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/): accessibility engineering target; conformance is not claimed.

## Review triggers

Update and reapprove this threat model when the application adds a new identity, external API, server-side storage system, synchronization path, shared-device role, public endpoint, sensitive log, or source-distribution channel—or when a security incident invalidates an assumption.
