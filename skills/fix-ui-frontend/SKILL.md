---
name: fix-ui-frontend
description: Fix UI, layout, cross-browser, mobile, console-error, and broken-asset bugs at their cause, verified across the same viewport and engine matrix the tester used. Use for visual, responsive, Safari, touch, image, or front-end crash bugs.
---
# Fix UI and Front-End Bugs

## Procedure
1. Reproduce on the reported engine and viewport (360, 390, 768, 1280). Note if only real Safari shows it; Chromium results don't count for Safari bugs.
2. Common causes and correct fixes:
   - Horizontal overflow → remove fixed widths ≥ 400px, add `max-width:100%`, `flex-wrap`, `overflow-wrap:anywhere` for user text. Measure against `clientWidth`, not `innerWidth`.
   - Image never loads → lazy image in a transformed or off-screen container; fix the container or loading strategy, serve missing assets with dimensions.
   - Console crash → parse types at the boundary (JSON turns dates into strings); handle failed responses before using them.
   - Touch gestures ignored → native listeners with `{ passive: false }`.
   - Duplicate IDs or hidden focusable elements → unmount hidden variants.
   - Fonts or modals wrong after a refactor → check loaded fonts and initial overlay state.
3. Don't hide errors with CSS or try/catch around rendering.
4. Re-run the tester's full UI sweep for the route on every viewport, and check neighbors that share the component.

## Exit criteria
The reported engine and viewport pass, the full route sweep is clean on all viewports, and Safari-only bugs are marked BLOCKED if no real Safari is available.

Counterpart of tester skill: `qa-browser-ui`.
