---
name: fix-api-contract
description: Fix API and webhook bugs — wrong status codes, 5xx on bad input, missing validation, broken idempotency, pagination errors, leaked fields, serialization mistakes — at the contract boundary with schema validation and an allow-list serializer. Use for any REST, GraphQL, or webhook defect.
---
# Fix API and Contract Bugs

## Procedure
1. Validate input at the boundary (type, emptiness, length, format) with a schema; bad input returns 400/422 with a plain message, never 500.
2. One allow-list serializer per resource for every response, including create, update, and duplicate paths. Never send raw records.
3. Idempotency: dedupe by key or `event_id` before side effects; set state, don't increment it.
4. Pagination and limits: clamp `limit`, reject negative offsets, stable ordering.
5. Serialization: parse dates at boundaries, use integer cents, and send `null` vs. missing deliberately.
6. Contract diff: compare response shapes before and after; announce every change; never drop a field without checking callers.
7. Re-run schema fuzzing (Schemathesis) and the tester's contract tests.

## Exit criteria
Fuzzing returns no 5xx and no schema violations, and the contract diff is empty or explicitly approved.

Counterpart of tester skill: `qa-api-contract`.
