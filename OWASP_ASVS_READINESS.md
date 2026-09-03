# Family Week — OWASP ASVS Readiness Matrix

**Reference baseline:** OWASP Application Security Verification Standard (ASVS) 5.0.0  
**Target:** Level 2  
**Status:** Readiness mapping only; not verified, certified, audited, or independently assessed  
**Scope:** The private Family Week web application and its calendar integration

## Why Level 2

Level 2 is the working target because the application processes private calendar information and authorization tokens. Level 1 remains the minimum baseline, while Level 3 would require a separate risk decision and substantially deeper assurance. Selecting Level 2 does not mean Family Week satisfies it.

This public-safe matrix summarizes engineering evidence by control area. It is not the requirement-by-requirement trace needed for an ASVS verification claim. Detailed source, configuration, provider-console evidence, and test artifacts remain private.

## Readiness matrix

| Control area | Current evidence | Status | Priority gap | Accountable role |
| --- | --- | --- | --- | --- |
| Architecture, design, and threat modeling | Documented trust boundaries, STRIDE threat model, private-by-default deployment, and constrained calendar mutation boundary | Partially evidenced | Map every applicable ASVS 5.0.0 Level 2 requirement and record design-review evidence | Security reviewer |
| Authentication | OAuth authorization with state and PKCE; provider-managed user authentication | Partially evidenced | Verify provider-console configuration, redirect restrictions, account recovery, and negative paths | Engineering owner |
| Session management | Authenticated and encrypted session state in secure, HTTP-only cookies | Partially evidenced | Test expiry, renewal, revocation, logout, replay resistance, and key rotation | Security reviewer |
| Authorization | Owner-only hosting; calendar writes and deletes restricted to the app-created calendar | Partially evidenced | Add live horizontal/vertical authorization tests and document deny-by-default decisions | Engineering owner |
| Input validation and encoding | Whole-batch validation before mutation; bounded image type, size, dimensions, and pixels; reviewed event fields | Partially evidenced | Add upload fuzzing, parser boundary tests, and output-context review | Engineering owner |
| Stored cryptography | Authenticated encryption protects session contents; secrets are runtime supplied | Partially evidenced | Perform a formal algorithm, key custody, rotation, failure, and backup review | Security reviewer |
| Error handling and logging | Fail-closed validation and user-safe errors; policy prohibits sensitive calendar or credential logging | Partially evidenced | Prove production log redaction, alerting, retention, and access controls | Operations owner |
| Data protection and privacy | Browser-local photo processing, local drafts and corrections, data minimization, and sanitized public artifacts | Partially evidenced | Approve retention/deletion rules and complete a privacy-impact assessment | Product owner |
| Communications security | HTTPS hosting, a restrictive Content Security Policy, and sanitized live security-header evidence | Partially evidenced | Independently evaluate TLS configuration plus downgrade and failure behavior | Operations owner |
| Supply chain and malicious-code controls | Pinned dependencies, integrity-checked OCR assets, private CycloneDX SBOM, license inventory, and secret/history scans | Partially evidenced | Resolve review-required licenses; add provenance and vulnerability-response evidence | Security reviewer |
| Business logic | Human approval, duplicate checks, deterministic event identifiers, revision checks, and two confirmations for deletion | Partially evidenced | Execute synthetic abuse, concurrency, retry, quota, and rate-limit scenarios | Product owner |
| Files and resources | Photos are bounded and processed locally; low-confidence extraction does not silently write events | Partially evidenced | Add malformed-image, decompression, memory-pressure, and browser-isolation tests | Engineering owner |
| API and web services | Calendar identifiers are constrained; selected overlays are capped; duplicate checks precede approved writes | Partially evidenced | Run authenticated negative tests for scope, object access, batching, quotas, and provider errors | Engineering owner |
| Configuration | Runtime secrets, owner-only access, exact outbound destinations, and private source boundaries are documented | Partially evidenced | Create a hardened configuration baseline and capture drift-resistant deployment evidence | Operations owner |

## Verification work package

1. Obtain the official ASVS 5.0.0 requirement list and freeze that version in the assessment record.
2. Record every Level 2 requirement as **Pass**, **Fail**, or **Not applicable**; include a rationale for every not-applicable decision.
3. Link each pass to reproducible evidence such as a test, reviewed source location, configuration capture, or operating record.
4. Resolve every critical or high-risk failure and record disposition of lower-risk gaps.
5. Have a reviewer independent of the implementation confirm scope, applicability, evidence, and results.
6. Repeat affected checks after material authentication, authorization, storage, dependency, hosting, or calendar-integration changes.

## Exit criteria for an “ASVS verified” statement

Family Week must not be described as ASVS verified until all of the following are true:

- every applicable ASVS 5.0.0 Level 2 requirement identifier is mapped;
- each mapped requirement has dated, reproducible evidence and a pass/fail result;
- every not-applicable item has an approved technical rationale;
- no unresolved critical or high-risk failure remains;
- independent review confirms the application boundary and evidence; and
- the statement names the exact ASVS version, level, application version, scope, assessor, and assessment date.

## Public claim boundary

Approved wording: “Family Week uses OWASP ASVS 5.0.0 Level 2 as a security-verification target and has begun an internal readiness mapping.”

Prohibited until the exit criteria are met: “ASVS compliant,” “ASVS certified,” “ASVS approved,” or “OWASP verified.” This matrix does not establish security certification or guarantee that the application is free from vulnerabilities.
