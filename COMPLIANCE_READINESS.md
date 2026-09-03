# Family Week — Security, Privacy, and Accessibility Readiness

**Assessment type:** Internal design and evidence mapping  
**Assessment date:** September 2026  
**Claim boundary:** This is not a certification, legal opinion, audit, attestation, or formal conformance report.

## How to read this document

- **Implemented and evidenced** means the repository contains a corresponding design or automated test.
- **Partially aligned** means relevant controls exist but the framework has not been assessed completely.
- **Target** means the standard guides implementation and testing, but conformance is not claimed.
- **Not assessed** means no readiness claim should be made.

## Standards summary

| Framework or standard | Current posture | Evidence in the product | What is still required |
| --- | --- | --- | --- |
| [NIST Cybersecurity Framework 2.0](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20) | Partially aligned | Governance rules, data boundaries, least privilege, protective controls, failure states, rollback, a security-operations runbook, and a product-level current/target engineering profile across Govern, Identify, Protect, Detect, Respond, and Recover | Formal organizational profile, approved risk tolerance, runbook exercise evidence, and independent review |
| [NIST SP 800-218 SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final) | Partially aligned | Pinned dependencies, integrity-checked OCR assets, reviewed changes, automated tests, build gates, baseline threat model, private SBOM, and documented release rules | Vulnerability-management SLA, provenance record, license resolution, and independent security testing |
| [NIST SP 800-122](https://csrc.nist.gov/pubs/sp/800/122/final) | Strong design alignment | Local photo processing, data minimization, owner-only hosting, prohibited-public-data list, clean-export rule, privacy-impact assessment, and incident response | Approve the retention schedule and PII confidentiality-impact rating; complete access review and incident exercise |
| [NIST Privacy Framework 1.0](https://www.nist.gov/privacy-framework) | Partially aligned | Data inventory, processing boundaries, minimization, user review, private-by-default operation, release gates, current/target profile, privacy-impact assessment, and scoped device-data deletion | Approved privacy notice and retention policy, operating evidence, supported-device reset testing, and independent review; monitor revisions without claiming a draft as final |
| [NIST AI RMF 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10) | Partially aligned for OCR | Human review, visible uncertainty, bounded inputs, source comparison, confidence handling, local correction, and failure-safe behavior align to Govern, Map, Measure, and Manage concepts | Document model limitations, representative evaluation set, accuracy measures, bias/accessibility review, monitoring, and change criteria; AI RMF 1.0 is currently under revision |
| [WCAG 2.2 Level AA](https://www.w3.org/TR/WCAG22/) | Target; near-ready engineering controls | Semantic dialog behavior, focus trapping/restoration, Escape close, full event-date labels, live status/alert roles, responsive viewport containment, touch-sized controls, and no forced autofocus | Full-page automated audit plus manual keyboard, screen-reader, contrast, 200%/400% zoom, reflow, orientation, and supported-browser testing; remediate all A/AA failures before a conformance claim |
| [Revised Section 508](https://www.section508.gov/buy/determine-ict-standards/) | Readiness target only; applicability not established | WCAG-oriented engineering supports the web accessibility baseline | Legal/applicability determination and systematic testing against all applicable web software, interoperability, documentation, support, and functional-performance requirements |
| [OWASP ASVS 5.0.0](https://owasp.org/www-project-application-security-verification-standard/) | Level 2 target selected; not verified | Chapter-level readiness matrix plus authentication, session, validation, CSP, access-control, supply-chain, and safe-error evidence | Complete a requirement-by-requirement Level 2 trace, test it, resolve gaps, and obtain independent review before citing verification |

## Implemented control evidence

### Security and identity

- OAuth authorization uses state and PKCE.
- Session data is authenticated and encrypted before it is stored in a secure, HTTP-only cookie.
- The deployed application is private and owner-only.
- Browser Content Security Policy restricts connection and execution destinations.
- Secrets and OAuth configuration are supplied at runtime rather than embedded in source.

### Privacy

- Source photos and extracted text stay in the browser during the normal workflow.
- Drafts and learned corrections are device-local.
- A two-step, app-scoped device reset clears the draft, learned corrections, photo preview, and display preferences without deleting calendar events, disconnecting Google, or clearing unrelated site data.
- The application does not use a remote language model to learn household corrections.
- Operational guidance excludes event details, photos, locations, and credentials from logs.
- Public portfolio artifacts are separated from the production repository and use synthetic data.

### Calendar safety

- Read access supports duplicate checking across approved calendars.
- Writes and deletes are limited to the app-created calendar.
- Every batch is validated before its first write.
- Deterministic identifiers and semantic duplicate checks reduce retry risk.
- Deletion verifies app ownership and revision before the final mutation.

### OCR and AI risk

- Model and runtime versions are pinned.
- OCR model assets are self-hosted and checked against recorded SHA-256 digests.
- File type, byte size, dimensions, and pixel count are bounded.
- Low-confidence output is not silently promoted to a calendar write.
- The source image remains available for human comparison.

### Accessibility

- Dialogs expose programmatic roles and labels.
- Keyboard focus is contained while modal surfaces are open and returns to the trigger when they close.
- Escape and outside-click dismissal are supported where appropriate.
- Calendar event controls include full date context for assistive technology.
- Status and error updates use live semantic roles.
- Mobile pop-outs respect the viewport and safe areas and scroll independently.

## Claims that must not be made yet

- “NIST certified,” “NIST compliant,” or “NIST approved.”
- “WCAG 2.2 AA compliant” or “accessibility certified.”
- “Section 508 compliant.”
- “OWASP ASVS verified.”
- “Production-ready for public or multi-tenant use.”
- “Zero risk,” “fully secure,” or “guaranteed private.”

## Approved portfolio language

> Family Week is a private-pilot, privacy-first calendar assistant built with NIST-aligned risk-management practices and a WCAG 2.2 Level AA accessibility target. The implementation includes least-privilege calendar access, on-device OCR, human approval, duplicate prevention, encrypted sessions, and release gates. Formal conformance and certification have not been claimed; manual accessibility testing, complete framework assessments, and independent security validation remain on the roadmap.

## Priority evidence backlog

1. Execute the pending human and supported-device rows in the accessibility test record.
2. Resolve the private software inventory's review-required license entries before any application distribution.
3. Record an end-to-end calendar create, duplicate, and delete test using synthetic data.
4. Complete the OWASP ASVS 5.0.0 Level 2 requirement trace defined in the readiness matrix.
5. Convert the product-level NIST engineering profile into a formal organizational profile only if broader deployment makes that useful.
6. Obtain independent review before upgrading any readiness statement to a conformance claim.
