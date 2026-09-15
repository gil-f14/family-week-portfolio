# Family Week — Privacy Notice Draft

**Status:** Engineering draft for independent privacy and legal review before broader access  
**Scope:** Private-pilot website and its device-local calendar workflow

This notice describes the current product design. It is not a legal opinion, certification, or claim of compliance with any privacy law or NIST framework.

## What Family Week does

Family Week helps an authorized user turn a schedule photo or pasted text into proposed calendar events. The user reviews and approves every event before it is added to the dedicated Family Week calendar. The app may also display selected calendars as read-only overlays and can request weather for an event when the user chooses that action.

## Information processed on this device

- Schedule photos are held in browser memory for preview and on-device OCR. The application does not upload them.
- Extracted text, event-review drafts, learned corrections, display choices, and color rules are stored only in this browser.
- Inactive OCR and event-review drafts expire automatically after seven days. Approval, **Clear draft**, or **Clear this device** can remove them sooner.
- Learned corrections and display preferences remain until the user removes or clears them. They do not silently synchronize to another device.

## Information sent to service providers

- Google receives the Calendar API requests needed to show approved calendars, check for duplicates, and create or delete eligible events in the dedicated application calendar.
- When the user selects **Check weather**, the minimum event location and time needed for the request are sent to approved U.S. geocoding and weather services.
- Family Week does not intentionally include photos, OCR text, event details, locations, credentials, or account identifiers in application monitoring.

Service providers process information under their own terms, settings, and retention practices. Provider-held calendar data is controlled through the connected calendar account.

## User choices and controls

- Review, edit, or reject proposed events before writing them.
- Choose which readable calendars appear as overlays.
- Decline weather lookup or omit a location.
- Use **Clear draft** to remove the current local review draft.
- Use **Clear this device** to remove Family Week drafts, learned corrections, photo preview, display choices, and color rules from this browser. This does not delete Google Calendar events, disconnect Google, or clear unrelated browser data.
- Use **Disconnect Google** to end the Family Week session. This does not delete provider-held calendar events.
- Delete only eligible application-calendar events through the two-confirmation deletion flow or use the calendar provider's controls.

## Shared-device and security limits

Anyone with access to an unlocked device and browser profile may be able to see locally stored Family Week information. Use **Clear this device**, lock the device, and use a separate browser profile before another person uses it. Family Week remains a private pilot and should not be used on an untrusted or unsupported device.

## Questions and security reports

Private-pilot users should contact the application owner through the private support channel supplied with their access. Do not include schedule photos, calendar contents, credentials, authentication codes, or other sensitive household information in a report. Security reporting expectations are described in [Security policy](SECURITY.md).

## Review and changes

This draft must be independently reviewed and approved before broader access. Reassess it whenever identity, providers, telemetry, synchronization, supported devices, data retention, or public distribution changes. The detailed engineering record is in the [data retention and disposal schedule](DATA_RETENTION_SCHEDULE.md) and [privacy impact assessment](PRIVACY_IMPACT_ASSESSMENT.md).
