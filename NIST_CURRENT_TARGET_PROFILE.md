# Family Week — NIST Current and Target Engineering Profile

**Assessment date:** September 2026  
**Scope:** Private single-household pilot and its sanitized documentation release  
**Frameworks:** NIST Cybersecurity Framework 2.0 and NIST Privacy Framework 1.0  
**Claim boundary:** This is a product-level prioritization aid, not a formal organizational profile, audit, certification, legal opinion, or statement of compliance.

## Method

NIST describes profiles as a way to express current and target outcomes and prioritize gaps. This lightweight engineering profile uses the CSF 2.0 Functions—Govern, Identify, Protect, Detect, Respond, and Recover—and the Privacy Framework Functions—Identify-P, Govern-P, Control-P, Communicate-P, and Protect-P.

Ratings mean:

- **Implemented:** repeatable repository or platform evidence exists for this product boundary.
- **Partial:** meaningful controls exist, but ownership, operating evidence, or independent validation is incomplete.
- **Planned:** the target is documented but material implementation evidence is not complete.

No NIST Implementation Tier is assigned. Tier selection requires a broader organizational assessment of governance, resources, workforce, and risk-management practices.

## CSF 2.0 current and target profile

| Function | Current posture | Current evidence | Target outcome | Priority evidence or action | Accountable role | Target phase |
| --- | --- | --- | --- | --- | --- | --- |
| Govern | Partial | Private-by-default rules, release gates, claim boundaries, roadmap ownership, and documented access decisions | A repeatable risk-governance process with reviewed policies, risk appetite, exception handling, supplier decisions, and review cadence | Maintain a risk register; define exception expiry and quarterly control review | Product owner / Security reviewer | V2 closeout |
| Identify | Implemented for current design scope | Asset and data classifications, trust boundaries, threat model, dependency inventory, SBOM, and documented external services | An inventory that remains current across code, providers, credentials, data flows, dependencies, devices, and supported users | Add an owner, review date, and change trigger to every inventory; reconcile against deployment settings | Engineering owner | V2 operations |
| Protect | Partial | Owner-only hosting, least-privilege calendar boundaries, sealed sessions, on-device OCR, bounded input, CSP, review-before-write, protected deletion, and a scoped two-step local-data reset | Tested preventive controls for identity lifecycle, shared-device privacy, retention, recovery, and supported endpoints | Test reset on supported devices; test disconnect/revocation; independently review access control | Engineering owner / Privacy reviewer | V2 closeout |
| Detect | Partial | GitHub secret, dependency, and push-protection monitoring; build integrity checks; visible application failure states; content-free monitoring schema, thresholds, and retention targets | Privacy-safe detection across authentication failures, calendar API errors, security control changes, and deployment health | Implement the approved schema; test field rejection, retention, and alert routing with synthetic signals | Operations owner | V2 operations |
| Respond | Partial | Private vulnerability reporting, containment and credential-rotation guidance, rollback rules, and stop-work conditions | A tested incident process covering triage, containment, evidence protection, notification decisions, and lessons learned | Run a synthetic tabletop; record response roles, severity definitions, contacts, and decision log | Incident owner / Product owner | V2 operations |
| Recover | Partial | Known-good private deployment, version rollback path, retry-safe identifiers, duplicate checks, and cleanup procedures | Tested restoration with recovery objectives, verified configuration, post-incident validation, and stakeholder communication | Define recovery-time and recovery-point objectives; rehearse rollback and configuration validation | Operations owner | Before broader access |

## Privacy Framework current and target profile

| Function | Current posture | Current evidence | Target outcome | Priority evidence or action | Accountable role | Target phase |
| --- | --- | --- | --- | --- | --- | --- |
| Identify-P | Implemented for current design scope | Data-flow map, sensitivity classification, local-versus-server boundaries, external-service inventory, misuse cases, and a synthetic privacy-impact and retention assessment | A maintained record of processing purposes, data elements, locations, recipients, retention, and risks to individuals | Independently review the privacy assessment and assign its recurring review cadence | Privacy reviewer / Product owner | V2 closeout |
| Govern-P | Partial | Data-minimization rules, public-release boundary, standards claim policy, human approval, and access restrictions | Approved privacy roles, policies, risk tolerance, retention schedule, access reviews, and supplier criteria | Assign review cadence; document exception handling, deletion expectations, and provider reassessment | Product owner / Privacy reviewer | V2 operations |
| Control-P | Partial | User reviews OCR and event details, chooses readable calendar overlays, controls calendar mutations, and has a two-step reset for app-specific device-local data | Clear controls for viewing, correcting, deleting, exporting, and resetting device-local data without hidden synchronization | Test reset behavior and messaging on supported devices; complete independent privacy review | Product owner / Design owner | V2 closeout |
| Communicate-P | Partial | In-product local-processing messages, visible uncertainty, portfolio claim boundaries, and security reporting instructions | A concise user-facing privacy notice that explains processing, storage, sharing, choices, retention, and support | Draft and independently review the notice before adding shared users | Product owner / Privacy reviewer | Before broader access |
| Protect-P | Partial | Same-origin OCR assets, input bounds, secure session cookie, owner-only hosting, CSP, no-sensitive-logging rule, and restricted calendar writes | Independently tested confidentiality, integrity, identity lifecycle, endpoint, logging, and disposal controls | Complete manual device tests, log-field safeguards, penetration testing, and revocation exercises | Security reviewer / Engineering owner | Before broader access |

## Prioritized gap register

| Priority | Gap | Risk | Planned treatment | Completion evidence |
| --- | --- | --- | --- | --- |
| P0 | Live calendar safety has not completed the approved synthetic test sequence | Incorrect or unrecoverable calendar mutation | Execute create, duplicate, uncertain retry, revision conflict, and two-stage delete plan | Signed text-only test record with zero synthetic records remaining |
| P0 | Manual accessibility and supported-device testing is incomplete | A user may be blocked from critical review or calendar actions | Execute the accessibility record on declared supported browsers and devices | Recorded results, remediated Level A/AA failures, independent review |
| P2 | Device-local reset needs manual supported-device evidence | Shared or lost device may expose drafts or learned corrections if the control fails on that device | Keep the consolidated reset fail-closed and test it on supported browsers | Automated scope test plus manual reset record |
| P1 | Privacy-safe operational detection is specified but not operating | Security or reliability failures may be missed | Implement the allowlisted schema and approved alert routes without household content | Field-rejection, retention, and synthetic alert tests |
| P1 | Incident and recovery procedures are not exercised | Slow or inconsistent containment and restoration | Run synthetic tabletop and rollback rehearsal | Completed exercise record and corrective actions |
| P1 | Eleven software-license entries require review before distribution | Source or binary distribution could miss obligations | Resolve metadata and package required notices and license texts | Independent license review and approved distribution bundle |
| P2 | Provider and dependency reassessment has no fixed cadence | Controls may drift as services and packages change | Establish quarterly review and change-trigger review | Dated review log with named roles |

## Measures

- Zero unauthorized calendar mutations in synthetic release tests.
- Zero unresolved critical or high dependency/security findings at release.
- Zero sensitive-data findings in public documentation history.
- One hundred percent of supported critical flows manually tested for keyboard and screen-reader operation before a conformance assessment.
- One hundred percent of declared external services, credentials, and sensitive data flows assigned an owner and review date.
- Incident containment and private rollback exercised before broader access.

## Review cadence and triggers

Review this profile quarterly during active development and immediately after any new identity, shared-user role, storage or synchronization path, telemetry field, external API, distribution channel, security incident, or material standards revision. Record changes without adding personal data or operational identifiers to the public portfolio.

## References

- [NIST CSF 2.0 Resource and Overview Guide](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.1299.pdf)
- [NIST Privacy Framework frequently asked questions](https://www.nist.gov/privacy-framework/frequently-asked-questions)

Use of either voluntary framework does not guarantee legal or regulatory compliance. Any future formal profile must select applicable Core outcomes, document organizational context and risk tolerance, and receive independent review.
