# Family Week — Accessibility Test Record

**Assessment date:** September 2026  
**Target:** WCAG 2.2 Level AA  
**Current decision:** Automated engineering baseline passed; conformance is not claimed because required human and supported-device testing remains incomplete.

## Scope

The record covers the photo inbox, OCR comparison dialog, event review queues, quick-add form, calendar chooser, week and agenda views, event-details and deletion dialogs, and tablet display mode. It uses synthetic test content and contains no household or account information.

## Completed automated evidence

| Area | Result | Evidence and boundary |
| --- | --- | --- |
| Static accessibility lint | Passed with zero errors | JSX accessibility rules run across the application; image-component performance advisories are not accessibility failures |
| Keyboard dialog structure | Passed | Source guards cover dialog roles, accessible labels, focus containment, Escape handling, and return focus |
| Calendar control context | Passed | Event controls include full date context; view controls expose pressed state |
| Mobile chooser containment | Passed | Source guards cover safe-area positioning, bounded height, independent scrolling, contained keyboard navigation, and touch-sized rows and checkboxes |
| Timeline readability | Passed | Timeline and all-day labels use the accessible muted text color |
| Color contrast regression | Passed | Automated WCAG contrast calculations require at least 4.5:1 for normal-text palette pairs listed below |
| Build and regression suite | Passed | Production build and all automated tests passed at the time of this record |

## Verified contrast pairs

| Text pair | Contrast ratio |
| --- | ---: |
| Primary text on page | 11.90:1 |
| Muted text on page | 4.59:1 |
| Muted text on white | 5.15:1 |
| White primary-action text on green | 6.67:1 |
| Red owner text on tint | 5.44:1 |
| Yellow owner text on tint | 5.61:1 |
| Gold owner text on tint | 4.98:1 |
| Green owner text on tint | 4.70:1 |
| Blue owner text on tint | 5.63:1 |
| Orange owner text on tint | 5.63:1 |

Color is supplemented by visible names, event text, labels, button states, or read-only badges; it is not intended to be the sole carrier of meaning.

## Required human test matrix

| Test | Required coverage | Status |
| --- | --- | --- |
| Keyboard-only operation | Logical order, visible focus, no trap outside open dialogs, every action reachable, Escape behavior | Pending |
| Desktop screen reader | Current supported Windows browser with NVDA or equivalent; names, roles, states, errors, dates, and dialog announcements | Pending |
| Mobile screen reader | Current supported iPhone/iPad with VoiceOver; touch exploration, rotor order, dialog containment, and status announcements | Pending |
| Zoom and reflow | 200% and 400% zoom plus 320 CSS-pixel reflow without loss of information or two-dimensional scrolling except the calendar grid | Pending |
| Orientation | Phone and supported tablet in portrait and landscape, including open chooser and event dialogs | Pending |
| Touch targets | Key actions and dense calendar controls on supported touch devices | Pending |
| Motion and visual preferences | Reduced-motion, increased contrast where supported, text spacing, and focus visibility | Pending |
| Error recovery | OCR uncertainty, validation errors, expired authentication, interrupted writes, duplicate detection, and denied deletion | Pending |

## Unsupported legacy boundary

First-generation tablets limited to obsolete browser engines are not part of the full web-application conformance target. The documented fallback is the built-in calendar application with only approved calendars visible. This fallback still requires household acceptance testing and must not be described as equivalent web support.

## Known limits of automation

Static checks cannot prove reading order, accessible-name quality, actual screen-reader announcements, focus behavior in every runtime state, zoom usability, cognitive clarity, or touch performance. Automated success therefore cannot be converted into a WCAG, ADA, or Section 508 compliance claim.

## Exit criteria for a conformance assessment

1. Execute every pending row on declared supported browser/device combinations.
2. Record reproducible evidence and severity for each failure without capturing personal calendar data.
3. Remediate all applicable WCAG 2.2 Level A and AA failures.
4. Retest regressions and obtain an independent accessibility review.
5. Define the exact pages, states, technologies, and supported user agents covered by any future conformance statement.
