---
name: fix-accessibility
description: Fix accessibility defects to WCAG 2.2 AA — missing labels, invisible focus, keyboard traps, contrast, alt text, announcements, reflow — using native semantics first, then verify with axe plus manual keyboard and screen-reader checks. Use for any accessibility finding.
---
# Fix Accessibility

## Procedure
1. Prefer native elements: `<button>`, `<label for>`, `<a href>` over ARIA patches.
2. Labels: every input gets a real label; a placeholder is not a label.
3. Focus: a visible `:focus-visible` style, logical order, no traps, Escape closes dialogs, focus returns to the trigger.
4. Images: meaningful `alt`; decorative images use `alt=""`.
5. Contrast and reflow: AA contrast in all themes, usable at 200% zoom and 320px width.
6. Errors and status: tie messages with `aria-describedby`; use `role="status"` for live updates.
7. Verify: axe (no serious or critical issues) plus a keyboard-only run of the journey; VoiceOver spot check if available.

## Exit criteria
axe is clean, and the manual keyboard checklist is recorded for every touched route.

Counterpart of tester skill: `qa-accessibility`.
