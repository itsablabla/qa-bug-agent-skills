---
name: fix-class-sweep
description: After fixing one instance, search served code and source for every sibling of the same bug class, including bypass variants, and fix or list each one. Use for every fix of a security, validation, access, idempotency, rendering, or error-handling bug.
---
# Class Sweep

| Class | Search | Bypass variants to prove |
|---|---|---|
| Open redirect | `redirect(`, `location =`, `next`, `return_url` | `https://evil`, `//evil`, `/\evil`, `%2F%2Fevil`, `javascript:` |
| Ownership (IDOR) | every lookup by `params.id`/`query.id`; search; exports; report pages | ID swap in URL, body, GraphQL, both directions |
| XSS | `innerHTML`, `dangerouslySetInnerHTML`, `v-html`, raw template output | HTML, attribute, and URL contexts |
| SSRF | server-side fetch of stored or user URLs | `127.1`, `0x7f000001`, `2130706433`, `[::1]`, `169.254.169.254`, DNS names resolving private |
| Idempotency | webhooks and POSTs that grant, charge, or email | replay, reorder, concurrent |
| Client trust | price, role, paid, or owner from the request | forged fields |
| Sensitive fields | every serializer, including create and duplicate responses | other users' emails, paid text, tokens |
| Swallowed errors | `catch {}`, missing `res.ok`, continue-on-fail | 404/500 paths |

## Procedure
1. Run every search for the class; list hits with file:line.
2. Fix each with the shared helper, or list it with a reason.
3. Run the Fixer guards (`tools/guards.py` or its ESLint/semgrep port); zero new hits.

## Exit criteria
A sweep report (searches, hits, fixed, listed with reasons) and a clean guard run.

Counterpart of tester skill: `qa-static-scan`.
