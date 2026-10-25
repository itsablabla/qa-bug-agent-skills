---
name: qa-performance-resilience
description: Measure Core Web Vitals, API latency, slow-network and offline behavior, failure recovery, memory growth, and approved load. Use for performance, reliability, or resilience testing.
---
# Performance and Resilience

## Procedure
1. Lighthouse plus web-vitals on key routes, mobile profile. Targets at p75: LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1 ([thresholds](https://www.pagespeedmatters.com/resources/guides/complete-core-web-vitals-guide)).
2. Throttle to Fast 3G and go offline mid-action. The UI shows state and recovers without data loss.
3. API p50 and p95 per endpoint from HAR. Flag slow calls on the critical path.
4. Long sessions: memory growth over 30 minutes, large data sets, and big transcripts (Nimbalyst heap issues).
5. Failure injection (staging): kill a dependency, return 500 or timeouts, restart services. Watch customer-visible behavior.
6. Load (approved only): ramp with k6 within the manifest's limits, and watch error rate and queue depth.
7. Gateway limits: large headers and cookies on signed-in pages (pattern E4).

## Exit criteria
A metrics table per route and endpoint, plus resilience scenarios with observed behavior.
