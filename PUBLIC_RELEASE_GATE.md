# Public Portfolio Release Gate

Status: **BLOCKED — not approved for public release**

This checklist governs creation of a separate public portfolio repository. The working product repository remains private. Publication is prohibited until every required gate is complete and a person performs the final review.

## Standards alignment and limits

This gate is informed by:

- [NIST Cybersecurity Framework 2.0](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20): Govern, Identify, Protect, Detect, Respond, and Recover.
- [NIST SP 800-122](https://csrc.nist.gov/pubs/sp/800/122/final): identify PII, assess confidentiality impact, apply safeguards, and prepare for incidents.
- [NIST SP 800-218 SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final): integrate secure practices into the software development lifecycle.
- [NIST Privacy Framework 1.0](https://www.nist.gov/privacy-framework): inventory data processing, define target privacy outcomes, verify them before release, and reassess over time. Version 1.1 remains an Initial Public Draft as of this review and is monitored, not claimed as the baseline.
- [NIST AI Risk Management Framework 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10): govern, map, measure, and manage OCR risks with visible uncertainty and human review. NIST is revising AI RMF 1.0, so the mapping must be revisited when a final successor is published.
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/): target Level AA for the complete responsive experience; do not claim conformance until full-page automated and manual evaluation is complete.
- [OWASP ASVS 5.0.0](https://owasp.org/www-project-application-security-verification-standard/): use as a future application-security verification baseline only after selecting a level and completing a requirement-by-requirement assessment.

This is a practical NIST-aligned control set for a small portfolio project. It is not a certification, legal opinion, compliance attestation, or substitute for an independent security assessment.

## Non-negotiable release rule

Use a clean export with new Git history. **Never change the working repository from private to public.** A deleted value may remain in Git history, cached views, forks, workflow logs, or artifacts.

The public repository must begin private. It may become public only after automated scanning, manual review, and explicit owner approval.

## Information classification

### Public-safe after review

- Generic product description and architecture.
- Source code containing only placeholder configuration.
- Synthetic household members, schedules, dates, locations, and screenshots.
- Test data that cannot reasonably be linked to a real person or household.
- General security decisions that do not reveal credentials or exploitable deployment details.

### Prohibited from public release

- Real names, initials used as family identifiers, email addresses, phone numbers, usernames, or account IDs.
- Information about minors, family relationships, schools, teams, medical care, appointments, work schedules, birthdays, routines, or travel.
- Home, school, workplace, venue, or precise location information.
- Original photographs, OCR inputs, calendar exports, screenshots of real calendars, browser data, or clipboard captures.
- Event titles, notes, attendees, calendar IDs, stable event IDs, or duplicate-scan results from real calendars.
- OAuth client IDs/secrets, API keys, bearer/refresh tokens, session secrets, cookies, authorization codes, private keys, or credential files.
- Production URLs, hosting project IDs, internal repository URLs, account allowlists, IP addresses, request IDs, logs, database files, or deployment artifacts.
- Prompt transcripts, support conversations, terminal output, crash dumps, or diagnostic bundles that may contain contextual personal data.

## Gate 1 — Govern and scope

- [ ] A named release owner is responsible for the decision.
- [ ] The public purpose is limited to an employer-facing portfolio demonstration.
- [ ] The working repository, live application, cloud configuration, and real calendar data remain private and out of scope.
- [ ] Third-party package, model, font, image, and icon licenses permit redistribution.
- [ ] The README accurately describes AI assistance and the human product/engineering contribution.
- [ ] The repository license is deliberately selected; public visibility is not treated as automatic permission to reuse the code.

## Gate 2 — Create a clean export

- [ ] Copy only an approved allowlist of source, test, and documentation files into a new directory.
- [ ] Do not copy `.git`, `.openai/hosting.json`, environment files, deployment output, logs, databases, screenshots, photographs, or temporary files.
- [ ] Create a new repository with one sanitized initial commit; do not preserve working-repository history.
- [ ] Replace household names with `Parent A`, `Parent B`, `Child A`, `Child B`, `Family`, and `Unassigned`.
- [ ] Replace schedules, dates, activities, addresses, and correction examples with independently invented synthetic data.
- [ ] Replace deployment-specific URLs with `https://example.invalid` or remove them.
- [ ] Use an empty `.env.example` containing variable names only.

## Gate 3 — Automated detection

- [ ] Run a recognized secret scanner against every file and the complete new repository history.
- [ ] Run case-insensitive searches for emails, phone numbers, account names, family names, schools, locations, production domains, project IDs, calendar IDs, and credential keywords.
- [ ] Inventory every binary file and manually open it; metadata and pixels must both be free of personal data.
- [ ] Scan dependency manifests for known vulnerabilities and review high/critical findings.
- [ ] Verify that generated files, source maps, build output, caches, and test snapshots are excluded.
- [ ] Treat any uncertain match as a release blocker until a person resolves it.

Minimum deny patterns include email addresses, phone-number-like strings, credential assignments with non-placeholder values, private-key headers, OAuth authorization codes, access/refresh tokens, production deployment domains, and opaque cloud resource identifiers.

## Gate 4 — Manual privacy review

- [ ] Review every public file line by line after automated substitutions.
- [ ] Search for contextual identifiers that scanners miss, including initials, nicknames, team names, school names, recurring routines, and recognizable combinations of dates and activities.
- [ ] Confirm screenshots contain synthetic content only and have no notifications, browser profile details, tabs, bookmarks, filenames, or image metadata.
- [ ] Confirm the Git author name/email are intentionally public portfolio identities.
- [ ] Confirm commit messages contain no personal, customer, or deployment information.
- [ ] Confirm documentation contains no link to the private live application.

## Gate 5 — Security and quality validation

- [ ] Install dependencies from the lockfile in the clean export.
- [ ] Run the full automated test suite and production build.
- [ ] Verify authentication and calendar integrations use environment variables and documented placeholder setup.
- [ ] Verify the sample application cannot reach the private production deployment or real calendar resources.
- [ ] Review least-privilege scopes and clearly explain that adopters must create their own OAuth configuration.
- [ ] Add a security policy describing private vulnerability reporting without publishing a personal email address.

## Gate 6 — GitHub staging

- [ ] Create the new GitHub repository as **private** first.
- [ ] Push only the sanitized repository and inspect the rendered files, commit, branches, tags, releases, Actions, artifacts, and package metadata.
- [ ] Enable secret scanning, push protection, dependency alerts, and supported code scanning.
- [ ] Confirm there are no forks, stale branches, hidden tags, releases, workflow artifacts, or cached public previews.
- [ ] Obtain explicit owner approval immediately before changing visibility to public.

## Gate 7 — Post-publication monitoring

- [ ] Re-run secret and PII scans after every material update.
- [ ] Review dependency and code-scanning alerts.
- [ ] Keep production data and portfolio examples separated by process and directory.
- [ ] Reassess privacy risks when adding screenshots, analytics, demos, issue templates, or contributor workflows.

## Incident response

If sensitive data is discovered:

1. Stop publication or make the portfolio repository private immediately.
2. Revoke and rotate exposed credentials before attempting repository cleanup.
3. Preserve only the minimum evidence needed to understand the incident; do not spread the sensitive value through tickets or chat.
4. Remove the data from files and history using GitHub's current sensitive-data procedure.
5. Check forks, caches, workflow logs, releases, artifacts, package registries, and clones for continued exposure.
6. Document the cause and add a preventive control before republishing.

## Final release record

### Sanitized documentation pack

| Required evidence | Result |
| --- | --- |
| PRD, one-pager, architecture, project plan, and readiness matrix agree on scope | Complete |
| Known household names, account strings, private domains, addresses, and cloud identifiers pattern scan | Passed |
| Email, phone, private-key header, and common credential pattern scan | Passed |
| Binary-file inventory inside the documentation pack | Passed — no binary files |
| AI-assisted line-by-line content review | Complete |
| Human owner review of rendered GitHub documents | Pending |

The documentation pack is ready for private GitHub staging after the human owner review. This result does not make the application source or working repository public-safe.

### Full public source repository

| Required evidence | Result |
| --- | --- |
| Clean export created without prior Git history | Pending |
| Automated secret scan | Pending |
| Automated PII/context scan | Pending |
| Binary and screenshot review | Pending |
| Dependency and code scan | Pending |
| Tests and production build | Pending |
| Manual line-by-line review | Pending |
| Private GitHub staging review | Pending |
| Explicit approval to publish | Pending |

Public release remains **BLOCKED** while any result is Pending, Failed, Unknown, or Not Reviewed.
