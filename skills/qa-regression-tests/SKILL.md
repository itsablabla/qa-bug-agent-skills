---
name: qa-regression-tests
description: Convert every confirmed bug into the smallest failing automated test before any fix, and keep tests protected from being weakened. Use when a bug is confirmed or when building a regression suite.
---
# Regression Tests (failing test first)

## Procedure
1. Write the smallest test that fails for the observed reason on the current build. Name it `area.behavior_expected`.
2. Run it and confirm it fails with the right assertion, not a setup error.
3. Choose the right layer: unit for logic, API for contracts, Playwright for UI, and a workflow fixture for async.
4. Assert outcomes (persisted state, visible result), not implementation details.
5. Commit it to the protected test directory and hand it to the repair agent.

## Protection rules
- The repair agent cannot edit tests, fixtures, snapshots, or CI config. Any diff touching them is flagged.
- No `skip`, `only`, loosened tolerance, or changed expected value without a reviewed test-defect record.
- AI "healing" of locators or waits must keep the original behavioral assertion. A reviewer approves it.

## Exit criteria
The test fails before the fix and passes after it on the deployed build, verified independently.
