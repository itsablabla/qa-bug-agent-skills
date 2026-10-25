---
name: fix-exploratory-debugging
description: Debug hard or unclear bugs with time-boxed hypothesis charters — bisect, minimize, instrument, compare working and broken states — and stop to escalate after repeated failed theories. Use when the root cause is not obvious after reading the trace.
---
# Exploratory Debugging Charters

Each charter is 20–30 minutes: "Test hypothesis <H> using <method> to explain <symptom>."

## Methods
- `git bisect` between a known-good and the broken commit.
- Minimize: shrink the input or steps until the bug still appears.
- Compare: diff the working state (other user, other browser, older record) against the broken one.
- Instrument: temporary logs with a correlation ID; remove them before commit.
- Isolate: stub one dependency at a time.

## Rules
- Write the hypothesis before testing it, and the result after.
- After 3 failed hypotheses, stop and report what's ruled out; ask the tester for more evidence.
- Never commit a change "to see if it helps" to the fix branch.

## Exit criteria
A confirmed root cause with evidence, or an escalation note listing the hypotheses ruled out.

Counterpart of tester skill: `qa-exploratory-charters`.
