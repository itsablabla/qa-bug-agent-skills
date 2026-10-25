---
name: qa-browser-ui
description: Test web UI across Chromium, Firefox, WebKit, mobile viewports, and real iOS Safari, capturing console errors, failed requests, layout overflow, broken images, and visual defects with screenshots and traces. Use for any UI, smoke, cross-browser, mobile, or visual testing.
---
# Browser and UI Testing

## Setup
- Playwright projects: desktop chromium/firefox/webkit at 1280, iPhone (webkit, 390), and Pixel (chromium, 360). Turn on trace `on-first-retry` or `on`, plus video and HAR.
- Use real iOS Safari (device or device cloud) for checkout, auth, file upload, media, gestures, and anything Safari-sensitive.
- If an engine cannot be installed (for example, Playwright WebKit and Firefox are unsupported on some Linux images), log it as BLOCKED with a fallback (the owner's Mac Safari through the local browser, or a device cloud). Never substitute Chromium results.

## Per-route checks (automate them)
1. Console: zero errors, and every warning reviewed.
2. Network: no unexpected 4xx/5xx, no mixed content, no CORS failures. Check every API response's `ok` field.
3. Overflow: `document.documentElement.scrollWidth <= document.documentElement.clientWidth` (or `visualViewport.width`). Never compare with `innerWidth`: in mobile emulation it grows to fit the content and hides the bug (found in Round 1).
4. Images: after a full scroll, every `img.complete && img.naturalWidth > 0` (pattern D1).
5. Fonts: `document.fonts` shows the intended families loaded (pattern D5).
6. Duplicate `id` and `data-testid` values (pattern D4).
7. Screenshot each route on each device, plus a full-page capture.
8. Structure: `toMatchAriaSnapshot` for key regions.
9. Labels: every input has a `<label>`, `aria-label`, or `aria-labelledby`. A placeholder is not a label.
10. If a page had 5xx responses, reload up to 3 times and record the flaky count; if it never loads cleanly, mark that route's content checks INCONCLUSIVE.
11. If a console error or failed request happened on the page, mark downstream checks on that page INCONCLUSIVE until rerun on an isolated state.

## Interaction checks
- Click every visible button, link, and chip, and confirm each does something (pattern: chips with no handler).
- Keyboard-only path, focus visibility, Escape closes dialogs, and the back button behaves.
- Touch: swipe, pull-to-refresh, and long-press on a touch device; watch for passive-listener warnings (pattern D2).
- On-screen keyboard covering inputs (mobile), and orientation change.
- Slow network (Fast 3G) and offline: spinners resolve and errors are shown.

## Evidence
`evidence/<case>/<device>.png`, `trace.zip`, `console.json`, `network.har`.

## Exit criteria
Every route × device cell has a status and evidence. A visual defect counts as FAIL even if the function works.
