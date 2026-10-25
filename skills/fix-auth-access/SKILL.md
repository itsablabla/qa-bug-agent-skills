---
name: fix-auth-access
description: Fix authentication, session, role, tenant-isolation, and object-access bugs on the server with a single ownership helper applied to every route, verified in both directions and on old and new records. Use for IDOR, data leaks across users, session, cookie, or role bugs.
---
# Fix Auth and Access

## Procedure
1. One helper owns the rule (`requireOwner` / `ownAudit`): missing or not owned → 404, so existence isn't revealed. Every lookup uses it: API, pages, exports, search, checkout, delete.
2. Scope every collection query by owner or tenant inside the query, not after.
3. Sessions: logout deletes the server session and expires the cookie; cookies are `HttpOnly; SameSite=Lax; Secure` on HTTPS; identity never comes from a posted email or ID.
4. Roles: check on every request, not only at login; a downgrade takes effect immediately.
5. Prove both directions (A→B, B→A), signed-out access, aged records, a real-browser user-agent, and production config. Each was a cheat our Done-Gate caught.
6. Run the sweep and log review from `fix-security-hotfix` if data may have leaked.

## Exit criteria
The ownership matrix (role × object × action) passes, including the hidden both-directions and aged-record tests.

Counterpart of tester skill: `qa-auth-access`.
