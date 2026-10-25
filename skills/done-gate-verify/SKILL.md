---
name: done-gate-verify
description: Independently decide whether a claimed fix or finished task is actually done, using re-derived facts, hidden tests, statistics, soak, production config, latency budgets, and new-route inventory. Use whenever any agent or person says something is fixed, done, working, deployed, or ready.
---
# Done-Gate: Verify a "Done" Claim

You are the only role allowed to set VERIFIED. You have no write access to the code.

## Re-derive, never trust
1. Ship target = the branch head. The claimed commit and the deployed build must both equal it. Otherwise the verdict is NOT VERIFIED – CLAIMED COMMIT IS NOT WHAT SHIPS, or FIXED IN DRAFT – DEPLOYED RETEST PENDING.
2. Bug tests come from the bug record; test files come from the Tester's ref. Ignore the claim's test list and its self-check.
3. Confirm on your own that the bug exists on the base. If the public test passes on the base, flag TEST_DEFECT to the Tester and judge with the hidden tests that do fail.

## Run (all on the deployed build, under production config)
| Check | Rule |
|---|---|
| Bug tests | Pass 3 of 3 |
| Full public suite | Passes twice |
| Hidden tests | Pass: random data, real-browser user-agent, both directions, outcome and side-effect asserts, aged records using the verifier clock (the canary must pass) |
| Fix removal | The discriminating tests fail with only this fix reverted |
| Stability | 1,000 calls with 0 failures; to claim a failure rate below 1 in N you need about 3N clean calls |
| Soak | Rerun hidden and bug tests after 3,000 realistic requests |
| Latency | Deployed p95 ≤ max(2× base p95, base p95 + 100 ms) |
| New routes | Every route added since the base is probed signed-out and cross-user; any leak fails |
| Words | `claim_audit.py` on the claim fields and the report (allow-list) |

## Verdicts
VERIFIED · NOT FIXED · NOT VERIFIED · PARTIALLY FIXED · FIXED IN DRAFT – DEPLOYED RETEST PENDING · NOT VERIFIED – CLAIMED COMMIT IS NOT WHAT SHIPS · INCONCLUSIVE – TEST CANNOT DISTINGUISH BUG. Honesty flags are listed first.

## Before reporting a failure, reproduce it a second way
In Round 1 our own hidden test produced a false failure (the client stalled). Plain `curl` exposed it.

## Exit criteria
A verdict JSON with every check, the evidence paths, and flags; nothing left out.
