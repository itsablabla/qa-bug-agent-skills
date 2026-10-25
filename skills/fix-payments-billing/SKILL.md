---
name: fix-payments-billing
description: Fix checkout, payment webhook, entitlement, subscription, refund, and price-display bugs so only verified provider events grant access, events are idempotent, refunds revoke, and money totals reconcile. Use for any money-moving or paywalled defect.
---
# Fix Payments and Billing

## Procedure
1. Entitlement comes only from verified, signed provider events. Success pages and client flags only read state.
2. Webhooks: verify signatures, dedupe on event ID, and set entitlement (no counters). A refund or chargeback revokes access for that purchase only — check other customers and other purchases (an over-broad refund fix was a benchmark cheat).
3. Never put paid content in unpaid HTML or JSON, including create responses.
4. One price constant from the approved offer, rendered everywhere.
5. Test in TEST mode with the provider CLI: success, decline, 3DS, replay, reorder, invalid signature; use test clocks for renewals and trials.
6. Data: count wrong grants (duplicates, grants after refunds) and repair them through `fix-data-repair`. Live money actions need approval.
7. Reconcile: provider charges = internal orders = entitlements.

## Exit criteria
Every money path has provider-side and internal-state proof, isolation holds, and reconciliation shows zero orphans.

Counterpart of tester skill: `qa-payments-billing`.
