# Family Week — Privacy Impact Assessment

**Status:** Engineering assessment for a private pilot; independent privacy and legal review not completed  
**Review trigger:** Before broader access, a new identity model, analytics, preference synchronization, or a new external data provider

## Purpose and scope

Family Week helps an authorized household user turn a photographed or pasted schedule into reviewed calendar events. This assessment covers the private web application, its dedicated calendar, optional readable-calendar overlays, device-local OCR and preferences, and user-initiated weather lookup. It uses synthetic descriptions and contains no household, account, deployment, or credential data.

This document is an engineering control record, not a legal determination or claim of NIST Privacy Framework compliance.

## Data inventory and lifecycle

| Data category | Purpose | Processing location and recipient | Retention and disposal | User control |
| --- | --- | --- | --- | --- |
| Schedule photo | Extract proposed events | Browser memory only; self-hosted OCR assets run on the device | Not uploaded by the application; preview ends when replaced, cleared, or the page closes | Replace the photo or use **Clear this device** |
| OCR text and event draft | Human review before calendar creation | Device-local browser storage | Bounded draft persists until approval, draft clearing, or device clearing | Edit, clear draft, or clear device |
| Learned corrections | Improve recurring household OCR terms | Device-local browser storage | Persists until individual removal or device clearing; optional user-created backup | Review before learning, remove, export, import, or clear device |
| Display preferences | Remember view, selected readable calendars, and color rules | Device-local browser storage | Persists until changed or device clearing | Change preferences or clear device |
| Google authorization | Read permitted calendars and write only to the dedicated application calendar | Sealed, secure, HTTP-only session cookie; Google receives normal Calendar API requests | Session-limited; invalid or expired state is rejected | Disconnect Google or revoke provider access |
| Calendar metadata and events | Show a week, detect duplicates, and create or delete approved application-owned events | Application worker and Google Calendar | Governed by the connected account and calendar settings | Select readable overlays; review writes; delete only eligible application-owned events |
| Event location and time | Return an optional forecast | Sent only after a user request to approved U.S. geocoding and weather services | Not intentionally retained by Family Week beyond the active response | Do not request weather or omit a location |
| Security and build evidence | Support release integrity without household content | Private engineering systems and sanitized portfolio records | Retained according to project operations policy | Maintainer review and repository controls |

## Data minimization decisions

- Raw photos are processed on-device and are not application uploads.
- A cloud language model is not used for OCR correction; learned terms remain local.
- Calendar writes target only the dedicated application calendar.
- Readable overlays are bounded and do not expose delete controls.
- Weather is user-initiated and receives only the location and event time needed for the request.
- Public documentation excludes production URLs, identities, schedules, screenshots with personal content, credentials, and cloud identifiers.
- The device reset removes only enumerated Family Week keys; it does not broadly clear unrelated browser storage.

## Privacy risks and treatments

| Risk to people | Current treatment | Residual risk and required follow-up |
| --- | --- | --- |
| Another person sees a draft or learned term on an unlocked shared device | Bounded local storage and a two-step **Clear this device** control | The user must run the control; verify it on every supported device and document shared-device guidance |
| An uncertain OCR result becomes a real event | Confidence gate, visible uncertainty, editable review, and explicit approval | Complete the approved synthetic end-to-end test and monitor false-ready results without retaining event content |
| More calendar data is read or changed than intended | Least-privilege scopes, bounded overlays, server-side target restrictions, duplicate checks, and protected deletion | Independently review OAuth configuration and test disconnect, revocation, and confused-deputy cases |
| Location is disclosed to an external service unexpectedly | Forecast lookup is explicit, labeled, and restricted to approved official hosts | Add a provider-retention reassessment before automatic weather or place autocomplete |
| Operational records leak household details | No-sensitive-logging rule, sanitized evidence, automated public-release gate | Add content-free logging tests and approve retention/access rules before operational telemetry |
| A public portfolio reveals an identity or system detail | Separate documentation-only repository, synthetic language, history scans, and manual release gate | Repeat human contextual review before every public media or document update |

## Notice and choice

The product currently explains that photos and pasted text are processed in the browser, requires review before a write, labels read-only calendars, explains the weather disclosure at the point of use, and distinguishes device clearing from calendar deletion and Google disconnection. Before broader access, an independently reviewed concise privacy notice must explain processing purposes, storage, recipients, retention, user choices, support, and the limits of shared-device protection.

## Access, retention, and deletion rules

- Hosting remains owner-only during the private pilot unless an explicit access review approves a change.
- Device-local data has no silent cross-device synchronization.
- **Clear this device** removes the local draft, dictionary, photo preview, display selections, view preferences, and color rules. It does not delete Google Calendar events or disconnect Google.
- Calendar deletion requires two confirmations and is limited to eligible events in the dedicated application calendar.
- Operational evidence must not contain event titles, notes, locations, photos, calendar contents, credentials, or account identifiers.
- Provider-held calendar data and authorization are subject to the connected provider's controls; the user can also revoke access there.

## Approval conditions before broader access

- Complete supported-device reset, keyboard, screen-reader, zoom/reflow, and orientation tests.
- Complete the synthetic create, duplicate, interruption, revision-conflict, delete, and cleanup sequence.
- Review OAuth scopes and test disconnect and provider revocation.
- Approve a privacy notice, retention schedule, operational logging schema, incident process, and provider reassessment cadence.
- Obtain independent privacy and security review; seek legal review before making regulatory or compliance claims.

## NIST-aligned outcome mapping

This assessment supports the project's NIST Privacy Framework engineering profile through data processing inventory, governance boundaries, individual control, clear communication requirements, and protective safeguards. Alignment is partial and evidence-based; neither this assessment nor the product has been certified by NIST.
