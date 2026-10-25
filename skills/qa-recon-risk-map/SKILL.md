---
name: qa-recon-risk-map
description: Map a product's journeys, roles, states, integrations, and recent changes into a risk-ranked coverage matrix with test case IDs. Use after preflight and before executing tests, or when asked what to test.
---
# Recon and Risk Map

## Procedure
1. Read requirements, acceptance criteria, pricing and offer pages, the README, API specs, and DB schema.
2. Enumerate surfaces from the running system: sitemap, route list, network calls during a full walkthrough, registered webhooks, cron jobs, and workflows.
3. Write the primary journey in one line, for example: enter site → verify email → create item → see progress → preview → pay → full access → return later.
4. Build the matrix: feature × role × state (new, returning, paid, expired, refunded) × device × integration. Give each cell an ID such as `PAY-03-mobile-webkit`.
5. Score risk = impact (money, access, data, irreversibility, primary journey) × likelihood (recent change, complexity, past bugs, third-party dependency). Order work by score.
6. Read `01-BUG-PATTERN-LIBRARY.md` and add a case for every pattern that applies.
7. Pull history: `git log --since=30.days`, open issues, and earlier QA reports. Recently changed areas get extra cases.
8. Start the assumption register for every requirement you had to guess.

## Exit criteria
- The matrix has IDs, risk scores, and a planned skill per row.
- Every matrix row starts as NOT RUN.

## Pitfalls
- Using the implementation as the spec.
- Skipping the returning-user and second-account states, where many bugs hide (pattern A1).
