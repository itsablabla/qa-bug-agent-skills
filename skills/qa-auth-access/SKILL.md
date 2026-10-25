---
name: qa-auth-access
description: Test authentication, sessions, roles, multi-tenant isolation, and object-level authorization, including IDOR, token tampering, magic links, and private content leakage through feeds, search, caches, and storage URLs. Use for any app with accounts or private data.
---
# Auth and Access Control

## Procedure
Use two customer accounts (A and B), an admin, and a signed-out browser.
1. Signup, verify, and login: new and existing email, invalid email, double-click, expired or reused verification link, and the original intent (such as a pending URL) surviving the redirect.
2. Sessions: logout invalidates the session server-side (use a stable probe: repeat the request at least 3 times before and after; 5xx never decides the result), concurrent sessions, session fixation, and cookie flags (HttpOnly, Secure, SameSite).
3. Object access: A requests B's object by changing IDs in the URL, body, and GraphQL variables. Expect 403/404 with no data in the body.
4. Tokens: tampered signature, `alg:none`, wrong issuer or audience, expired, and an untrusted key URL. Identity must never come from a posted email or member ID.
5. Private content leakage: Content API, RSS, sitemap, site search, OG tags, CDN/storage direct links, cached HTML, and unpaid HTML/JSON containing paid text.
6. Roles: downgrade mid-session, an unrelated tier or comp membership unlocking everything, and admin endpoints from a customer session.
7. Password reset, email change, and account deletion flows.

## Rules
On any cross-tenant leak, it is P0: stop and escalate. Do not browse more real records to prove it.

## Exit criteria
The matrix of role × object × action is complete with statuses.
