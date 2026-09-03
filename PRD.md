# Family Week — Product Requirements Document

**Document status:** Portfolio edition 1.0  
**Product stage:** Private pilot; V1 complete, V2 core complete, V3 planned  
**Audience:** Product, program, design, engineering, security, and prospective employers

## Executive summary

Family Week is a privacy-first assistant that converts a photographed or pasted household schedule into reviewed Google Calendar events. The product reduces repetitive entry without allowing uncertain handwriting recognition to write directly to a calendar. It combines on-device OCR, human review, time validation, cross-calendar duplicate detection, least-privilege calendar access, and a responsive weekly display.

This portfolio PRD uses synthetic language only. It intentionally excludes real household data, account information, production URLs, credentials, cloud identifiers, and private operational details.

## Problem

Family schedules arrive through whiteboards, paper handouts, school notices, team messages, and ad hoc conversations. Re-entering them is slow and error-prone. Generic OCR is especially unreliable for handwriting, while a wrong time or duplicate event can be more damaging than no automation at all.

## Product principles

1. **Human approval before automation.** Recognition output is always a proposal.
2. **Fail closed.** Ambiguous or invalid events cannot be written.
3. **Least privilege.** Read access supports duplicate checking; writes and deletes are limited to the app-created calendar.
4. **Local first.** Photos, drafts, and learned corrections stay on the device in the normal workflow.
5. **Explain uncertainty.** Inferred times, low-confidence text, duplicates, and failures are visible.
6. **Touch and keyboard parity.** Core actions must work on supported desktop, phone, and tablet browsers.
7. **No silent destructive actions.** Deletion requires contextual, staged confirmation.

## Primary users and jobs

### Household coordinator

- Capture a weekly schedule quickly.
- Correct recognition mistakes beside the source image.
- Prevent duplicate entries across readable calendars.
- Add only reviewed events to the shared family calendar.

### Shared-display user

- See the current week or agenda with minimal interaction.
- Identify ownership using text and consistent colors.
- Add an ad hoc event using touch.

### Product owner / operator

- Keep calendar permissions narrow.
- Recover from expired authorization or interrupted writes.
- Validate releases without exposing household data.

## V1 — Complete private pilot

### Functional requirements

- Accept a supported image or pasted text.
- Run OCR in the browser with bounded file size and image dimensions.
- Keep the source image available for side-by-side review.
- Normalize recurring OCR errors with a device-local correction dictionary.
- Require owner, date, title, and valid time information before submission.
- Require explicit review before every calendar write.
- Search readable calendars for likely duplicates before writing.
- Write only to the app-created Family Week calendar.
- Use deterministic event identifiers and safe retry behavior.
- Maintain a durable encrypted Google session across deployments.

### V1 acceptance evidence

- Production build and automated suite pass.
- Calendar scope and write-boundary behavior are covered by source-guard tests.
- Duplicate, validation, retry, session, OCR, and local-draft behavior are tested.
- A disposable event has been created and removed in a private test calendar.

## V2 — Core complete; verification remains

### Functional requirements

- Responsive week and agenda views.
- Calendar selection for approved read-only overlays.
- Manual quick-add with a visible one-hour default duration.
- Exact recognized times remain editable and are not rounded silently.
- Safe two-stage deletion for application-owned events only.
- Subject-based owner colors plus review for unmatched titles.
- Consent-based weather lookup for supported events with locations.
- Tablet-focused display mode and device-local view preferences.
- Calendar chooser contained within the mobile viewport and dismissible outside.
- Scrollable day range through midnight with a sticky all-day row.
- Two-step **Clear this device** control removes local drafts, learned corrections, calendar-display choices, color rules, and the current photo preview without deleting Google Calendar events or ending the Google connection.

### Accessibility requirements

- Target WCAG 2.2 Level AA across supported responsive layouts.
- Provide semantic names, roles, states, status messages, and full date context.
- Trap focus in modal surfaces, support Escape, and return focus to the trigger.
- Preserve visible focus, keyboard operation, zoom/reflow, and touch target usability.
- Never use color as the sole indicator of owner, warning, duplicate, or status.

### Remaining V2 acceptance work

- Manual keyboard-only walkthrough on every core flow.
- VoiceOver testing on a supported iPhone/iPad and screen-reader testing on desktop.
- 200% and 400% zoom/reflow testing, contrast verification, and orientation testing.
- Approved end-to-end create, duplicate, edit-review, and delete test.
- Confirmation of the intended readable-calendar set.
- Manual verification of the clear-device flow on each supported browser and device.

## V3 — Planned

- Automatic forecast presentation when viewing an eligible event or week.
- Place-name and address autocomplete through an approved location provider.
- Forecast freshness, availability, and source labeling.
- Advanced shared-device access without exposing a primary personal calendar.
- Optional synchronized preferences after privacy and account-model review.
- Improved supported-tablet installation and display behavior.

## Data and integration boundaries

| Data | Normal location | Retention intent |
| --- | --- | --- |
| Source photo | Browser memory | Not retained by the service |
| Extracted text and draft | Device-local browser storage | User-controlled, bounded local state |
| Learned corrections | Device-local browser storage | User-controlled; no cloud model training |
| Google authorization | Encrypted, secure session cookie | Session lifetime; invalid data is rejected |
| Calendar event | Google Calendar | Governed by the user's calendar settings |
| Weather request | Approved weather provider | Minimum event time and location needed for response |

## Success measures

- Median time to turn a weekly schedule into reviewed events.
- Percentage of proposed events requiring manual text correction.
- Percentage of writes safely skipped as duplicates.
- Rate of invalid or ambiguous events blocked before write.
- Successful completion rate by device class.
- Accessibility defects by severity and release.
- Calendar write/delete incidents involving the wrong calendar: target zero.

## Out of scope for the current release

- Automatic writes from raw OCR.
- Writing to arbitrary calendars.
- Deleting from read-only or non-application calendars.
- Public multi-tenant service operation.
- Legacy-browser support that requires weakening authentication or security controls.
- Formal legal, NIST, Section 508, or WCAG certification claims.

## Release definition

A release is eligible for private deployment only when the production build and automated tests pass, owner-only access is confirmed, and no unapproved live calendar mutation is performed. A public portfolio release follows the separate clean-export gate and never exposes the private working repository.
