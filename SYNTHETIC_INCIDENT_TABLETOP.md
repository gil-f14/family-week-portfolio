# Family Week — Synthetic Incident Tabletop Record

**Exercise date:** September 3, 2026  
**Exercise type:** Documentation-based engineering dry run using synthetic facts only  
**Scope:** Private-site access expansion, suspected credential exposure, containment, recovery, and communication  
**Claim boundary:** No live account, credential, calendar, deployment, or external alert route was used. This record is not proof of operational response performance, a penetration test, an audit, or certification.

## Scenario

A routine privacy-safe access check reports that the private Family Week site may no longer be owner-only. At the same time, a synthetic release artifact is reported as possibly containing a session-sealing value. There is no confirmed calendar mutation and no household content is supplied to the exercise team.

The scenario intentionally combines potential unauthorized access with potential credential exposure so the team must prioritize containment without copying sensitive evidence or changing calendar records.

## Objectives

1. Classify the event and select accountable decision roles.
2. Stop additional exposure before investigating root cause.
3. Sequence credential containment before repository-history cleanup.
4. Preserve only the minimum sanitized evidence needed for decisions.
5. Prevent automatic or unapproved calendar recovery actions.
6. Define safe validation and approval conditions for restoring the private pilot.

## Exercise injects and decisions

| Inject | Decision | Expected control behavior | Result |
| --- | --- | --- | --- |
| Access check returns a non-owner-only state | Treat as critical and remove or disable broader access before investigation | Keep the application and source private; do not wait for impact confirmation | Passed in documented decision flow |
| A release artifact may contain a credential | Revoke or rotate the affected value before rewriting history or republishing | Invalidate affected sessions and stop deployments | Passed in documented decision flow |
| A responder requests raw logs in a shared ticket | Refuse; record only rounded time, release reference, fixed reason, severity, containment state, and restricted evidence location | Never copy photos, calendar content, tokens, account identifiers, or request payloads | Passed in documented decision flow |
| Calendar changes cannot be ruled out | Disconnect or disable the mutation path; perform read-only comparison before proposing recovery | Never run bulk deletion or restoration automatically | Passed in documented decision flow |
| The source scan is clean after containment | Do not restore service yet | Require access validation, successful release gate, no unresolved critical/high finding, and owner approval | Passed in documented decision flow |
| A responder wants to disclose the event publicly immediately | Escalate notification analysis to authorized privacy/legal review | Avoid both concealment and unsupported disclosure; preserve a decision record | Passed in documented decision flow |

## Sanitized decision record

- **Initial severity:** Critical because unauthorized access and credential exposure were both plausible.
- **First containment:** Restore owner-only access or disable the service, then revoke or rotate the suspected value.
- **Evidence boundary:** Counts, fixed reason codes, rounded time, release reference, decisions, and restricted evidence location only.
- **Calendar boundary:** No event creation, deletion, restoration, or modification without explicit calendar-owner approval.
- **Recovery gate:** Known-good private version, verified access policy, invalidated affected sessions, successful automated release gate, resolved critical/high findings, and recorded approval.
- **Communication boundary:** Private need-to-know routing; notification obligations require authorized privacy/legal judgment.

## What the exercise demonstrated

- The runbook gives a clear privacy-first containment sequence.
- Credential revocation or rotation precedes history cleanup.
- The monitoring specification can signal the issue without household content.
- Calendar recovery remains separate from service recovery and requires human approval.
- The release gate and owner-only access check provide concrete reopening conditions.
- Public portfolio material can describe the exercise without exposing operational identifiers.

## Gaps and corrective actions

| Gap | Risk | Corrective action | Exit evidence |
| --- | --- | --- | --- |
| Alert routing is specified but not operating | A real access change may not reach the owner promptly | Implement and test the content-free monitoring plan | Synthetic threshold and private-route test |
| Actual access containment and credential rotation were not exercised | Procedures may fail under real permissions or provider constraints | Run an authorized non-production operational drill | Timed, sanitized drill record |
| Private incident contacts and alternates are not recorded in this public-safe package | Escalation could stall | Maintain a restricted contact and decision-role sheet | Owner review without publishing identities |
| Recovery time and recovery point objectives are not approved | Reopening decisions may be inconsistent | Approve private-pilot recovery objectives | Dated owner decision |
| Notification decision process has not received legal/privacy review | Required communication could be delayed or incorrect | Obtain qualified review before broader access | Approved decision guide |

## Exercise conclusion

The documentation-based engineering tabletop completed its decision objectives without using sensitive or live data. It provides limited evidence that the planned sequence is coherent; it does not demonstrate that access-control changes, credential rotation, alert delivery, or recovery can be completed within a target time. An authorized operational drill and independent review remain required before broader access.

## NIST-aligned outcome mapping

The exercise provides preliminary evidence for Respond and Recover outcomes in the project's NIST CSF 2.0 engineering profile and reinforces the Privacy Framework emphasis on minimizing data during incident handling. The result remains partial and self-assessed; no compliance, audit, or certification claim is made.
