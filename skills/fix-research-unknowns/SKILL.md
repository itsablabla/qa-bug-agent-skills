---
name: fix-research-unknowns
description: Research unfamiliar libraries, APIs, platforms, or versions before changing code that depends on them, using version-specific primary docs, changelogs, and upstream issues, and confirm with a small probe. Use whenever a fix relies on third-party behavior you have not verified.
---
# Research Before Changing

## Procedure
1. Find the exact installed version (lockfile, `/version`, API version header).
2. Read primary sources for that version: vendor docs, changelog, migration notes. Check semantics that fixes often get wrong: error codes, retries, idempotency keys, webhook signatures, time zones, caching.
3. Search upstream issues for your exact symptom and deployment shape; an upstream bug may need a workaround plus a pinned version.
4. Probe: a tiny script that confirms the documented behavior in this environment before you build on it.
5. Record each finding: source URL, version, claim, probe result.

## Exit criteria
Every third-party assumption in the fix plan has a source and a probe result.

Counterpart of tester skill: `qa-research-unknowns`.
