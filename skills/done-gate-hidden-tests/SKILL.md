---
name: done-gate-hidden-tests
description: Write tester-private hidden acceptance tests that a fixer cannot fit or game — random data, both directions, real-browser identity, outcome and isolation assertions, verifier-controlled clock, independent observation channels, and instrument self-tests. Use when creating acceptance tests for any bug or feature that an AI agent will fix.
---
# Done-Gate: Hidden Tests That Can't Be Fitted

## Rules (each one exists because a cheat got past without it)
| Rule | Cheat it stops |
|---|---|
| Random data every run; no fixed prefix | Hard-coded test data (S02) |
| Every direction and role (A→B, B→A, signed out) | One-direction fix (S12) |
| Real browser user-agent and a second channel (page plus API) | Test-environment sniffing (S20) |
| Assert the outcome: a file with the record, a new owned ID, a count +1 | Cosmetic fix (S09), fake ID (S33), no-persist (S08) |
| Assert isolation: what must NOT change | Over-broad fix (S11) |
| Count through an independent channel (admin or tag count) | Hiding duplicates from the list (S22) |
| Verifier clock ages records; a canary proves the clock moved | Fresh-data window (S21) |
| Test the API layer, not just the button | Client-only fix (S03) |
| Repeat; 1,000 calls for stability claims | Rare flakes (S10, S35) |
| Keep them out of the fixer's repo and context | Test fitting in general |

## Every new instrument gets a self-test
In Round 2 the clock control looked done but did nothing, because the clock file was never passed to the app. The canary test (`ho-clock-canary`) caught it.

## Exit criteria
Each hidden test fails on the buggy base and passes on a genuine fix (proven on at least one control), and the instrument canaries pass.
