---
name: fix-journey-e2e
description: Restore a broken customer journey so the real end outcome happens — the record is created and owned, the email arrives, the entitlement is granted — not just the visible signal. Use for signup, intake, progress, checkout, delivery, and any 'button does nothing / says success but nothing happened' bug.
---
# Fix the Journey, Not the Message

## Procedure
1. Write the journey's required end state from the requirement (for example: "Run again" creates a new owned audit and opens its progress page).
2. Find where the chain breaks: missing route, unchecked `fetch` response, fake progress timer, unpersisted write, wrong ID passed forward.
3. Fix so the outcome happens, and surface errors in plain language when it can't.
4. Avoid incomplete fixes seen in our lab: an endpoint returning 200 without creating anything; returning an old ID; a button showing "coming soon"; a page that changes but delivers nothing.
5. Check continuity: refresh, new session, back button, double submit, and closing the tab mid-way.
6. Check copy truth: prices, timings, and claims on the page match the requirement (one constant, not literals).

## Exit criteria
The tester's journey test and the hidden outcome tests pass, with the end state proven through an independent read (database, admin count, provider).

Counterpart of tester skill: `qa-journey-e2e`.
