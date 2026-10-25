---
name: qa-security-web
description: Run scoped, non-destructive web security checks guided by OWASP ASVS 5.0 and the WSTG, covering injection, XSS, SSRF, CSRF, open redirects, headers, secrets exposure, and rate limits. Use for security review of any web app within approved scope.
---
# Web Security (scoped)

Reference: [OWASP ASVS 5.0](https://github.com/owasp/asvs) for requirements and the [WSTG](https://wstg.owasp.org/) for methods. Active or disruptive tests need explicit approval.

## Procedure
1. Passive scan: ZAP baseline and security headers (CSP, HSTS, X-Content-Type-Options, frame-ancestors, Referrer-Policy).
2. Cookies: session cookies have HttpOnly, Secure (on HTTPS), and SameSite. Check the raw Set-Cookie header.
3. Secrets: search the served JS bundles, source maps, `.env` exposure, git directories, and error pages for keys and tokens.
4. XSS: put HTML/script-like text in every stored field (names, titles, findings) and confirm it renders inert.
5. Injection: SQL-ish and template-ish strings in search, filters, and IDs. Look for errors or behavior changes.
6. SSRF (for any URL input): loopback, private ranges, link-local, IPv6, decimal IPs, redirect-to-private, and DNS rebinding. Use controlled fixtures only, never real metadata endpoints.
7. CSRF on state-changing endpoints, and CORS misconfiguration (reflected origin with credentials).
8. Open redirects on `next=`, `return_url=`, and `redirect=`.
9. Uploads: content-type spoofing, oversized files, path traversal in filenames, and SVG with script.
10. Rate limiting on login, signup, password reset, free-tier, and AI endpoints.
11. Dependency audit (`npm audit`, `pip-audit`) and the lockfile age.

## Exit criteria
Each ASVS chapter in scope is marked tested, not applicable, or blocked.
