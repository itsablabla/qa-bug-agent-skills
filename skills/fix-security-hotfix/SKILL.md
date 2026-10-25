---
name: fix-security-hotfix
description: Handle security bugs — data exposure, auth or payment bypass, SSRF, XSS, CSRF, open redirects, secrets, missing rate limits — with contain-first steps, server-side fixes using shared guards, bypass-variant sweeps, exploitation log review, and minimal disclosure. Use for any P0/P1 security finding.
---
# Security Fixes

## Procedure
1. Contain (P0): flag off, block the route, or require auth temporarily. Production containment needs fast approval with the exact change.
2. Fix on the server with a shared guard: `safePath` (redirects), `parsePublicUrl` + DNS re-check at fetch time (SSRF), DOM text nodes and template escaping (XSS), CSRF tokens or SameSite, a rate limiter on public and AI-cost endpoints, secure cookie flags.
3. Sweep with `fix-class-sweep`, including every bypass variant.
4. Check logs for past exploitation and report counts, not personal data.
5. Secrets: request rotation; never paste values anywhere.
6. Disclosure: keep exploit details out of tickets and chats.
7. Ask for expedited verification; keep containment until VERIFIED and deployed.

## Exit criteria
Containment recorded, the fix VERIFIED with bypass variants, log review summarized, and owner decisions requested.

Counterpart of tester skill: `qa-security-web`.
