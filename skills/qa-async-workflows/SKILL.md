---
name: qa-async-workflows
description: Test background jobs, queues, cron, workflow engines (n8n, Windmill, Sim), and email delivery for execution order, swallowed errors, retries, idempotency, drift between repo and live, and observability. Use when any part of a journey runs asynchronously.
---
# Async Workflows and Integrations

## Procedure
1. Inventory from the LIVE engine: active workflows, version IDs, triggers, webhook paths, credentials (names only), and error workflows. Diff against the repo (pattern E1).
2. Find swallowed errors: continue-on-fail, never-error, empty catch, or `alwaysOutputData`. Each write must be read back (pattern A2).
3. Trace one real run through every node with run data. Compare the actual order with the intended order (pattern B1).
4. Expression and code nodes: validate syntax in a throwaway workflow before trusting it.
5. Failures: kill a dependency, time out an API, and return malformed data. The customer-visible state should explain the failure and retry safely.
6. Idempotency: trigger twice and retry after a partial failure. Expect no duplicate reports, emails, or charges.
7. Restart the worker or engine mid-run. The job resumes or fails visibly (pattern B3).
8. Email: the message arrives in a test inbox, links use the canonical domain, unsubscribe works, and SPF/DKIM/DMARC pass.
9. Correlation: one ID connects intake → processing → delivery in the logs.

## Exit criteria
Each workflow stage has run IDs as evidence and a verified output row or artifact.
