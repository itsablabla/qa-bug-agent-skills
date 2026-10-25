---
name: fix-intake-triage
description: Take bug records from the tester, reject incomplete ones, group them into root-cause clusters, and order the repair queue by severity, unblocking value, and blast radius. Use at the start of a fixing run or whenever new bug records arrive.
---
# Fix Intake and Triage

## Procedure
1. Check every record has steps, an expected result tied to a requirement, evidence, a build fingerprint, a reproduction count, and a failing regression test. Return incomplete records to the tester as INCOMPLETE-RECORD; do not guess.
2. Cluster by root cause, not symptom: the same function, the same missing control (ownership check, redirect guard, idempotency store, serializer), or the same data flow. Three open redirects form one cluster with one shared helper.
3. Unblockers first: bugs that make other tester results INCONCLUSIVE (console crashes, flaky endpoints, broken login).
4. Order: P0 → unblockers → P1 → P2 → P3; within a level, smaller blast radius and higher customer reach first.
5. Attach the matching entry from the Fix Recipe Library to each cluster.
6. Mark clusters needing a human decision (policy, production data, deploys).

## Exit criteria
A triage table: cluster | bug IDs | severity | unblocks | recipe | approval needed | order.

Counterpart of tester skill: `qa-bug-reporting`.
