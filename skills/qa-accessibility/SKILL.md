---
name: qa-accessibility
description: Test WCAG 2.2 AA accessibility with axe-core plus manual keyboard, focus, screen-reader, contrast, and zoom checks. Use for any customer-facing UI.
---
# Accessibility

Automated scans catch only part of the problem: [axe-core finds about 57% of WCAG issues](https://github.com/dequelabs/axe-core). Manual checks are required.

## Procedure
1. Run axe-core with WCAG 2.0, 2.1, and 2.2 A/AA tags on every route and state (open dialogs, errors shown). Review results marked "incomplete".
2. Keyboard-only primary journey: logical tab order, visible focus (search the CSS for `:focus-visible`, see pattern D7), no traps, Escape closes dialogs.
3. Screen reader spot check (VoiceOver on iOS/macOS): headings, landmarks, button names, and announced form errors.
4. Contrast in light and dark themes, zoom to 200% and 400% reflow, and a 320px width.
5. Forms: real labels (axe-core accepts a placeholder as the accessible name, so check labels separately), autocomplete attributes, and error text tied with aria-describedby.
6. Motion: respect `prefers-reduced-motion`.

## Exit criteria
No serious or critical axe violations, and the manual checklist is recorded per route.
