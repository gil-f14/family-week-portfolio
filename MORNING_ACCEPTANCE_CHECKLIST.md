# Family Week — Private-Pilot Acceptance Checklist

**Purpose:** A short human verification pass for the current private deployment

**Safety boundary:** Use only the isolated test identity, app-created test calendar, and synthetic event defined in the synthetic end-to-end plan. Do not use household schedules, real names, real locations, or a primary calendar.

This checklist supplements the detailed accessibility and synthetic end-to-end plans. It does not replace independent security testing or establish production, accessibility, NIST, or OWASP conformance.

## Before starting

- [ ] Confirm the site still requires sign-in and is available only to the intended test user.
- [ ] Use a supported current desktop browser first; treat the legacy tablet as an Apple Calendar display fallback only.
- [ ] Confirm the selected writable calendar is the isolated Family Week calendar, never the primary calendar.
- [ ] Open the synthetic end-to-end plan and accessibility test record for the detailed expected results.
- [ ] Stop if the account, calendar, or event details are not clearly synthetic.

## Core calendar path

| ID | Human action | Expected result | Result |
| --- | --- | --- | --- |
| H-01 | Open the private site and reconnect only if requested | The site loads without exposing content before sign-in; an existing valid Google session is recognized | ☐ Pass ☐ Fail |
| H-02 | Open the calendar chooser, select approved readable overlays, then click outside | The chooser stays inside the viewport, scrolls when needed, and closes without changing write access | ☐ Pass ☐ Fail |
| H-03 | Create the single synthetic event from the detailed plan and approve it | Every field is reviewable; duplicates are checked first; exactly one event appears in the app-created calendar | ☐ Pass ☐ Fail |
| H-04 | Submit the same synthetic event again | The app reports the existing match and creates zero additional events | ☐ Pass ☐ Fail |
| H-05 | Refresh the site and reopen the week | The Google session remains usable and exactly one synthetic event is displayed | ☐ Pass ☐ Fail |
| H-06 | Open the synthetic event and begin deletion, then cancel at the first confirmation | The event remains present | ☐ Pass ☐ Fail |
| H-07 | Delete the synthetic event through both confirmations | Only the app-owned synthetic event is removed; other calendars are unchanged | ☐ Pass ☐ Fail |
| H-08 | Refresh the site and the provider calendar | Zero synthetic test events remain | ☐ Pass ☐ Fail |

## Responsive and accessibility path

| ID | Human action | Expected result | Result |
| --- | --- | --- | --- |
| H-09 | Navigate the chooser, quick-add form, event detail, and deletion dialogs with keyboard only | Focus is visible, stays inside open dialogs, Escape closes them, and focus returns to the trigger | ☐ Pass ☐ Fail |
| H-10 | Test at 200% zoom and a narrow phone-sized viewport | No required control is clipped; pop-outs fit the viewport and scroll independently | ☐ Pass ☐ Fail |
| H-11 | Rotate a supported tablet or resize between portrait and landscape | Agenda/week behavior remains understandable and no selection or draft is lost unexpectedly | ☐ Pass ☐ Fail |
| H-12 | Use one available screen reader for the core flow | Dialog names, buttons, full event dates, status updates, and errors are announced meaningfully | ☐ Pass ☐ Fail |

## Immediate stop conditions

Stop testing, disconnect Google, and record only sanitized facts if any of these occur:

- a write targets the primary or an unexpected calendar;
- more than one event is created from one approved submission;
- retry status is uncertain and the duplicate check cannot confirm the outcome;
- deletion can bypass either confirmation or affects a non-app-owned event;
- private information appears before authentication or in an error message; or
- a required control is unreachable by keyboard, touch, zoom, or the selected screen reader.

Do not repeatedly submit, bulk-delete, change access controls, or paste event content into an issue while investigating.

## Evidence record

Record only:

- date, browser/device class, and test IDs;
- Pass, Fail, Blocked, or Not Run;
- count of synthetic events created and removed;
- sanitized defect description without event, account, calendar, address, or deployment identifiers; and
- release decision and approver role.

Do not attach real screenshots, calendar exports, photos, tokens, browser profiles, or console/network dumps to public records.

## Acceptance decision

- [ ] All H-01 through H-12 checks passed, or every Not Run item is explicitly excluded from the supported release scope.
- [ ] Every synthetic event was removed and cleanup was independently confirmed.
- [ ] No critical or high-severity defect remains open.
- [ ] The release decision remains limited to a private pilot unless a separate access and risk review is approved.

**Decision:** ☐ Accept private pilot ☐ Reject ☐ Retest required

**Sanitized notes:**

______________________________________________________________________________
