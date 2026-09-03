# Family Week — Privacy-Safe Monitoring Plan

**Status:** Content-free monitoring specification; instrumentation and alert routing are not yet implemented  
**Scope:** Private-pilot availability, access posture, authentication boundaries, calendar-operation outcomes, release integrity, and incident signals  
**Claim boundary:** This plan is not evidence that monitoring is operating, that alerts meet a service level, or that the product complies with a standard.

## Monitoring principles

- Detect failures without collecting household content.
- Prefer counters, durations, version references, and fixed reason codes over request or response bodies.
- Never place photos, OCR text, event titles, notes, locations, calendar names, account identifiers, credentials, session values, authorization codes, IP addresses, or full user-agent strings in application telemetry.
- Keep monitoring access private and least privilege; do not place operational dashboards or alerts in the public portfolio.
- Treat an unexpected access-policy expansion or calendar authorization failure as a security signal, not merely a reliability issue.
- Require human approval for calendar recovery; monitoring must never trigger automatic event creation, deletion, or restoration.

## Approved event schema

Every application-generated event is limited to these fields:

| Field | Allowed content |
| --- | --- |
| `occurred_at` | Rounded UTC timestamp |
| `event_type` | Fixed allowlisted name from the table below |
| `outcome` | `success`, `denied`, `failed`, or `degraded` |
| `reason_code` | Fixed allowlisted code with no provider response text |
| `duration_bucket` | Coarse range such as under one second, one-to-five seconds, or over five seconds |
| `release_ref` | Non-secret application version reference |
| `count` | Integer aggregate; never a household or account identifier |

Free-form fields, request bodies, response bodies, URLs with query strings, cookies, headers, and stack traces containing request data are prohibited. Diagnostic detail that cannot meet this schema stays in short-lived, access-restricted incident evidence and follows the security runbook.

## Event and control catalog

| Event type | Safe reason examples | Detection purpose | Starting alert target |
| --- | --- | --- | --- |
| `deployment_health` | `unreachable`, `server_error`, `header_policy_mismatch` | Availability and security-header regression | High when two consecutive independent checks fail; critical for confirmed header-policy removal on the live private service |
| `access_policy_check` | `owner_only`, `unexpected_viewer`, `unexpected_group`, `public_mode` | Detect broadened site access | Critical on any result other than the approved owner-only posture |
| `oauth_boundary` | `state_rejected`, `session_expired`, `provider_denied`, `callback_failed` | Detect authentication breakage or repeated abuse | High when failures exceed ten in fifteen minutes; investigate single state-validation regressions after a release |
| `calendar_read` | `provider_unavailable`, `scope_denied`, `rate_limited`, `invalid_request` | Detect week-view and duplicate-check failures | High when more than five failures occur in fifteen minutes or success rate falls below ninety-five percent in an hour |
| `calendar_mutation` | `validation_denied`, `origin_denied`, `wrong_target_denied`, `revision_conflict`, `provider_failed`, `success` | Detect unsafe or unreliable create/delete attempts | Critical for any confirmed wrong-target success; high for repeated provider failures; retain only counts and fixed codes |
| `release_gate` | `passed`, `failed_build`, `failed_test`, `inventory_stale`, `privacy_scan_failed` | Prevent unverified deployment | Block release on every failure; high if a failed gate is bypassed |
| `dependency_signal` | `critical_advisory`, `high_advisory`, `integrity_mismatch`, `license_review_required` | Detect supply-chain changes | Follow the documented severity and distribution gates |

Thresholds are conservative private-pilot starting points. They must be tuned from content-free operating evidence and approved before broader service-level commitments.

## Collection boundaries

- Client-side OCR, photos, extracted text, dictionary entries, drafts, display preferences, and device clearing produce no server telemetry.
- Authentication and calendar events are recorded only after server-side classification into the fixed schema.
- Provider error messages are mapped to allowlisted reason codes before recording; raw messages are not logged.
- Platform-generated logs must be reviewed for default IP, request-header, query-string, and user-agent collection. Disable or minimize those fields where the platform permits; otherwise restrict access and retention and document the residual risk.
- Synthetic health checks use read-only endpoints and never open a live calendar, refresh a user session, or perform a calendar mutation.

## Retention and access target

| Record | Starting retention target | Access |
| --- | --- | --- |
| Content-free application events | 14 days | Named operations and security maintainers only |
| Aggregated counts with no stable user or device identifier | 90 days | Product and security reviewers |
| Alert and incident decision record | Per the approved incident-retention policy | Incident owner and explicitly authorized reviewers |
| Public portfolio evidence | Sanitized summaries only; no operational events | Public after the separate release gate |

Retention starts only after the owner approves the monitoring implementation and confirms provider-default logging. Legal, contractual, and provider obligations may require a different schedule and must be reviewed before activation.

## Alert handling

1. Route alerts to a private channel with the event type, outcome, fixed reason, count, rounded time, severity, and runbook link only.
2. Do not paste raw logs or calendar/provider payloads into an alert.
3. Use the security-operations runbook for triage, containment, recovery approval, and sanitized closure evidence.
4. Deduplicate repeated alerts by event type and time window without adding a user or account identifier.
5. Escalate an access-policy expansion, credential exposure, or confirmed unauthorized mutation immediately under the critical playbook.

## Verification before activation

- Unit-test the field allowlist and reject every unknown or free-form field.
- Use synthetic fixed-code events to test each threshold and alert route.
- Confirm alerts contain none of the prohibited content categories.
- Verify retention deletion and access review with sanitized evidence.
- Run read-only deployment and access-policy checks without authenticated calendar access.
- Confirm monitoring failure cannot bypass the release gate or trigger a calendar mutation.
- Obtain independent privacy and security review before treating this plan as an operating control.

## NIST-aligned outcome mapping

This specification supports Detect, Respond, and Govern outcomes in the project's NIST CSF 2.0 profile and the data-minimization objectives in its Privacy Framework profile. Implementation, operating evidence, exercises, and independent assessment remain required; no compliance or certification claim is made.
