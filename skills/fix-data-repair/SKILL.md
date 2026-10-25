---
name: fix-data-repair
description: Repair data damaged by a bug — duplicates, wrong grants, orphans, unowned records, stale caches — with dry-run counts, backups, idempotent reversible scripts, and human approval for production. Use when root-cause analysis shows a bug may have written bad data.
---
# Data Repair

## Procedure
1. Define the damage query and how you know a row is wrong.
2. Dry run: counts and a sanitized sample (no personal data).
3. Script: back up affected rows first, then repair. It must be idempotent (safe to rerun) and reversible.
4. Staging: run it, compare counts before and after, rerun to prove idempotency.
5. Production: request approval with the script, counts, and backup location. Never run it without a yes.
6. Record customer impact (who got wrong access or charges) for an owner decision on communication.
7. Verify by re-running the damage query: zero rows.

## Exit criteria
Before/after counts, a backup reference, and a zero-row damage query, or a pending approval request.

Counterpart of tester skill: `qa-data-integrity`.
