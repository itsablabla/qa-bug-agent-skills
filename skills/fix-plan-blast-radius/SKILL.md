---
name: fix-plan-blast-radius
description: Plan the smallest correct fix at the right trust boundary, listing siblings, callers, adjacent journeys, contract changes, data impact, rollback, and approvals before writing code. Use for every non-trivial fix and always for security, payment, auth, or data bugs.
---
# Fix Plan and Blast Radius

Fill `templates/fix-plan.md`:
1. Fix location: the layer that owns the rule (server for access, payments, and validation; template for rendering; job for async).
2. Smallest change; a shared helper when the class appears more than once (`requireOwner`, `safePath`, `parsePublicUrl`, `toPublic`, an idempotency store).
3. Siblings: search patterns and hits (see `fix-class-sweep`).
4. Callers and adjacent journeys at risk, mapped to the tester's guard tests.
5. Contract change? List every field, status code, or shape that changes. In our lab an allow-list serializer silently dropped `owner` and broke a journey.
6. Customer-visible or policy change? Then NEEDS-PRODUCT-DECISION.
7. Data impact and repair plan.
8. Rollback: revert, flag, or config switch.
9. Approvals: deploys, data repair, and policy only.

## Exit criteria
The plan is complete, and approvals are requested in one batch if needed.

Counterpart of tester skill: `qa-recon-risk-map`.
