---
name: qa-business-rules
description: Test business-rule correctness: time zones and DST, money and rounding, currency, taxes, quotas and plan limits, feature flags, caching and staleness, notifications, and policy edge cases like refunds and trials. Use when an app computes prices, dates, entitlements, limits, or sends notifications.
---
# Business Rules

## Procedure
1. List every rule from the requirements as a numbered acceptance criterion. Missing policy gets NEEDS-PRODUCT-DECISION.
2. Time: user time zone vs. server UTC, DST change days, month end, leap day, "today" boundaries, expiry exactly at the limit. Use Stripe test clocks for billing time.
3. Money: integer cents, rounding mode, currency display, tax, discounts stacking, refunds partial and full, proration.
4. Limits and quotas: exactly at the limit, one over, reset timing, concurrent consumption.
5. Feature flags: each flag on and off for each role; flags cached client-side after change.
6. Caching: stale data after an update (CDN, browser, service worker, API cache); private data never cached publicly.
7. Notifications: right recipient, exactly once, correct links and time zone, opt-out respected. Verify by receiving them.
8. Policy transitions: trial → paid → past due → canceled → refunded, each with the expected access.

## Exit criteria
Each rule has PASS, FAIL, or NEEDS-PRODUCT-DECISION with EXECUTION evidence.
