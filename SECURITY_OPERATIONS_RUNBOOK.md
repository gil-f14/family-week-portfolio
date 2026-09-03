# Family Week — Security Operations Runbook

**Status:** Internal operating target for a private pilot  
**Scope:** The private application, its source repository, hosted configuration, authorization integration, and app-created calendar  
**Claim boundary:** This is not a certification, audit, legal opinion, or guarantee of response time.

## Operating principles

- Protect people and private calendar information before preserving service availability.
- Keep the site and application source private during investigation.
- Stop further exposure or mutation before attempting cleanup.
- Revoke or rotate exposed credentials before rewriting repository history.
- Collect the minimum evidence necessary and never copy calendar details, photos, tokens, or credentials into tickets or chat.
- Require human approval before restoring, deleting, or recreating calendar records.

## Severity and working response targets

These are internal goals for prioritization, not contractual service levels.

| Severity | Example | Acknowledge target | Containment target | Resolution or accepted plan |
| --- | --- | --- | --- | --- |
| Critical | Active credential exposure, unauthorized calendar mutation, public disclosure of private data | 4 hours | 24 hours | 3 business days |
| High | Exploitable authorization failure, stored-session compromise, high-impact dependency issue | 1 business day | 3 business days | 10 business days |
| Medium | Security weakness requiring authenticated access or significant user action | 3 business days | 10 business days | 30 days |
| Low | Defense-in-depth improvement with no demonstrated exposure | 5 business days | As scheduled | Next planned release |

If the operator cannot safely meet a target, the application remains private or unavailable until risk is accepted by the accountable owner.

## Triage record

Record only sanitized metadata:

- discovery time and reporting channel;
- affected application version and control boundary;
- severity, decision owner, and current containment state;
- whether credentials, personal data, or calendar mutations may be involved;
- evidence location with access restrictions, not evidence contents;
- actions, approvals, validation results, and closure time.

Do not record event titles, attendees, notes, addresses, photographs, extracted text, account identifiers, session values, authorization codes, or secret material.

## Response playbooks

### Suspected credential or session exposure

1. Keep or make the affected service and repository private.
2. Revoke the affected provider grant and rotate the exposed secret or key; rotating the session-sealing secret must invalidate existing sessions.
3. Stop deployments until the source and complete relevant history pass secret scanning.
4. Inspect only sanitized access metadata for use after the earliest possible exposure time.
5. Reauthorize with least privilege, run the automated release preflight, and obtain human approval before restoring access.

### Unauthorized or uncertain calendar mutation

1. Disconnect authorization or make the application unavailable to stop additional changes.
2. Do not perform bulk deletion or restoration automatically.
3. Identify only app-owned records using constrained application metadata and compare them with provider history.
4. Present proposed recovery actions to the calendar owner for explicit approval.
5. Restore or delete one bounded batch, verify the result, and preserve a sanitized count-only record.

### Personal-data or portfolio disclosure

1. Remove public access immediately without waiting for root-cause analysis.
2. Revoke exposed secrets before attempting file or history cleanup.
3. Determine the smallest affected data categories, time window, locations, caches, forks, artifacts, and recipients.
4. Seek legal or privacy guidance if notification duties may apply.
5. Rebuild public material from the allowlist, repeat automated and human review, and require fresh publication approval.

### Dependency, build-tool, or OCR-asset compromise

1. Freeze dependency changes and deployment.
2. Preserve the lockfile, SBOM, expected checksums, package source, and advisory reference as restricted evidence.
3. Remove or upgrade the affected component through a reviewed change; never bypass an integrity failure.
4. Regenerate the SBOM and third-party inventory, run the full release preflight, and review transitive impact.
5. Restore service only when the affected path is removed, mitigated, or explicitly risk-accepted.

### Service or provider failure

1. Fail closed for calendar mutations and retain user-reviewed drafts only within documented device-local limits.
2. Do not retry uncertain writes blindly; use duplicate detection and deterministic identifiers.
3. Confirm provider recovery using read-only checks before allowing a new mutation.
4. Communicate status without exposing calendar content, account data, or infrastructure identifiers.

## Recovery validation

Before reopening the private pilot:

- the containment action is still effective;
- required credentials and sessions have been revoked or rotated;
- the release preflight passes;
- no critical or high finding remains unresolved without written risk acceptance;
- calendar recovery has explicit owner approval and synthetic or count-only evidence;
- repository, hosting, and calendar access remain least privilege; and
- monitoring and rollback ownership are recorded.

## Monitoring boundary

The separate [privacy-safe monitoring plan](PRIVACY_SAFE_MONITORING_PLAN.md) defines the only approved application-event fields, prohibited content, starting thresholds, retention targets, and activation tests. The plan is a specification, not proof of operating detection. Alerts must remain content-free and route back to this runbook; they must never trigger automatic calendar mutation or recovery.

## Exercises and maintenance

- Use the [synthetic incident tabletop](SYNTHETIC_INCIDENT_TABLETOP.md) as the baseline scenario and corrective-action record; it validates decision logic only, not operating performance.
- Run a sanitized tabletop exercise at least annually and after a material identity or hosting change.
- Test credential revocation, private-access restoration, and repository containment without using live calendar data.
- Review this runbook after incidents, major architecture changes, and changes to applicable notification duties.
- Keep private contact and escalation details outside the public portfolio.

## Readiness statement

This runbook adds response and recovery structure aligned with the project’s NIST-oriented engineering approach. It does not establish NIST compliance, incident-response certification, or proof that these procedures have been exercised. Exercise records and operating evidence remain required.
