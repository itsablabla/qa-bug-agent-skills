---
name: qa-data-integrity
description: Verify persistence, constraints, migrations, duplicates, orphans, and cleanup of test data. Use when testing anything that writes data or after schema changes and deploys.
---
# Data Integrity

## Procedure
1. For each write in a journey, read the row back and check owner, status, timestamps (with timezone), and foreign keys.
2. Constraints: uniqueness under concurrent requests, and no null in required fields.
3. Orphans: runs without owners, payments without orders, and files without records (pattern G1).
4. Migrations: apply on a copy, check row counts and checksums before and after, and check rollback.
5. Retention: paid and active records are protected from cleanup jobs.
6. Cleanup: delete only rows tagged with the run ID. Log every deletion and every failure in `cleanup.csv`.
7. Verify cleanup: query or count leftover records by tag after deleting. A 200 response from DELETE is not proof.

## Exit criteria
Integrity queries return zero violations, and the cleanup ledger is reconciled.
