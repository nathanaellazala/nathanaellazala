# Career portfolio handoff

Prepared November 17, 2026. Work remains in unmerged branches and pull requests. No deployments, trades, customer-data access, credential changes, or LinkedIn edits were performed. The public business homepage was retrieved read-only and returned HTTP 200; its deployed JavaScript behavior was not tested.

## Review these pull requests

| Priority | Repository / PR | Purpose |
| --- | --- | --- |
| 1 | [CRM #3](https://github.com/nathanaellazala/Medicare-CRM/pull/3) | Remove hidden owner startup provisioning, expose legacy hidden accounts to owner listing, stop writing obsolete default-login instructions, add bootstrap tests and CI |
| 2 | [CRM #4](https://github.com/nathanaellazala/Medicare-CRM/pull/4) | Secure cookies by default, reject inactive refresh accounts, add offline session tests and CI |
| 3 | [CRM #5](https://github.com/nathanaellazala/Medicare-CRM/pull/5) | Require explicit local isolation for mutating integration tests |
| 4 | [Bot #2](https://github.com/nathanaellazala/DiscordTradingBot/pull/2) | Exercise ambiguous broker failures and run offline Python/JS CI |
| 5 | [Website #1](https://github.com/nathanaellazala/vertexwebsolutions/pull/1) | Add developer case studies, improve documentation/navigation, clarify demos, remove rendered placeholder testimonials, repair npm build reproducibility |
| 6 | This profile/career-review PR | Correct stale source-publication status and prepare career documents for factual review |

These are review artifacts. The user explicitly authorized publishing this career-review pack, including résumé drafts and contact information, in a public GitHub review branch and draft PR on November 17, 2026. Approval is still required before merge, production deployment, account remediation, submission or publication of final résumés, or LinkedIn publication. Check repository deployment workflows before any approved merge.

## Phase 1 — security and reliability

**Completed:** cloned all three repositories including reachable default-branch history; inspected key backend, authentication, bootstrap, API-client, bot order-state, message-validation, bridge, and website configuration code; reviewed tests before execution; prepared three independent CRM PRs and one bot PR. The merged first-owner fix is commit `58a6697`, merged in `489cabd`; seed behavior was exercised offline without a real database. The in-process smoke test ran the proposed hidden-owner-removal branch with synthetic credentials and an in-memory MongoDB substitute.

**Security findings:**

- High priority: startup on main can create or promote/reactivate a hidden owner using MASTER_EMAIL / MASTER_PASSWORD, and resets its password on startup. Removing this code does not remove already-existing hidden accounts. An authorized owner must review and remediate those separately. No production account list was accessed.
- High priority: predictable owner/agent credentials remain in historical source and current tests. Historical seed blob `0e2d0bc4fdebdd5abd4f22caf2fa82976f07180c` includes a predictable password assignment; earlier `backend/seed.py` revisions are reachable. If any such credentials were ever active, rotate affected accounts and invalidate sessions through an approved administrative process. The merged fix does not rotate existing accounts. No credentials were tried against a live service.
- Main issues cookies with Secure disabled. PR #4 changes the default; HTTPS deployment configuration must be reviewed.
- Main refresh does not reject inactive accounts; PR #4 adds that check. Access-token lookup already rejects inactive accounts.
- Access tokens remain in localStorage and in login JSON. XSS, refresh reuse, logout/password-reset revocation, CSRF/origin policy, authentication rate limits, and secret-strength validation still need a coherent session design.
- CRM allows wildcard origins with credentials disabled while the frontend enables credentialed requests; cross-origin browser behavior requires explicit environment review.
- Startup includes migrations/backfills and obsolete credential-file writing; PR #3 removes credential-file writing only. Do not point demonstrations at a real database.
- Database network exposure, database user roles/ACLs, TLS, backups, retention, and environment secrets cannot be verified from source. No production database was contacted.
- Reassignment deletes notes, calls, and per-lead audit records. This is existing intentional behavior in source; retention requirements need business review before real use.
- Bot loopback bridge trusts extension-origin strings, not cryptographic sender identity. DOM drift, forged local requests, bounded dedupe history, partial fills, cancellations, and real reconciliation remain risks. No live mode or broker SDK calls were executed.
- Website backend includes unauthenticated status-check storage; it should not be exposed as a production data endpoint without a separate decision.

**History scan:** a redacted heuristic scan inspected 288 CRM, 19 bot, and 130 website reachable blobs at scan time. Patterns covered recognizable GitHub/AWS tokens, private keys, credential-bearing MongoDB URLs, and quoted password/secret/token assignments. Five CRM blob/pattern matches were flagged: a shell variable-read false positive, synthetic test data, two test modules, and the historical seed. No matches were found in the bot or website under these patterns. This is not an exhaustive secret or personal-data audit; generic assignments, logs/test reports, deleted/unreachable refs, encoded values, and provider-specific tokens can be missed. Pattern absence is not a clean bill of health.

**Tests/checks:**

| Check | Result and practical limit |
| --- | --- |
| CRM bootstrap unittest | 4 pass: no settings, partial/weak settings, explicit synthetic owner, existing-owner preservation |
| CRM session unittest | 3 pass: cookie flags, inactive refresh denial, active refresh cookie |
| Combined offline CRM test files in temporary checkout | 7 pass; source composition only, no Git merge performed |
| CRM ASGI smoke with in-memory database | Startup provisions one synthetic owner and no hidden user; owner-only visibility of a synthetic legacy hidden account; unauthenticated request 401; login/me 200; inactive access 403 |
| CRM existing integration suite | Refused before collection without explicit isolation; full suite not executed because disposable real MongoDB and historical fixtures were not provisioned |
| Bot existing suite | 43 Python tests pass |
| Bot proposed suite | 46 Python tests pass, including ambiguous entry restart, uncertain take-profit/API failure, corrupt state |
| Bot JavaScript matcher | 6 tests pass |
| CRM frontend test command | No tests found; zero exit with passWithNoTests does not establish tested components |
| CRM strict CI build | Fails on three existing React effect-dependency warnings in ApplicationInfo, LeadDetail, Settings after local AJV resolution repair |
| CRM non-CI build | Builds with those warnings after an uncommitted local AJV installation; this does not prove a clean-checkout reproducible build |
| Website build on proposed PR | CI=true build passes after direct AJV development dependency and lockfile |
| Website frontend tests | No tests found; no component test coverage claimed |
| Website browser preview | Blocked: managed relay timed out waiting for readiness; preview stopped |
| GitHub Actions | Workflows prepared; see individual PR checks for actual remote status. [Session CI passed](https://github.com/nathanaellazala/Medicare-CRM/actions/runs/44064901713) and [bot CI passed](https://github.com/nathanaellazala/DiscordTradingBot/actions/runs/44065278427); [bootstrap CI passed on the final visibility-adjustment head](https://github.com/nathanaellazala/Medicare-CRM/actions/runs/44066579072) |

The full original Python dependency lists were not installed or vulnerability-audited. A minimal application-import environment was used for offline CRM tests; the bot's tests use Pillow and standard-library mocks. Existing dependency pins include environment-specific and unrelated packages and need cleanup.

## Phase 2 — GitHub portfolio

**Completed:** reviewed important application paths and source maps; preserved the CRM and bot's useful README structure; documented website features, architecture, setup, tests, and limitations; corrected the profile's stale claim that the bot source was unpublished. Added readable architecture descriptions in website case studies and README. CI added for offline safety regressions. Proposed résumé text avoids claiming the new agent-produced fixes as independently authored candidate achievements.

**Recommended pins:** CRM (API/full-stack depth), bot (Python/state/testing), Vertex (presentation/UI). Keep security and prototype limits visible. Do not pin a market-data pipeline as a verified achievement until its source and reproducibility are reviewed.

**Not complete:** exhaustive file-by-file review of every application/UI component; dependency vulnerability audit; sanitized screenshots/GIFs; a full synthetic CRM demo with real disposable MongoDB; verification of real client outcomes; separate pipeline evaluation. The bot's existing `--demo-alert` and mocked tests offer an offline demonstration path; do not use live mode. The new `/developer` section is a presentation demo requiring no customer data.

## Phase 3 — website

**Completed:** source review of routing, navigation, service selector, portfolio, metadata, testimonials, and backend scaffold. Website PR adds developer case studies with problem, technical solution, architecture, verification limits, tradeoffs, source links, and email contact. No résumé file is linked publicly while facts remain unconfirmed. The proposed landing-page source removes the placeholder testimonials from rendering; the old component remains in source for replacement with approved real feedback. The deployed homepage was not changed.

**Verification:** proposed production build passes. Public homepage HTTP response is 200, but source/host equivalence is not established. Browser preview infrastructure failed, so responsiveness, keyboard behavior, contrast, accessibility scores, live navigation, and performance scores are unverified. No screenshots were fabricated.

**Remaining:** mobile browser QA; 404/deep-link hosting behavior; per-route metadata/canonicals/social previews; real performance measurement; approved résumé download; verified client screenshots and outcomes. Static HTML currently uses homepage metadata for all routes. No deployment occurred.

## Phase 4 — LinkedIn

**Completed:** exact review-ready headline, About text, project descriptions, conditional Vertex experience copy, skills, Featured order, and Open to Work suggestions in [LINKEDIN-DRAFT.md](LINKEDIN-DRAFT.md).

**Blocker:** people search found no matching profile; tool supports search only. Profile URL and history are needed to review actual education, dates, and experience. No profile was edited. Skills from source should be added only if you can personally demonstrate them.

## Phase 5 — résumés

**Completed:** three one-page PDF drafts with matching editable Word and Markdown copies: junior software developer, automation/implementation, SaaS technical support. Standard single-column text with no graphics or tables. PDF text extraction confirms searchable text and project links. Comparisons against real job descriptions are in the application plan.

**Not final:** employment/education dates, actual job titles, individual contribution details, AI assistance, location, and work eligibility are missing. Drafts use project descriptions rather than fabricated employment accomplishments. Do not submit them without factual review. Formal ATS ingestion was not tested; conventional layout is not a guarantee about a particular employer's system.

## Phase 6 — interviews and applications

**Completed:** three project explanation outlines, fifteen code-based practice questions, honest bug/tradeoff discussion prompts, eight prioritized exercises, a targeted application workflow, pay-goal arithmetic, and comparison to three real postings in [INTERVIEW-AND-APPLICATION-PLAN.md](INTERVIEW-AND-APPLICATION-PLAN.md). Some benchmark roles have location, authorization, or experience requirements not yet established; they are not presented as guaranteed matches. No applications or outreach were sent.

## What is needed from you

1. Review the PR diffs; decide whether to approve any merges. Deployment and production account remediation remain separate approval decisions.
2. Provide your exact LinkedIn URL, work/education history with dates, location/eligibility/preferences, and personal versus AI contributions to each project.
3. Identify any historical default accounts that were ever active, through an authorized private administrative process. Do not paste active passwords or secrets into this PR.
4. Supply the market-data pipeline source if you want that evaluated as a fourth project.
5. Once facts and infrastructure are ready, finish real disposable-database integration tests, browser QA, synthetic demonstrations/screenshots, final résumé exports, and approved publication.

## Artifact handling

Career files are in this unmerged review branch. PDF and Word copies are review drafts. The session's designated local output path was not writable in the managed environment, so review artifacts are delivered through this GitHub PR instead of local file links. No privileged filesystem changes were made to work around that limit.
