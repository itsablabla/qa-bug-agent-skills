---
name: fix-performance-flaky
description: Fix performance regressions, slow endpoints, memory growth, flaky failures, and race conditions by finding the nondeterministic or slow cause, never by adding sleeps or retries, and prove it statistically under soak. Use when the tester reports FLAKY, intermittent 5xx, slow pages, or degradation over time.
---
# Fix Performance and Flakiness

## Procedure
1. Measure first: failure rate over N≥20 runs, or p50/p95 latency against the base build.
2. Find the cause: shared mutable state, counters, missing awaits, ordering assumptions, N+1 queries, blocking work on the request path, unbounded caches, leaking listeners.
3. Fix the cause. Retries are allowed only for transient external faults, bounded and logged. No sleeps.
4. Prove it:
   - Flakiness: 0 failures in ≥1,000 calls (to claim a failure rate under 1 in N you need about 3N clean calls).
   - Soak: rerun the hidden tests after 3,000 realistic requests (one cheat stopped working after 2,000).
   - Latency: deployed p95 ≤ max(2× base p95, base p95 + 100 ms).
   - Memory: flat over a 30-minute session.
5. Approved load tests only (k6) within the manifest limits.

## Exit criteria
Before/after numbers with N, the named cause, and no added sleeps or unbounded retries.

Counterpart of tester skill: `qa-performance-resilience`.
