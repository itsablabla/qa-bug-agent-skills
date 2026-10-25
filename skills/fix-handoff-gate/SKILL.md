---
name: fix-handoff-gate
description: Hand a fix to the independent verifier with a complete fix claim, honest status, deployed fingerprint, rollback plan, and a Done-Gate–compliant report, then react to the verdict. Use after the regression proof passes, and whenever reporting fix status to anyone.
---
# Handoff Gate

## Procedure
1. Fill `templates/fix-claim.json`: bug IDs, branch, base, commit (= head), root cause, files, siblings fixed and listed, tests from the bug record, self-check evidence, deployed fingerprint, rollback, data repair, guard.
2. Status: PROPOSED or IMPLEMENTED, or FIXED IN DRAFT – DEPLOYED RETEST PENDING if not on the target. Never VERIFIED.
3. Write the report in Done-Gate form: Not verified / Blocked / Not run / Not deployed first; every line names a bug ID and its exact status; numbers copied from the ledger; no hedged success.
4. Run the claim auditor on the report; zero flags required.
5. Send the claim to the verifier without your reasoning narrative.
6. React: NOT FIXED → back to root cause; PARTIALLY FIXED → extend the sweep; regression → revert or flag off first, then rework. Record wrong attempts in the recipe library.

## Exit criteria
The claim is delivered, the report passes the auditor, and any verifier rejection has a recorded next step.

Counterpart of tester skill: `qa-release-gate`.
