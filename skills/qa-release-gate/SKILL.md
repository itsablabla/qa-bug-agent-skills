---
name: qa-release-gate
description: Make the final release verdict, reconcile cleanup of test data, and produce the QA handoff report. Use at the end of every test run or before any production promotion.
---
# Release Gate

## Procedure
1. Make sure every matrix row has a final status. Any NOT RUN, FLAKY, INCONCLUSIVE, or BLOCKED on a critical case blocks READY.
2. Lint the evidence: every evidence path in the ledger exists and is non-empty.
3. Sanitize: redact cookies, tokens, and personal data in HAR, trace, and screenshot files before sharing.
4. Apply the verdict rules from the master instructions (READY / CONDITIONALLY READY / NOT READY).
5. Confirm the critical journey is verified on the deployed build across the device matrix, including real iOS Safari where required.
6. Cleanup: delete run-tagged records, verify leftovers by tag count, reconcile `cleanup.csv`, and list anything remaining.
7. Fill `templates/final-handoff.md`, including Not Covered, Assumptions, Corrections, and New Patterns.
8. Append new patterns to `01-BUG-PATTERN-LIBRARY.md`.
9. Production promotion remains a separate human approval.

## Exit criteria
The handoff report is delivered and the cleanup ledger is reconciled.
