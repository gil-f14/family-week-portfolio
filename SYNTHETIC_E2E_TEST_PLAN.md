# Family Week — Synthetic Calendar End-to-End Test Plan

**Status:** Approved test design; live execution requires the user in an isolated test-calendar session  
**Purpose:** Verify calendar creation, duplicate prevention, uncertain retry, read-only boundaries, revision conflicts, and two-stage deletion without using household data.

## Safety rules

1. Use only the isolated non-production test identity and its dedicated **Family Week** calendar.
2. Do not enter real names, schedules, schools, teams, addresses, notes, photographs, or subscribed household-calendar data.
3. Confirm the visible write target is **Family Week** before every mutation.
4. Use the synthetic records below exactly, except for selecting a future test date.
5. Stop immediately if the app shows an unexpected identity, write target, calendar set, or real event in the review result.
6. Do not capture credentials, browser storage, authentication URLs, tokens, or unrelated calendar content as evidence.
7. Remove every synthetic event at the end and record the cleanup result.

## Preconditions

- The private application is owner-only and shows the expected isolated test identity as connected.
- The dedicated **Family Week** calendar is present and writable.
- Any calendars selected for display are intentional and contain no data needed for this test.
- The application build and automated test suite are green.
- A future weekday with no synthetic test events is selected.

## Synthetic records

| Record | Subject | Owner | Time | Location | Notes |
| --- | --- | --- | --- | --- | --- |
| A | `E2E-SYNTHETIC-A` | Family | 10:00–11:00 AM | Test Location A | Synthetic test only; safe to delete |
| B | `E2E-SYNTHETIC-B` | Family | 1:00–2:00 PM | Test Location B | Synthetic retry test; safe to delete |

Use a date at least two days in the future. Do not reuse an existing personal or household event title.

## Test sequence

### E2E-01 — Reviewed creation

1. Enter Record A through quick add.
2. Verify subject, owner, date, start, end, location, notes, privacy, and destination before approval.
3. Approve the event once.
4. Confirm exactly one Record A appears in the Family Week app and the dedicated Google calendar.

**Pass:** One correctly bounded event exists only in the approved write calendar.

### E2E-02 — Exact duplicate prevention

1. Submit Record A again with identical fields.
2. Review the duplicate result.
3. Confirm the app reports a duplicate and the calendar still contains exactly one Record A.

**Pass:** No second event is written, and the duplicate result identifies the checked calendar without exposing unrelated event data.

### E2E-03 — Similar-time duplicate prevention

1. Submit the same Record A subject on the same date, shifted fifteen minutes later.
2. Confirm the proposal is treated as a likely duplicate.

**Pass:** No second event is created within the protected same-day time window.

### E2E-04 — Uncertain-result retry

1. Prepare and approve Record B.
2. During submission, use the browser's supported network-offline control to create an uncertain client result; do not close the app or clear local data.
3. Restore connectivity and retry the unchanged reviewed record once.
4. Check both the app and dedicated calendar.

**Pass:** Record B exists exactly once, whether the first request reached the provider or not. If a controlled interruption cannot be produced safely, mark this case **Not executed**, not Passed.

### E2E-05 — Read-only mutation denial

1. Open a synthetic event from a selected read-only overlay calendar, if an approved synthetic overlay is available.
2. Confirm the Family Week delete action is absent or refused.

**Pass:** The app cannot delete an event outside its dedicated write calendar. If no approved synthetic overlay exists, mark **Not executed**.

### E2E-06 — Revision-conflict protection

1. Open Record A's details in Family Week without deleting it.
2. In Google Calendar, change only Record A's synthetic notes.
3. Return to the stale Family Week dialog and attempt the two-stage delete.

**Pass:** The stale delete is refused and the externally changed event remains. Refresh Family Week before continuing.

### E2E-07 — Two-stage deletion and cleanup

1. Refresh the app.
2. Delete Record B, confirming that cancellation is available at both stages.
3. Repeat for Record A after verifying its current details.
4. Confirm neither record remains in the app or dedicated Google calendar.

**Pass:** Both confirmations are required, only app-owned synthetic events are removed, and cleanup leaves zero test records.

## Evidence record

Record text-only results. Do not attach calendar screenshots or exports unless they are cropped, synthetic-only, metadata-reviewed, and separately approved for storage.

| Case | Result: Pass / Fail / Not executed | Date | Browser/device class | Defect or observation |
| --- | --- | --- | --- | --- |
| E2E-01 | Pending | — | — | — |
| E2E-02 | Pending | — | — | — |
| E2E-03 | Pending | — | — | — |
| E2E-04 | Pending | — | — | — |
| E2E-05 | Pending | — | — | — |
| E2E-06 | Pending | — | — | — |
| E2E-07 | Pending | — | — | — |

## Exit criteria

- E2E-01, E2E-02, E2E-03, E2E-06, and E2E-07 pass.
- Optional environment-dependent cases are either passed or explicitly recorded as Not executed with a follow-up owner.
- No event is written outside the dedicated calendar.
- Zero synthetic records remain after cleanup.
- Any failure affecting authorization, data exposure, duplicate safety, or deletion is resolved and retested before broader household use.

Passing this plan supports private-pilot readiness only. It does not establish security certification, WCAG conformance, legal compliance, or public multi-tenant production readiness.
