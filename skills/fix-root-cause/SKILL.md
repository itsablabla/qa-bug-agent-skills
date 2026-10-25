---
name: fix-root-cause
description: Find the true root cause of a reproduced bug by tracing the full data and control path, asking why until reaching the decision that created the bad state, and checking history. Use after reproducing and before planning any fix.
---
# Root Cause

## Procedure
1. Trace end to end: UI event → request → handler → data write → response → render. Mark each trust boundary crossed.
2. Ask "why" until you reach a decision in code or config, not a symptom.
3. Classify: missing control, wrong layer (client enforcing a server rule), swallowed error, wrong contract (status codes, types, fields), state or ordering, config or drift, content or copy, dependency.
4. Check history: `git log -L` / `git blame` on the lines, related issues, and whether an earlier fix regressed.
5. Write one sentence with file:line and confidence (CONFIRMED with a trace, or SUSPECTED).
6. Note whether bad data may already exist, which triggers `fix-data-repair`.
7. If 3 theories fail, stop and write what you ruled out; ask the tester for more evidence instead of stacking guesses.

## Exit criteria
A root-cause statement with class, file:line, confidence, and a yes/no on data impact.

Core fixer skill; pairs with tester skill `qa-recon-risk-map` (the tester maps risk, the fixer maps cause).
