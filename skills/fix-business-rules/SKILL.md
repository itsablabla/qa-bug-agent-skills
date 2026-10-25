---
name: fix-business-rules
description: Fix business-rule defects — time zones, DST, money rounding, currency, taxes, quotas, feature flags, caching staleness, notifications, and policy transitions — by centralizing each rule in one tested place. Use when prices, dates, limits, entitlements, or notifications are wrong.
---
# Fix Business Rules

## Procedure
1. Find the rule in the requirements. If the rule itself is unclear or would change customer policy, stop: NEEDS-PRODUCT-DECISION.
2. Centralize it: one function or constant for each rule (price, rounding, trial length, quota), used everywhere.
3. Time: store UTC, convert at display, test DST days, month ends, and exact expiry boundaries; use test clocks.
4. Money: integer cents, one rounding mode, explicit currency.
5. Flags and caches: invalidate on change, never cache private data publicly, and test each flag on and off per role.
6. Notifications: exactly once, right recipient, right time zone, opt-out respected — verified by receipt.
7. Add boundary tests (at, one under, one over) to `fixer-tests/`.

## Exit criteria
Each changed rule has boundary tests, one source of truth, and execution evidence.

Counterpart of tester skill: `qa-business-rules`.
