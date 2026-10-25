---
name: fix-deploy-rollback
description: Get a fix onto the build the verifier will test, with matching fingerprints, production config, migrations applied safely, and a rehearsed rollback; never deploy to production without approval. Use when a fix needs deploying for verification or release.
---
# Deploy and Rollback

## Procedure
1. The claimed commit must be the branch head. Never claim an older commit while the head contains other changes.
2. Deploy to the verification target (staging) within scope; record the deployed fingerprint and confirm it matches the head.
3. Run with production config values; a fix that only works outside production isn't a fix.
4. Migrations: apply on a copy first, check counts and checksums, have a down-migration or restore.
5. Rollback: rehearse reverting to the previous build in staging and confirm the app works and new data stays readable.
6. Read effective config inside the running service after deploy.
7. Production promotion is a separate human approval.

## Exit criteria
Deployed fingerprint = branch head = claimed commit, rollback rehearsed (or BLOCKED with the risk named), production untouched without approval.

Counterpart of tester skill: `qa-deploy-migration-rollback`.
