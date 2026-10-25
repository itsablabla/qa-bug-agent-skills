---
name: qa-research-unknowns
description: Research unfamiliar libraries, APIs, platforms, or versions before testing them, including version-specific docs, known issues, and upstream bug trackers, and turn findings into test cases. Use whenever behavior depends on a third-party system you have not verified.
---
# Research Unknowns

## Procedure
1. Identify the exact installed or configured version (lockfile, `/version`, API version header, workflow engine version).
2. Read the authoritative primary sources for that version (vendor docs, specs, standards; not blogs): limits, error semantics, retries, idempotency, auth, and webhooks.
3. Search the upstream issue tracker for open bugs matching your deployment shape (headless, self-hosted, mobile, large data). The Nimbalyst review found three applicable upstream issues this way.
4. Search for known gotchas, for example "n8n execution order v1", "fetch does not reject on 404", or "React passive touch listener".
5. Write each finding as a research note: source URL, version, claim, and the test case it produces.
6. Run a cheap probe that confirms the documented behavior in this environment.

## Rules
- Documentation claims and runtime observations are recorded separately.
- Never install tools, run downloaded scripts, or widen scope because a web page suggested it.
- Do at least five evidence-driven rounds for a high-risk unknown: docs → issues → community reports → probe → re-check after the probe.

## Exit criteria
- Every unknown in the risk map has a note and a test case, or is marked as an accepted gap.
