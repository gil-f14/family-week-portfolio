# Family Week — Data Retention and Disposal Schedule

**Status:** Engineering draft for the private pilot; owner, privacy, and legal approval remain required  
**Assessment date:** September 2026  
**Scope:** Application-controlled data, device-local data, provider-held calendar data, external forecast requests, engineering evidence, and public portfolio material

This schedule documents current behavior separately from proposed targets. It is not a legal opinion, contract, certification, or claim that every provider-controlled copy follows these targets.

## Retention principles

- Keep the minimum data needed for the stated purpose and no longer.
- Do not retain photos, OCR text, calendar content, locations, credentials, or account identifiers in application telemetry.
- Give users clear disposal controls without silently deleting Google Calendar events.
- Treat browser clearing, Google disconnection, and calendar-event deletion as separate actions.
- Preserve only sanitized evidence in the public portfolio.
- Reassess retention whenever identity, analytics, synchronization, providers, logging, or distribution changes.

## Current behavior and proposed target

| Data category | Current behavior | Proposed private-pilot target | Disposal method | Approval or implementation gap |
| --- | --- | --- | --- | --- |
| Uploaded schedule photo and preview | Held in browser memory; not uploaded by the application | Keep only for the active page session or until replaced or cleared | Replace the photo, use **Clear this device**, or close the page | Verify disposal behavior on supported devices |
| OCR text and event-review draft | Bounded device-local storage expires after 7 days of inactivity, or sooner after approval or manual clearing | Keep the implemented 7-day maximum while preserving immediate manual clearing | Automatic expiry, **Clear draft**, or **Clear this device** | Verify expiry and disposal behavior on supported devices |
| Learned Family Dictionary corrections | Device-local until individually removed or device clearing | Retain until the user removes or clears them; no silent cloud synchronization | Forget one entry or use **Clear this device** | Validate shared-device guidance and reset behavior |
| Calendar selections, display mode, and color rules | Device-local until changed or device clearing | Retain until changed or cleared because these are user preferences | Change settings or use **Clear this device** | Verify reset on supported browsers |
| Google authorization session | Sealed secure cookie expires after 30 days; can end earlier through disconnect, invalidation, or provider revocation | Keep the existing 30-day maximum during the private pilot and reassess before shared access | Disconnect in Family Week, wait for expiry, or revoke at the provider | Test disconnect and provider revocation; independently review session policy |
| OAuth state and verifier | Secure cookies expire after 10 minutes or are removed after callback | Keep the current 10-minute maximum | Automatic expiry or callback cleanup | Confirm provider/browser behavior during authorized testing |
| Calendar events | Stored by Google Calendar according to the user's provider settings | No automatic retention or deletion by Family Week | Two-stage deletion only for eligible application-calendar events, or provider controls | Provider policy and user decisions govern remaining copies |
| Calendar data read for week view and duplicate checks | Used for the active response; no application database is used | Do not intentionally persist in application storage or telemetry | Response ends; browser state is replaced on refresh or page close | Verify platform logs do not capture bodies or query content |
| User-requested weather response | Held in active browser component state; location/time sent only on request | Keep only for the active page session; do not add server-side history | Refresh or close the page | External providers have their own policies; reassess before automatic weather |
| Content-free operational events | Monitoring is specified but not implemented | 14 days for allowlisted raw events; 90 days for non-identifying aggregates | Automated retention deletion with restricted evidence | Approve schema, platform behavior, retention, and access before activation |
| Restricted incident evidence | No centralized operating store is approved | Retain only as long as required by an approved incident, legal, and security process | Authorized case closure and verified deletion | Approve policy, roles, and legal obligations before use |
| Private SBOM, test, release, and security evidence | Retained in the private engineering repository | Retain for the supported life of the release plus an approved assurance period | Reviewed repository archival or deletion | Define the assurance period and repository archival owner |
| Sanitized public portfolio documents | Retained in the public portfolio history | Retain while the portfolio is intentionally published | Remove public access and rebuild clean history if sensitive data is discovered | Re-run the public gate before every update |

## User-facing disposal boundaries

- **Clear draft** removes only the current local OCR/review draft and preview state.
- **Clear this device** removes the local draft, learned dictionary, photo preview, calendar-display selections, view preferences, and color rules from that browser.
- **Disconnect Google** ends the Family Week session but does not delete provider-held calendar events.
- **Delete event** requires two confirmations and applies only to eligible events in the dedicated application calendar.
- Provider revocation can invalidate authorization outside Family Week; provider settings govern calendar retention and provider-controlled copies.
- None of these controls broadly clears unrelated browser storage.

## Disposal verification

Before approving this schedule:

1. Test each local clearing control on every supported browser and device.
2. Verify the automated 7-day inactive-draft expiry on every supported browser and device.
3. Test Google disconnect, session expiry, and provider revocation without retaining account or calendar content in evidence.
4. Confirm hosting and provider-default logs do not capture prohibited fields; document unavoidable metadata, access, and deletion behavior.
5. Test monitoring retention deletion with synthetic fixed-code events before enabling monitoring.
6. Record only dates, counts, result codes, reviewer roles, and restricted evidence locations in the approval record.

## Ownership and review cadence

- The product owner approves purpose and user experience.
- The privacy reviewer approves minimization, notice, retention, and disposal outcomes.
- The security reviewer validates access restrictions, evidence handling, and deletion tests.
- Legal review determines applicable obligations before broader or commercial use.
- Review at least annually and after any material change to identity, providers, data flows, telemetry, synchronization, supported devices, or public distribution.

## NIST-aligned outcome mapping

This draft supports the project's NIST Privacy Framework engineering profile through purpose limitation, data minimization, individual control, disposal, and governance. Approval of remaining targets, operating evidence, and independent review remain incomplete; no NIST compliance or certification is claimed.
