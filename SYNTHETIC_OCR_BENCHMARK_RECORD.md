# Family Week — Synthetic OCR Benchmark Record Template

**Status:** Blank execution record; no benchmark run or accuracy result is represented here  
**Use:** One record per evaluated application and OCR-asset version  
**Claim boundary:** Completing this record does not establish model certification, demographic fairness, accessibility conformance, NIST AI RMF conformance, or fitness for broader production use.

## Privacy boundary

Use only the approved synthetic benchmark. Do not enter names, initials, email addresses, account identifiers, device identifiers, schools, teams, real locations, calendar text, support text, screenshots, production images, or excerpts of recognized handwriting.

Record only fixed references, hashes, numeric aggregate measures, coded failure categories, role labels, dates, and issue references that contain no household data. Keep synthetic source images private until they independently pass the public-release gate.

## Execution identity

| Field | Required value |
| --- | --- |
| Benchmark reference | Fixed manifest reference |
| Benchmark manifest SHA-256 | Lowercase 64-character digest |
| Application reference | Bounded release or commit reference |
| OCR asset hashes | Four hashes from the pinned private asset manifest |
| Result-set SHA-256 | Lowercase 64-character digest |
| Execution date | UTC date only |
| Browser family/version | Supported browser name and major version; no profile or device ID |
| Device class | `desktop`, `tablet`, or `phone` only |
| Dictionary mode | `empty` or `approved_synthetic` only |
| Executor role | `reviewer_a` or `reviewer_b` only |

## Dataset verification

Mark each item `pass` or `fail`. Any failure blocks scoring and change approval.

| Check | Status |
| --- | --- |
| Exactly one result exists for every manifest case | Pending |
| Case identifiers are unique and match the manifest | Pending |
| Benchmark, application, and OCR hash references match | Pending |
| Forty or more cases and every required condition are present | Pending |
| No prohibited identity or household field is present | Pending |
| Every ambiguous time or unreadable case requires correction | Pending |
| Two role-only reviewers approved ground truth | Pending |

## Aggregate measures

Copy only the evaluator's numeric output. Do not calculate or alter results manually.

| Measure | Result | Engineering threshold | Decision |
| --- | ---: | ---: | --- |
| Case count | Pending | At least 40 | Pending |
| Character error rate | Pending | Diagnostic; baseline increase must not exceed 2 percentage points | Pending |
| Word accuracy | Pending | Baseline decrease must not exceed 2 percentage points | Pending |
| Structured-field accuracy | Pending | Baseline decrease must not exceed 2 percentage points | Pending |
| Day accuracy for clear cases | Pending | At least 95% | Pending |
| Start-time accuracy for clear timed cases | Pending | At least 95% | Pending |
| End-time accuracy when present | Pending | At least 90% | Pending |
| Explicit all-day accuracy | Pending | 100% | Pending |
| Duplicate-outcome accuracy | Pending | Baseline decrease must not exceed 2 percentage points | Pending |
| Unsafe-pass rate | Pending | 0% | Pending |
| Average corrections per case | Pending | Diagnostic | Pending |

## Failure register

Record one row per blocking or reviewed failure. Use only these categories: `unsafe_pass`, `day_error`, `start_time_error`, `end_time_error`, `all_day_error`, `subject_error`, `location_error`, `duplicate_error`, `harmful_dictionary_substitution`, `manifest_mismatch`, or `scoring_error`.

| Synthetic case ID | Failure category | Severity | Issue reference | Retest status |
| --- | --- | --- | --- | --- |
| Pending | Pending | `block` or `review` | Bounded issue reference | Pending |

Do not describe the source text, recognized text, person, activity, or location in this register.

## Change decision

| Gate | Decision |
| --- | --- |
| Manifest validation | Pending |
| Aggregate thresholds | Pending |
| Regression comparison against approved baseline | Pending |
| Every blocking failure resolved and retested | Pending |
| Independent method and evidence review | Pending |
| Final decision | `blocked` until every gate passes |

## Approval boundary

The executor records results but cannot independently approve the same run. A second reviewer verifies the manifest and result hashes, threshold output, failure classification, retest evidence, and claim wording. Use role labels only; retain reviewer identity and any required approval evidence in an access-controlled system outside this public-safe record.

Until the manifest is executed against synthetic images and every gate is independently reviewed, leave this record in `Pending` state and continue to describe OCR evaluation as designed but not completed.
