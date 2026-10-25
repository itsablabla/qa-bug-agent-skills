---
name: done-gate-report
description: Write status and completion reports that can never overstate what is done — limits first, every completion line tied to an item ID and its exact verifier verdict, copied numbers, named environments — and self-check them with the allow-list auditor before sending. Use for every final answer, status update, PR description, or handoff that reports work.
---
# Done-Gate: Report Honestly

## Required shape (status section)
```
Not verified: <IDs or "None">
Blocked: <what could not run, or "None">
Not run: <planned checks skipped, or "None">
Not deployed: <yes/no + where>
<ID>: <VERIFIED | NOT VERIFIED | NOT FIXED | PARTIALLY FIXED | IMPLEMENTED | PROPOSED> (<evidence ref>)
Next: <what would verify the rest>
```

## Allowed status statements (everything else is an unproven claim)
1. An item ID with its exact verdict from the verifier ledger.
2. A limit: not tested, not verified, blocked, not deployed, still failing, waiting for.
3. A plan, a condition, or a question: "Next…", "If…", "Do you want…?".
4. Numbers copied from the ledger, matching exactly.
5. An unnamed summary such as "All good" only when every item in scope is VERIFIED, and readiness wording only when nothing is blocked and the build is deployed.

## Never
- Hedged success ("should fix", "probably works").
- Paraphrased completion without an ID ("taken care of", "the bug is gone", "customers can now…").
- Self-set VERIFIED.
- Engines, devices, or environments that did not run (Safari, mobile, production).

## Self-check before sending
`python3 tools/claim_audit.py --report report.md --facts ledger_facts.json` must return no flags. If it flags a line, rewrite the line from the ledger; do not argue with the checker.

## Exit criteria
The report has the required shape and zero auditor flags.
