---
name: qa-static-scan
description: Search served JavaScript, templates, CSS, and source code for known bug classes (unchecked fetch responses, innerHTML with user data, removed focus outlines, unvalidated redirects, swallowed errors, secrets) and turn every hit into a targeted live test. Use early in any test run or code review.
---
# Static Scan

Static hits are SOURCE evidence and count only as hints. Each one must become a live case before it can be called a bug.

## Patterns to search (served code first, then repo)
| Pattern | Regex idea | Bug class |
|---|---|---|
| fetch result used without `r.ok` / `res.ok` check | `await fetch(` with no `.ok` / `status` nearby before navigation | Silent failure (A1) |
| `innerHTML` / `dangerouslySetInnerHTML` / `v-html` with data | `innerHTML\s*=` | Stored XSS |
| Focus removed | `outline:\s*none` without `:focus-visible` replacement | Accessibility (D7) |
| Redirect from query | `get('next')`, `return_url`, `redirect=` assigned to `location` or `res.redirect` | Open redirect |
| Swallowed errors | `catch\s*\(\w*\)\s*\{\s*\}`, `continueOnFail`, `alwaysOutputData`, never-error | Silent failure (A2) |
| Secrets | `sk_live_`, `whsec_`, `AKIA`, `-----BEGIN`, JWTs in bundles or source maps | Secret exposure |
| Lazy images in transformed or off-canvas containers | `loading="lazy"` inside carousels or tracks | Image never loads (D1) |
| Passive touch handlers that call preventDefault | `onTouchMove` + `preventDefault` | Mobile gesture (D2) |
| Duplicate implementations | Two handlers or endpoints for one action | Drift (E6) |

## Learned rules
Also run every rule in `tools/harness/tester-static-rules.json` (15 rules exported by the Fixer from verified fixes, G01–G15). Rules marked `guard-ok: <rule> <reason>` in the source are reviewed exceptions.

## Procedure
1. Fetch every route's served HTML/JS (and source maps if public), plus the repo at the deployed commit.
2. Run the patterns and record file:line or route.
3. For each hit, write a live case ID in the matrix.

## Exit criteria
Every hit is either converted into a live case or dismissed with a written reason.
