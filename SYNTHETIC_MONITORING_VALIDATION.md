# Family Week — Synthetic Monitoring Validation Plan

**Status:** Schema and local threshold cases automated; instrumentation, retention jobs, access enforcement, and alert routing remain inactive
**Scope:** Content-free event validation, thresholds, retention, access, and fail-safe behavior  
**Claim boundary:** This plan is not operating evidence and does not demonstrate monitoring coverage, alert delivery, service levels, incident response, or compliance.

## Safety rules

- Use fixed synthetic event types, reason codes, rounded times, duration buckets, release references, and integer counts only.
- Never use photos, OCR text, event titles, notes, locations, calendar names, account identifiers, credentials, session values, authorization codes, IP addresses, full user agents, provider messages, URLs, cookies, request bodies, or response bodies.
- Do not contact a live calendar, refresh a session, mutate an event, broaden access, or send an external alert.
- Keep all test routing local or to a non-delivering synthetic sink until the owner separately approves activation.

## Schema validation cases

| ID | Synthetic input | Expected result |
| --- | --- | --- |
| MON-01 | Every approved field with fixed allowlisted values | Accept |
| MON-02 | Unknown field | Reject the complete event |
| MON-03 | Free-form provider message in `reason_code` | Reject the complete event |
| MON-04 | Timestamp with second-level or finer precision | Reject or round before record creation |
| MON-05 | Negative, fractional, or identifier-like `count` | Reject |
| MON-06 | URL, query string, header, cookie, stack trace, or request body | Reject |
| MON-07 | Event title, OCR text, address, account value, or credential-shaped content in any field | Reject and create no fallback log containing the value |

## Threshold cases

| ID | Synthetic signal | Expected local decision |
| --- | --- | --- |
| MON-08 | Two consecutive independent deployment failures | High |
| MON-09 | Any access-policy result other than owner-only | Critical |
| MON-10 | Eleven OAuth-boundary failures inside fifteen minutes | High |
| MON-11 | Six calendar-read failures inside fifteen minutes | High |
| MON-12 | Hourly calendar-read success rate below ninety-five percent | High |
| MON-13 | Confirmed wrong-target mutation success | Critical; require human containment and recovery approval |
| MON-14 | Any failed release-gate event | Block release |
| MON-15 | Dependency integrity mismatch | Follow the vulnerability and distribution gates; do not release |

## Retention and access cases

| ID | Synthetic condition | Expected result |
| --- | --- | --- |
| MON-16 | Content-free application event reaches fourteen days | Delete under the approved retention job |
| MON-17 | Identifier-free aggregate reaches ninety days | Delete under the approved retention job |
| MON-18 | Unauthorized role requests raw or aggregate records | Deny and record only a fixed access decision |
| MON-19 | Deletion job fails | Raise a content-free operational signal without extending retention silently |

## Fail-safe cases

| ID | Synthetic condition | Expected result |
| --- | --- | --- |
| MON-20 | Monitoring validator is unavailable | Application fails without bypassing the release gate or emitting unvalidated telemetry |
| MON-21 | Alert route is unavailable | Preserve the bounded local decision state; do not add payload detail or retry indefinitely |
| MON-22 | Recovery action would create, delete, or restore a calendar event | Stop and require explicit human approval through the normal guarded workflow |

## Evidence record

For each executed case, retain only the case ID, implementation version, rounded execution date, pass/fail, fixed failure reason, reviewer role, and corrective-action reference. Evidence must not contain a raw event payload, live route, account value, provider response, screenshot, or operational identifier.

## Exit criteria before activation

1. Every schema rejection, threshold, retention, access, and fail-safe case passes with synthetic data.
2. A privacy reviewer confirms prohibited values cannot enter primary, fallback, error, or alert records.
3. A security reviewer confirms monitoring failure cannot bypass a release gate or trigger a calendar mutation.
4. The owner approves retention, named access roles, a private alert destination, and rollback.
5. An authorized non-delivering drill produces sanitized evidence before any external alert route is enabled.

Until these criteria are met, monitoring remains a specification and test plan rather than an operating control.

## Current evidence boundary

Automated tests exercise MON-01 through MON-15 against a pure validator and threshold evaluator with no storage or network side effects. MON-16 through MON-22 require future retention, access-control, routing, and operational-drill implementations. None of these results demonstrates live monitoring or alert delivery.
