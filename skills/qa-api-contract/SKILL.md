---
name: qa-api-contract
description: Test REST, GraphQL, and webhook APIs for contract conformance, input fuzzing, error semantics, idempotency, pagination, and rate limits using schema-driven and property-based tools. Use when an app exposes or consumes APIs or webhooks.
---
# API Contract and Fuzz Testing

## Procedure
1. Get or derive the contract: OpenAPI/GraphQL schema, or reconstruct one from observed traffic (HAR).
2. Schemathesis (approved environments only): `st run <schema> --phases=examples,coverage,fuzzing,stateful`, rate limited to the manifest. Treat 5xx, schema violations, and stateful-link failures as findings.
3. Property-based tests (fast-check / Hypothesis) for core logic: round-trips, invariants (totals never negative, one owner per object), and stateful models of create/update/delete.
4. Error semantics (fuzz each input with empty, whitespace, very long, wrong type, and Unicode values): invalid input → 4xx with a useful message, not 500; auth missing → 401; wrong owner → 403/404 without leaking existence.
5. Idempotency: replay POSTs with the same idempotency key and replay webhooks. Expect one effect.
6. Pagination and limits: empty, one item, page boundary, huge `limit`, negative `offset`.
7. Webhooks: valid signature, invalid signature, missing signature, replay, out of order, and wrong account. Only trusted state may change entitlements.
8. Rate limits on public endpoints, especially free-tier and AI-cost endpoints.
9. Sensitive fields: scan every JSON response for emails, phone numbers, tokens, and internal IDs that the caller should not see (another user's email was exposed in Round 3).
10. Serialization: dates, timezones, decimals and currency, null vs. missing, and Unicode (pattern C1).

## Exit criteria
Every endpoint in the contract has at least valid, invalid, unauthorized, and wrong-owner cases with recorded status.
