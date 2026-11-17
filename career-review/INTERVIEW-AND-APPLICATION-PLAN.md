# Interview and application preparation

Prepared November 17, 2026. These are project-grounded study prompts and a strategy, not claims that you have already mastered every topic.

## Explain the three strongest projects

**CRM:** A React UI calls a FastAPI REST API. MongoDB stores users, leads, notes, calls, and related workflow records. Authentication uses signed JWTs and user lookup; owner checks protect administrative operations. Follow one lead from CSV intake through assignment and an agent update. Explain which checks live on the server, how hidden-field masking works, and why UI visibility alone is not authorization. Admit that database ACLs, full integration tests, and deployed security remain unverified.

**Alert automation:** Rendered Discord messages pass through an extension and a local HTTP bridge. Python validates message age, channel, language, and duplicates. The engine uses persisted state and client order identifiers; dry-run is the default. Explain why uncertain network acknowledgements must not trigger blind retries. Tests use mock broker objects; no claim of real fills or investment performance is justified.

**Vertex:** React Router selects business, client-work, and proposed developer pages. Reusable components present services and contact actions. Explain the difference between a front-end service selector and a real connected AI product. Discuss the balance between animation, accessibility, bundle size, and content clarity. Source review and successful build are not mobile or performance certification.

## Code-based practice questions

1. How does `require_owner` differ from hiding a menu item? What tests would prove an agent cannot access another agent's record?
2. Why are cookies marked HttpOnly, Secure, and SameSite? Why does localStorage still matter for XSS risk?
3. Why can disabling an account be checked immediately while password changes may leave old JWTs valid? Design revocation and refresh-token rotation.
4. What could happen if two startup workers both try to create the first owner? How would an atomic provisioning workflow improve this?
5. Why is a unique email index useful? What does it fail to guarantee about the number of owners?
6. Explain the consequences of deleting notes and audit history when reassigning leads. What should the retention policy be?
7. Why does the bot persist `ENTRY_UNKNOWN` before making the broker request? What happens if the acknowledgement is lost?
8. When should an API request be retried? Explain client request IDs, idempotency, timeouts, and reconciliation.
9. Why are message creation time and arrival time different? How do startup baselines and stale-message checks help?
10. Can a `chrome-extension://` Origin prove sender identity? Explain the remaining trust assumptions.
11. Why are partial fills harder than a single successful request? What must be known before a take-profit order can be placed?
12. How would you diagnose a React page that displays stale data after a route change? Explain effect dependencies and stale closures.
13. Why might a client-rendered `/developer` page still have the homepage canonical URL in static HTML?
14. What does a passing mocked test establish, and what does it leave unknown?
15. Walk through one generated PR diff without AI assistance. Explain each behavior change and its remaining risks.

## Honest bug and tradeoff stories

Use these as learning/review stories until you personally reproduce and understand them; do not say you independently discovered or fixed them if you did not.

- Startup privilege management: predictable default seeding had been removed, but a separate hidden-master path still existed. The proposed fix removes that startup behavior and makes legacy hidden accounts visible to owners. Existing accounts are not deleted.
- Cookie and refresh behavior: the proposed fix enables Secure by default and rejects inactive refresh accounts. Remaining problems include token revocation and browser local storage.
- Test isolation: hosted-preview defaults made an integration suite unsafe to invoke blindly. The proposed gate requires loopback configuration and synthetic isolation.
- Ambiguous broker responses: additional tests retain unresolved state across restart and avoid assuming a timeout means the broker rejected an order.
- Website reproducibility: npm dependency resolution initially failed around AJV; the website PR adds an explicit dependency and lockfile. Building a page still does not prove its accessibility or business impact.

## Practical exercises, in priority order

1. Reproduce all seven CRM offline tests after combining the two security branches locally. Trace why each test would fail before its fix.
2. Design session revocation on paper, then implement it in a disposable demo with per-session identifiers and refresh rotation. Test logout, password reset, replay, and deactivation.
3. Add one isolated authorization integration test with two synthetic agents and owner, including direct-object access and hidden-field update attempts.
4. Build a tiny SQLite/PostgreSQL issue tracker to demonstrate joins, indexes, migrations, and safe parameterized queries. SQL is a recurring gap against job descriptions.
5. Write a support runbook: symptom, reproduction, expected/actual behavior, sanitized logs, diagnosis, workaround, escalation, verification.
6. Build one small actual LLM automation with synthetic inputs, structured-output validation, timeouts, cost bounds, and an evaluation set before claiming AI integration experience.
7. Reproduce the bot failure tests and explain state transitions without running live trading.
8. Complete keyboard/mobile/browser QA once preview infrastructure works; capture sanitized screenshots only from synthetic or public presentation content.

## Application strategy

Assuming the goal is US dollars, $700/week equals $17.50/hour at 40 paid hours, or $36,400/year at 52 paid weeks, before tax and unpaid time. This is arithmetic, not a salary or hiring guarantee. If the target is take-home pay, the required gross pay is higher and depends on your circumstances.

Prioritize roles with defined junior responsibilities, training, and software/API exposure. Split an initial search between junior development, implementation/onboarding, and SaaS support; adjust based on response rates. Favor local or hybrid opportunities you can actually attend alongside eligible remote roles, once your location and work eligibility are confirmed.

For each application: verify location and eligibility; identify three required skills; choose the matching résumé; link two relevant projects; write a short evidence-based note; log the date, role, status, compensation if stated, and next action. Aim for 10–15 carefully matched applications per week plus project study. Do not use this plan to auto-submit applications or messages.

## Representative real job-description comparisons

Retrieved November 17, 2026. Availability may change. These are benchmarks, not a claim that you satisfy their location, authorization, experience, or education requirements.

| Benchmark | Relevant evidence in portfolio | Gaps / screening conditions | Résumé choice |
| --- | --- | --- | --- |
| [Self Financial — Associate Software Engineer](https://job-boards.greenhouse.io/selffinancial/jobs/6255478004) | Python/FastAPI, REST, project source, tests, PR workflow | SQL and CS fundamentals need evidence; Austin hybrid; US citizen/permanent-resident requirement stated | Junior software developer |
| [Revinate — Technical Implementation Specialist](https://jobs.lever.co/revinate/b258ae78-6a7c-45eb-92e0-6f60d8da0fff) | Business interfaces and configuration-oriented workflows | Search listing describes two years of professional experience and support/project tools; full-page fetch was blocked, so verify current detail before applying | Automation / implementation |
| [Tines — Technical Support Engineer I](https://job-boards.greenhouse.io/tines/jobs/6220290004) | API, JWT, Python, workflow testing | Ireland remote, two years SaaS support, customer handling, GraphQL/SQL and network skills not established; published schedule details differ within page and require clarification | SaaS technical support |

Résumé review result: the project-based drafts align with Python/REST/React and workflow vocabulary without adding unsupported SQL, ticketing-platform experience, employment dates, degrees, or customer-service history. They cannot be finalized as employment résumés without those facts. AI model/agent claims are intentionally omitted because no working LLM integration was verified.

## Market-data pipeline showcase decision

No pipeline repository was supplied among the three audited repositories, so quality and authorship cannot be evaluated. Give it a separate showcase only if you can provide sanitized source, permitted/sample data, replayable inputs, schema validation, reconnect and duplicate handling, benchmarks with methodology, tests, and a clear boundary between historical simulation and real-time operation. A small reproducible replay pipeline would be a stronger initial showcase than an unverified profitability claim.
