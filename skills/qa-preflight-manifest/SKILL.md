---
name: qa-preflight-manifest
description: Start every bug-testing run by filling a run manifest, fingerprinting the live build, and confirming access, scope, budgets, and prohibited actions. Use before any QA, bug hunt, regression, or release-gate test of a web app, API, workflow, or agent.
---
# QA Preflight Manifest

## Procedure
1. Copy `templates/run-manifest.yaml` to `runs/<run-id>/manifest.yaml`.
2. Fingerprint the live target: version endpoint, `<meta>` build tags, hashed JS bundle names, response headers (`x-vercel-id`, `server`, `etag`), workflow version IDs, and DB migration version. Record expected and observed values. If they differ, stop and report a drift warning.
3. Inventory access per role (customer A, customer B, admin, signed-out). Test each login now. A missing account makes its cases BLOCKED.
4. List available and unavailable tools: browser engines, real iOS device, DB read access, provider dashboards (Stripe, email, Ghost, n8n), logs, CLIs.
5. Confirm the mode (read_only / staging_mutation / authorized_production_smoke) and list every action that needs a separate approval.
6. Set budgets: minutes, workers, requests per second, spend, and retries.
7. Create `PROGRESS.md`, `ledger.csv`, `cleanup.csv`, and `evidence/`.

## Exit criteria
- All required manifest fields are filled, or the run is reported BLOCKED with the reason.
- The build fingerprint is captured from the running system.
- The approvals list has been sent to the human if it is non-empty.

## Pitfalls
- Fingerprinting the repo instead of what is deployed (see pattern E1).
- Treating an earlier approval as covering new recipients, amounts, or environments.
