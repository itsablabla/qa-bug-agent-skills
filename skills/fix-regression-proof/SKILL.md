---
name: fix-regression-proof
description: Prove each fix with the five self-checks — tester test fails on base, passes on the fix, fails again with only the fix reverted, full suite and guards green, no protected files touched — plus fixer-owned extra tests, and save the evidence for the verifier. Use before handing any fix to the verifier.
---
# Regression Proof (self-check, not certification)

## Five proofs
1. Base fails: the tester's test fails on the base commit (from `fix-reproduce`).
2. Fix passes: it passes on the fix commit — and at the branch head that will actually ship.
3. Fix-removal: with only this fix reverted, it fails again. If it still passes, the test doesn't exercise your fix; investigate before claiming.
4. No collateral: the full tester suite, adjacent guards, and the Fixer guards are clean.
5. Integrity: `git diff --name-only base..head` contains no protected path.

## Extra
- Add fixer-owned tests in `fixer-tests/` for contracts and edge cases. They never replace tester tests.
- If the tester's public test can't tell bug from fix (passes on base), file TEST-DEFECT and point to the discriminating test.
- Run `tools/fix_loop.py` (or the CI job) to produce `evidence/<cluster>-selfcheck.json`.

## Exit criteria
All five proofs recorded; any failure blocks handoff.

Counterpart of tester skill: `qa-independent-verification` (the fixer self-checks; only the verifier certifies).
