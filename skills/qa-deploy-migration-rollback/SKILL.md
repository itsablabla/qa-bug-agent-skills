---
name: qa-deploy-migration-rollback
description: Verify deployments, database migrations, rollback, environment config, and drift between the repo and the live system. Use before and after any release, schema change, or infrastructure change.
---
# Deploy, Migration, and Rollback

## Procedure
1. Fingerprint before and after deploy: build ID, commit, asset hashes, workflow versions, migration version.
2. Drift: compare live routes, webhooks, workflows, env var names, and feature flags with the repo. Live state wins; record each difference.
3. Migration on a copy: row counts and checksums before and after; constraints valid; down-migration or restore tested.
4. Rollback rehearsal (staging): deploy N, roll back to N-1, confirm the app works and data written by N is still readable. If not possible, mark BLOCKED and record the risk.
5. Config: read the effective config inside the running service, not the file you uploaded (pattern E3).
6. Smoke the critical journey after deploy and after rollback.

## Exit criteria
Fingerprints recorded, drift list complete, and rollback rehearsed (or BLOCKED with the risk named).
