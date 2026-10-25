---
name: qa-payments-billing
description: Test checkout, payment webhooks, entitlements, subscriptions, refunds, and disputes in test mode using Stripe CLI and test clocks, or Chargebee test sites. Use for any money-moving or paywalled feature.
---
# Payments and Billing

## Preflight
Confirm the account, mode (TEST), price IDs, amount, and currency against the approved offer. Live charges and refunds need explicit approval per action.

## Procedure
1. Checkout: the correct product, customer, and amount; cancel and return; repeated clicks; an arbitrary `return_url` rejected; and a checkout started by a non-owner rejected.
2. Success page: forged query parameters unlock nothing (pattern A4). Entitlement comes from verified provider state.
3. Webhooks: `stripe listen` + `stripe trigger` for success, failure, and async payment methods. Replay duplicates, reverse order, send an invalid signature, and use the wrong account or mode.
4. Cards: success, decline, insufficient funds, 3DS required, and expired.
5. Subscriptions: use test clocks for trial end, renewal, failed renewal → dunning, cancel at period end, upgrade/downgrade, and proration ([Stripe billing testing](https://docs.stripe.com/billing/testing)).
6. Refunds and disputes: full, partial, and dispute open/won/lost. Access follows the approved policy; if there is no policy, mark it NEEDS-PRODUCT-DECISION.
7. Paying while generation or review is still incomplete.
8. Reconciliation: provider charges equal internal orders equal entitlements, with no orphans.

## Exit criteria
Every money path has a provider-side proof and an internal-state proof.
