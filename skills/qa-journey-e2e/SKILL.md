---
name: qa-journey-e2e
description: Execute critical customer journeys end to end through the real UI, then verify persisted state, downstream effects, and continuity in a fresh session. Use for signup, onboarding, core value creation, checkout, delivery, and any "does it actually work" question.
---
# End-to-End Journey Verification

## Procedure (per journey, per required device)
1. Known start state: a fresh account or a cleaned fixture tagged with the run ID.
2. Perform each step in the UI, with a screenshot and the network request/response per step.
3. After each state-changing step, verify the persisted state through an authorized read (DB, admin API, provider dashboard).
4. Verify downstream effects: email in the test inbox, webhook received, file in storage, entitlement granted, charge in TEST mode for the right amount and currency.
5. Check continuity: reload, open a new browser profile, sign out and back in, and return later. Everything should reappear correctly.
6. Check isolation: account B cannot see A's objects.
7. Run the variants: returning signed-in user, double submit, closing the tab mid-process and reopening, back button after payment.

## Copy truth
Compare every displayed price, currency, timing promise ("results in 7 minutes"), and claim ("secure", "sent") with the requirements and the real behavior. A wrong displayed price is P1 even if checkout charges correctly. Round 3 seeded a $9.90 button against a $99 requirement, and the frozen tester missed it.

## Evidence
A journey trace table: step | action | screenshot | request | persisted proof | downstream proof | status.

## Exit criteria
The journey is PASS only when every step's end state is proven. Otherwise, record the exact failing step.

## Pitfalls
- Stopping at "the request returned 200".
- Testing only the first-time path (pattern A1).
- A test mode mismatch: confirm the payment account and mode before checkout.
