---
name: qa-bug-reporting
description: Write, dedupe, and rank defect records with minimal repro steps, expected-versus-actual results, sanitized evidence, reproducibility counts, and root-cause confidence. Use whenever a test fails or an anomaly is found.
---
# Bug Reporting

## Procedure
1. Reproduce at least twice from a clean state. Record failures over attempts.
2. Minimize the steps to the shortest path that still fails.
3. Fill `templates/bug-report.md`. The title states the wrong outcome ("Repeat audits by signed-in members never start"), not the component.
4. Attach sanitized evidence: screenshot, trace, response, and run ID. Redact tokens, cookies, emails, and keys.
5. Root cause: mark CONFIRMED only with a code or log trace. Otherwise SUSPECTED or UNKNOWN.
6. Reachability: confirm the code path is live in this build (pattern F4).
7. Dedupe: one record per distinct root cause, with symptoms linked.
8. Rank by severity, then customer reach.

## Exit criteria
Every FAIL in the matrix links to a bug record or a test-defect record.
