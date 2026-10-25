---
name: fix-preflight-manifest
description: Start every fixing run by filling a fix manifest: repository and base commit, live build fingerprint, write scope and protected test paths, environments, approvals, and budgets. Use before changing any code in response to bug reports.
---
# Fix Preflight Manifest

## Procedure
1. Copy `templates/fix-manifest.yaml` into `fixes/<run-id>/manifest.yaml`.
2. Record the repository, the base branch, and the base commit. Fingerprint the live target (version endpoint, asset hashes, workflow versions) and compare it with the base commit. If they differ, report drift before fixing anything.
3. Write scope: application code and config only. List the protected paths you may not edit (tester tests, fixtures, snapshots, CI, graders, the Done-Gate tools). Confirm the token or branch protection enforces this; if it can't, say so in the manifest.
4. Environments: where you may run the app (local, staging), the production config values to mirror (`NODE_ENV`, flags), and where fixes get deployed for verification.
5. Approvals needed: production deploys, production data repair, secret rotation, policy changes (price, refund, access rules). List them now and batch the request.
6. Budgets: time, retries per bug (3 failed theories → escalate), and spend.
7. Create `PROGRESS.md` and `fix-ledger.csv`.

## Exit criteria
The manifest is complete, protected paths are listed and enforced (or the gap is reported), and the approval list is sent if non-empty.

Counterpart of tester skill: `qa-preflight-manifest`.
