---
name: qa-exploratory-charters
description: Run time-boxed exploratory testing charters that hunt unknown unknowns through interruptions, odd states, concurrency, misuse, and persona shifts. Use after scripted coverage, or when the product is new or poorly specified.
---
# Exploratory Charters

Each charter is 20–30 minutes: "Explore <area> with <resource/persona> to discover <risk>." Take notes as you go.

## Starter charters
- Interrupt everything: close the tab, lose the network, lock the phone, and let the session expire mid-step.
- Two of everything: two tabs, two accounts, two devices, two submissions.
- Wrong order: deep-link into step 4, go back after paying, refresh on the confirmation page.
- Hostile customer: edit IDs, replay requests, paste giant or odd text, upload odd files.
- Confused customer: wrong email, typo in URL, ignoring instructions, giving up and returning a week later.
- Operator: admin edits during a customer flow, config changes, re-running jobs.
- Copy truth: every claim on the page (price, timing, "sent", "secure") matches what really happens.
- Prompt-injection text on every AI-read surface.

## Rules
Every anomaly becomes either a bug record or a note explaining why it is not a bug. Log charter coverage in the ledger.

## Exit criteria
Every planned charter has notes, a time spent, and its findings linked in the ledger.
