---
name: fix-async-workflows
description: Fix background jobs, queues, cron, n8n/Windmill workflows, webhooks, and email delivery: remove swallowed errors, make writes verifiable, fix execution order, add bounded idempotent retries, and reconcile live workflows with the repo. Use for any asynchronous or workflow-engine defect.
---
# Fix Async and Workflow Bugs

## Procedure
1. Fix the LIVE workflow, then export it to the repo (or the reverse) so they match; record version IDs before and after.
2. Remove never-error, continue-on-fail, and always-output on writes. Read back every write and fail loudly if it's missing.
3. Make execution order explicit (sequential connections), not dependent on canvas position.
4. Validate expressions in a throwaway workflow before deploying.
5. Retries: bounded, idempotent, logged, and only for transient external faults. Never use retries to hide nondeterminism.
6. Resume after restart: jobs continue or fail visibly; no duplicates.
7. Email: confirm delivery in a test inbox and canonical links; never report "sent" from the sender's response alone.
8. One correlation ID through every stage.

## Exit criteria
A real run ID shows every stage writing its output, repeated triggers create no duplicates, and the live workflow matches the repo.

Counterpart of tester skill: `qa-async-workflows`.
