# Family Week — Privacy-First Photo-to-Calendar Assistant

## Product summary

Family Week turns a photographed or pasted household schedule into reviewed Google Calendar events. It is designed for busy families who need a faster way to translate handwritten schedules without giving up control over dates, times, ownership, or privacy.

This portfolio document uses synthetic descriptions only. It contains no real household names, email addresses, schedules, schools, locations, calendar identifiers, credentials, photographs, or production links.

## The problem

Household schedules often arrive on whiteboards, paper handouts, team messages, and school notices. Re-entering each item is slow, while ordinary OCR can misread handwriting and create incorrect or duplicate calendar events.

## The V1 solution

1. Capture or choose a schedule image, or paste extracted text.
2. Run OCR locally in the browser so the source image is not uploaded by default.
3. Normalize common handwriting and OCR errors with a household dictionary.
4. Present every proposed event for human review and correction.
5. Require explicit dates and unambiguous start/end times.
6. Scan readable calendars for likely duplicates.
7. Add approved events only to an app-created calendar.
8. Display the resulting family week in the application.

## Product and engineering decisions

- **Human approval before automation:** OCR output never goes directly to Google Calendar.
- **Least-privilege calendar access:** the application reads calendars for duplicate checking and writes only to its own calendar.
- **Local-first OCR:** schedule photos remain on the device during the normal workflow.
- **Fail-closed validation:** ambiguous times, missing fields, expired authorization, and failed duplicate scans block calendar writes.
- **Retry safety:** stable event identifiers and duplicate checks make uncertain network retries safer.
- **Household learning without cloud AI:** reviewed corrections improve a device-local dictionary without sending schedules to a language model.
- **Accessible review:** side-by-side source comparison, clear ownership colors, and explicit warnings support careful correction.

## Security and privacy posture

- OAuth credentials and session secrets are supplied at runtime, never hardcoded.
- Browser storage is limited to device-local drafts and dictionary preferences; Google bearer tokens are not stored there.
- Operational logs exclude event titles, notes, addresses, photographs, and credentials.
- Calendar writes are restricted to the application-created calendar.
- Photos are not permanently stored by default.
- Public portfolio artifacts use synthetic data and pass a separate release gate before publication.

The project follows NIST-aligned risk-management practices, but it has not undergone a formal NIST assessment or certification.

## Evidence of quality

- 65 automated tests covering calendar rules, duplicate behavior, retry handling, OCR correction, draft recovery, validation, accessibility source guards, and rendered safety messages.
- Production build verification before private deployment.
- End-to-end validation against a disposable Google Calendar event.
- Owner-only deployment with explicit account access.
- A separate clean-export release gate for any public portfolio material.

## My role

I defined the product workflow, requirements, privacy boundaries, OAuth model, duplicate-handling behavior, review safeguards, acceptance criteria, and release testing. I used AI-assisted development tools to accelerate implementation, then reviewed, tested, and validated the resulting product decisions and behavior.

## V2 delivered

- Responsive week and agenda views with a tablet-focused display mode.
- Touch-friendly manual event entry and a visible one-hour duration default.
- Two-stage deletion limited to application-owned events.
- Mobile photo review and device-local OCR correction learning.
- Consent-based location-aware game-time weather with data minimization.
- Read-only calendar overlays, duplicate checks, full-day scrolling, and reviewable owner colors.
- Accessibility hardening for dialogs, keyboard focus, status messages, mobile pop-outs, and spoken event-date context.

Manual supported-device and accessibility verification remain before any broad production-readiness or conformance claim.

## V3 direction

- Automatic event-time weather presentation with freshness labeling.
- Place-name and address autocomplete through an approved provider.
- Advanced shared-device access and recovery.
- Optional preference synchronization after privacy review.

## Technology

TypeScript, React, Next.js-compatible application routing, Cloudflare Worker-compatible deployment, Google Calendar API, browser-based PaddleOCR/ONNX processing, and Node.js automated tests.
