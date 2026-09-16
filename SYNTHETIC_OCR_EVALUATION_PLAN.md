# Family Week — Synthetic OCR Evaluation Plan

**Status:** Evaluation design prepared; representative benchmark execution remains pending
**Scope:** On-device handwriting recognition, correction, parsing readiness, and human-review safety
**Claim boundary:** This plan is not model certification, an accuracy claim, a bias assessment, an AI RMF assessment, or evidence that real household handwriting has been validated.

## Privacy-safe dataset rule

Create an independently invented benchmark containing no real household names, initials, schedules, schools, teams, addresses, birthdays, appointments, photographs, calendar exports, or OCR corrections. Use synthetic names such as Parent A, Parent B, Child A, Child B, Family, and Unassigned. Use fictional activities, non-routable locations, and dates that are not copied from a live calendar.

Store only approved synthetic images, their ground-truth text, case metadata, and results. Do not derive examples from production photos, browser storage, support conversations, screenshots, clipboard history, or calendar content.

## Dataset matrix

The first benchmark target is at least forty independently created images, balanced across these conditions:

| Dimension | Required coverage |
| --- | --- |
| Layout | Single day, multi-day columns, uneven spacing, crossed-out item, annotation, and blank day |
| Writing | Print, mixed case, joined handwriting, narrow spacing, large spacing, and multiple writers |
| Capture | Straight, mild rotation, perspective, shadow, glare, low contrast, and background clutter |
| Ink | Dark, light, red, blue, green, and mixed colors |
| Content | Names, activity words, dates, single times, ranges, AM/PM, locations, and all-day notes |
| Safety edge | Ambiguous digit, missing meridiem, overwritten time, unreadable word, duplicate item, and conflicting day heading |

Every case receives a stable synthetic ID and records only its declared conditions. Do not encode a person, device, creator, or household identifier in the ID.

## Ground truth

Two reviewers independently transcribe each synthetic image. Resolve disagreements before testing and retain the final text plus structured expected fields: day, subject, start time, end time when present, all-day status, location when present, and whether parsing must be blocked for human correction.

Ground truth preserves intended spelling and punctuation but does not silently infer information absent from the image. A missing end time remains missing so the separate one-hour product default can be evaluated explicitly.

## Measures

| Measure | Definition | Safety interpretation |
| --- | --- | --- |
| Character error rate | Insertions, deletions, and substitutions divided by ground-truth characters | Diagnostic only; low character error does not prove event safety |
| Word accuracy | Exact normalized word matches divided by ground-truth words | Tracks spelling and family-dictionary effects |
| Day and field accuracy | Exact match for day, subject, start, end, all-day, and location fields | Primary workflow measure |
| Unsafe-pass rate | Cases marked ambiguous or unreadable that the product allows to parse without correction | Must be zero for release eligibility |
| False-block rate | Clear cases unnecessarily blocked for correction | Usability measure; does not override unsafe-pass priority |
| Review correction load | Number of words or fields changed before approval | Estimates user effort without using real users or schedules |
| Duplicate outcome accuracy | Correctly identifies a synthetic duplicate or distinct event | Must not mutate a calendar during benchmark execution |

## Initial engineering thresholds

- Unsafe-pass rate: **0%** across the benchmark.
- Exact day and start-time accuracy: **at least 95%** for clear cases.
- Exact end-time accuracy: **at least 90%** when an end time is visibly present.
- All-day classification: **100%** for explicit all-day cases.
- No regression larger than two percentage points in word accuracy or structured-field accuracy from the approved baseline.
- Every failure involving a day, time, all-day state, or blocked/allowed decision is release-blocking until reviewed and either remediated or explicitly excluded with a documented reason.

These are internal starting thresholds, not service levels or public accuracy claims. Increase dataset size and diversity before broader use.

## Execution procedure

1. Record application version, OCR asset hashes, browser version, device class, and benchmark manifest hash without account or device identifiers.
2. Clear the device-local family dictionary so the baseline measures raw recognition and built-in normalization.
3. Run every image without calendar authentication and export only synthetic results.
4. Repeat with an approved synthetic dictionary to measure correction benefit and harmful substitutions.
5. Compare extracted text and structured fields to ground truth using deterministic normalization.
6. Manually review every unsafe-pass, day/time error, and large correction delta.
7. Rerun affected cases plus the full benchmark after OCR model, preprocessing, parser, dictionary, browser, or image-bound changes.

## Bias and accessibility review boundary

The benchmark should vary writing styles, contrast, color, layout, and capture conditions, but forty synthetic images cannot establish demographic fairness or accessibility. Do not infer protected characteristics or label reviewers by sensitive traits. A qualified review must determine whether broader participatory testing is appropriate and how to obtain consent without collecting unnecessary personal data.

## Evidence and release rule

Retain the synthetic manifest, ground truth, aggregate measures, fixed failure categories, application version, OCR hashes, reviewer roles, and corrective-action references. Keep source images private until they pass the portfolio release gate; publish only independently reviewed synthetic examples.

The benchmark may support an engineering release decision only after every case is executed, unsafe-pass results are zero, blocking failures are resolved, and an independent reviewer confirms the dataset and method. Until then, representative OCR evaluation remains an open production-readiness item.
