# Family Week — Employer Portfolio Pack

This directory is the public-safe narrative for Family Week. It describes the product, delivery approach, architecture, and control posture without exposing the private application, household data, credentials, deployment identifiers, or production URLs.

## Recommended reading order

1. [Portfolio one-pager](PORTFOLIO_ONE_PAGER.md) — concise product case study.
2. [Product requirements document](PRD.md) — problem, users, requirements, acceptance criteria, and roadmap.
3. [Architecture one-pager](ARCHITECTURE_ONE_PAGER.md) — system boundaries and key design decisions.
4. [Program and release plan](PROJECT_PLAN.md) — completed milestones, release gates, and forward plan.
5. [Compliance readiness](COMPLIANCE_READINESS.md) — evidence-based standards mapping and known gaps.
6. [NIST current and target engineering profile](NIST_CURRENT_TARGET_PROFILE.md) — prioritized cybersecurity and privacy outcomes, roles, evidence, and gaps.
7. [Privacy impact assessment](PRIVACY_IMPACT_ASSESSMENT.md) — data lifecycle, minimization, risks, controls, and approval conditions.
8. [Privacy-safe monitoring plan](PRIVACY_SAFE_MONITORING_PLAN.md) — content-free events, prohibited fields, thresholds, retention targets, and verification gates.
9. [OWASP ASVS readiness matrix](OWASP_ASVS_READINESS.md) — Level 2 target, present evidence, priority gaps, and verification exit criteria.
10. [Accessibility test record](ACCESSIBILITY_TEST_RECORD.md) — completed automated evidence, contrast results, and the required human test matrix.
11. [Private-pilot acceptance checklist](MORNING_ACCEPTANCE_CHECKLIST.md) — concise human calendar, responsive, accessibility, cleanup, and stop-condition checks.
12. [Synthetic end-to-end test plan](SYNTHETIC_E2E_TEST_PLAN.md) — safe live-calendar verification and cleanup procedure.
13. [Security threat model](THREAT_MODEL.md) — assets, trust boundaries, STRIDE analysis, misuse cases, and residual risks.
14. [Security operations runbook](SECURITY_OPERATIONS_RUNBOOK.md) — severity targets, minimal-evidence rules, incident playbooks, and recovery gates.
15. [Live security-header record](LIVE_SECURITY_HEADER_RECORD.md) — sanitized read-only evidence from the private deployment and its limitations.
16. [Security review](SECURITY_REVIEW.md) — completed portfolio checks, compensating controls, and residual risk.
17. [Security policy](SECURITY.md) — private vulnerability-reporting expectations.
18. [Public release gate](PUBLIC_RELEASE_GATE.md) — mandatory checklist before any GitHub repository becomes public.

## Publication boundary

These Markdown files are intended to be portable into a separate portfolio repository after the release gate is completed. The private working repository must not be made public or have its Git history copied into the portfolio repository.

The public portfolio should use only synthetic screenshots and test data. It must not link to the private application or name real people, accounts, schools, teams, schedules, locations, calendars, or cloud resources.
