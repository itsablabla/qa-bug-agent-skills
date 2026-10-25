---
name: fix-learn-guards
description: Turn every verified fix into durable prevention — recipe library entry, shared helper or guard rule that fails CI on the bug class, a new static-scan rule and seeded bug for the tester — and prove the guard catches a fresh instance. Use after each VERIFIED verdict and at the end of each run.
---
# Learn and Guard

## Procedure
1. Add the recipe: class, root cause, correct fix, wrong fixes seen, tests, guard.
2. Build the strongest guard that fits: a shared helper or middleware (the right way becomes the easy way), a lint/semgrep rule, or a type that makes the bad state impossible.
3. Prove the guard: add a fresh instance of the class on a scratch branch; the guard must flag it. In our lab one guard could never fire until this test exposed it.
4. Give the tester the rule for its static scan and a seeded bug for its benchmark.
5. Track recurrence per class across runs; a recurring class means the guard is too weak.
6. Calibrate the fixer itself: run it on the seeded false-done benchmark after changing its instructions; the target is zero fake "done" claims.

## Exit criteria
Library updated, the guard catches a fresh instance (evidence saved), and the tester has the new rule and seeded bug.

Counterpart of tester skill: `qa-test-the-tester`.
