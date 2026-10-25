---
name: qa-test-the-tester
description: Measure the bug tester's and test suite's real detection power with seeded bugs, mutation testing, and recall scoring. Use when adopting the tester, after changing its instructions, or periodically.
---
# Test the Tester

## Procedure
1. Seeded-bug benchmark: in staging, plant 10–20 known bugs drawn from the pattern library (swallowed 404, IDOR, mobile overflow, duplicate webhook, lazy image, paid-content leak, and so on). Run the tester blind and score recall (found/planted), false positives, and time to find.
2. Mutation testing on the suite (Stryker for JS/TS/.NET, mutmut for Python). Survived mutants show weak assertions ([how to read results](https://learn.microsoft.com/en-us/dotnet/core/testing/mutation-testing)).
3. Honesty audit: sample PASS results and check that each has openable evidence that would differ if the feature were broken.
4. Gaming audit: check whether any test or expected value was changed during repair.
5. Track recall per category over time. Update instructions where recall is low, then rerun.

## Exit criteria
A scorecard with recall per category, mutation score, honesty-audit results, and instruction changes made.

## Multi-round improvement (required after changing the kit)
Run three rounds. Each round:
1. Test the entire thing: kitcheck on the documents, plus the harness against the benchmark at the current difficulty.
2. Write an improvement plan from every miss, false positive, and failed check.
3. Implement the plan.
4. Rerun all earlier rounds' suites as well as the new one, so later fixes cannot break earlier ones.
Raise the difficulty each round: harder seeded bugs, then attacks on the tester itself (weakened tests, undeployed fixes, prompt injection, fake evidence, unsanitized traces).

## Escaped bugs
Every bug found after release becomes a pattern-library entry and a seeded bug in the benchmark before the next run.
