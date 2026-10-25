---
name: qa-independent-verification
description: Independently verify a claimed fix from a fresh context with no write access, retesting the exact deployed build, the original failure, and adjacent journeys. Use whenever someone or some agent says a bug is fixed or a feature is done.
---
# Independent Verification

## Inputs
Only the bug record, the target build fingerprint, and the evidence. Do not read the repair agent's reasoning.

## Procedure
1. Confirm the deployed build matches the claimed fix version. If it is not deployed, the status is FIXED IN DRAFT – DEPLOYED RETEST PENDING.
2. Repeat the original reproduction steps exactly, on the original device.
3. Run the regression test and confirm it was not weakened or edited to pass (diff against the version committed with the bug record).
4. Fix-removal check: run the same test against the build without the fix (or with the fix reverted). It must FAIL. A test that passes both ways proves nothing.
5. Test adjacent journeys: the same feature with other roles, devices, and states, and anything sharing the changed code.
6. Look for new side effects: console errors, performance, and data.
7. Verdict: VERIFIED, NOT FIXED, or PARTIALLY FIXED, with evidence.

## Rule
Ask: would this evidence look different if the fix were not there? If not, gather better evidence.

## Exit criteria
All five checks are recorded (fingerprint, original repro, regression test unchanged, fails with the fix reverted, adjacent journeys), each with evidence, and the verdict is stated.
