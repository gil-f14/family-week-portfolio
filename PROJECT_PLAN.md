# Family Week — Program and Release Plan

**Plan date:** September 2026  
**Delivery model:** Small, gated increments with a private pilot before any public portfolio release

## Completed delivery timeline

| Period | Release milestone | Product outcome | Program evidence |
| --- | --- | --- | --- |
| Aug 19–25, 2026 | Foundation | Durable Google session, core calendar workflow, private deployment integration | Initial build and calendar-path tests |
| Aug 26–27, 2026 | Recognition and review | Timed sample validation, guarded OCR, self-hosted models, correction pipeline, side-by-side review, local dictionary | OCR integrity checks and review safeguards |
| Aug 28, 2026 | V1 private release | Batch validation, all-calendar duplicate checks, retry recovery, release criteria | V1 release decision and production-readiness checklist |
| Aug 29, 2026 | Safety and portfolio controls | Safe-delete specification and public-release gate | Sanitization and disclosure controls documented |
| Aug 30–Sep 1, 2026 | V2 core | Quick add, one-hour default, safe deletion, read-only overlays, weather on request, mobile calendar, colors, full-day scrolling, tablet display mode | Feature tests and private iterative deployments |
| Sep 1–2, 2026 | Accessibility hardening | Mobile chooser containment, dialog focus management, keyboard dismissal, spoken event-date context | 65 automated tests passing and private deployment |

Internal hosting revision numbers and deployment identifiers are intentionally excluded from the public portfolio.

## Current release state

### V1

Complete for private pilot use. The core photo-to-reviewed-calendar workflow, duplicate checks, constrained writes, and session durability are implemented.

### V2

Feature-complete at the core level. Manual supported-device, accessibility, and end-to-end release verification remain before describing it as broadly production-ready.

### V3

Planned. Automatic weather presentation, place autocomplete, and advanced shared-device access remain outside V2.

## Four-week closeout plan

| Timing | Workstream | Deliverables | Exit criteria |
| --- | --- | --- | --- |
| Week 1 | Product verification | Create/duplicate/delete test, readable-calendar confirmation, defect triage | No incorrect calendar mutations; priority defects resolved |
| Week 1–2 | Accessibility validation | Keyboard, screen reader, zoom/reflow, contrast, touch targets, portrait/landscape | Test record completed; blockers fixed; remaining issues documented |
| Week 2 | Security evidence | Threat model, dependency/license review, vulnerability scan, secret and PII scans | No unresolved critical/high finding; evidence retained privately |
| Week 2–3 | Portfolio clean export | Synthetic examples, sanitized documentation, new Git history, private GitHub staging | All public-release gates pass except final owner approval |
| Week 3 | Employer presentation | Final case study, architecture graphic, optional synthetic screenshots, interview walkthrough | Narrative reviewed for accuracy and privacy |
| Week 4 | Release decision | Manual review and explicit decision to keep private or publish portfolio | Approval recorded; monitoring owner assigned |

## V3 planning horizon

| Phase | Estimated duration | Scope | Dependency |
| --- | --- | --- | --- |
| Discovery | 3–5 working days | Provider selection, cost/privacy review, UX prototypes | Approved weather and place providers |
| Location autocomplete | 5–8 working days | Search, selection, address normalization, failure states | Provider keys, quotas, and terms |
| Automatic weather | 5–8 working days | Event-time forecast, freshness labeling, caching, graceful fallback | Location resolution and forecast policy |
| Shared-device access | 8–15 working days | Identity model, least-privilege sharing, revocation, recovery | Security/privacy design approval |
| Validation | 5 working days | Supported devices, accessibility, security, regression | Feature-complete V3 candidate |

Estimates assume one product owner working with AI-assisted engineering and include implementation plus automated validation, but not third-party review or provider approval lead time.

## Release governance

- Every release has an explicit scope, acceptance criteria, and rollback path.
- Live calendar mutations require human authorization during testing.
- Build and tests must pass before private deployment.
- Access stays owner-only unless a separate access change is explicitly approved.
- Public GitHub publication uses a new clean repository and new history.
- Standards claims are evidence-based and use “aligned,” “partially aligned,” or “target” until formal validation is complete.

## Risks and mitigations

| Risk | Impact | Mitigation | Owner |
| --- | --- | --- | --- |
| Handwriting recognition error | Wrong event details | Side-by-side review, confidence gating, fail-closed validation | Product/Engineering |
| Duplicate or partial write | Calendar clutter or uncertainty | Cross-calendar checks, deterministic IDs, retry-safe messaging | Engineering |
| Excess calendar access | Privacy exposure | Least-privilege scopes and app-owned mutation boundary | Security/Engineering |
| Legacy tablet incompatibility | Unusable shared display | Supported-device policy and Apple Calendar fallback | Product |
| Accessibility regression | Users blocked from core flow | WCAG 2.2 AA target and release test matrix | Design/Engineering |
| Portfolio privacy leak | Personal or credential exposure | Clean export, new history, automated and manual gates | Release owner |
| External API cost or data expansion | Budget/privacy risk | V3 provider review, minimization, caching, explicit limits | Product/Security |

## Definition of done for employer-ready portfolio

- Sanitized PRD, one-pager, architecture, plan, and compliance matrix agree on scope and status.
- All examples are synthetic and no private link or identifier is present.
- Claims can be traced to implementation or test evidence.
- Known limitations and unfinished verification are visible.
- The public repository begins private, contains new history, and receives explicit approval before publication.

