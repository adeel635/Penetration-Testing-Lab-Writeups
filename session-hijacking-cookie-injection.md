# Session Hijacking via Cookie Injection

## Overview

A hands-on demonstration of session hijacking by extracting an authenticated session 
cookie from one browser and injecting it into a second, unauthenticated browser — 
gaining full account access without ever entering a password.

## Objective

Demonstrate session hijacking by extracting a session cookie from one browser, 
injecting it into another browser, and gaining unauthorized access without credentials.

## Lab Environment

- **Test Target:** Facebook (session/cookie handling demonstration)
- **Browser A:** Firefox — authenticated session
- **Browser B:** Chrome — fresh, unauthenticated session
- **Tool Used:** Cookie-Editor (browser extension)

## Vulnerability Identified

**Insecure Session Cookie Handling (CWE-384: Session Fixation)**

A session cookie, once obtained, was sufficient on its own to fully impersonate an 
authenticated user — no password or second factor was required to hijack the session.

## Methodology

| Step | Action |
|---|---|
| 1 | Logged into the target account in Browser A (Firefox) with valid credentials |
| 2 | Extracted session cookies (`c_user`, `xs`, `datr`, etc.) using the Cookie-Editor extension |
| 3 | Copied the full set of session cookie values |
| 4 | Opened Browser B (Chrome) with a fresh, unauthenticated session |
| 5 | Injected the copied cookies into Browser B using Cookie-Editor |
| 6 | Refreshed the page — Browser B was automatically logged in, no password prompt |

## Key Findings

- Session cookies functioned as a complete authentication bypass — possession of the 
  cookie set was equivalent to possession of the password.
- No additional binding (IP, device fingerprint, or short-lived expiry) was in place to 
  invalidate a session cookie used from an unexpected browser/context.

## Result

✅ Session hijacking was successful — Browser B gained full access to the account with 
no authentication prompt.

## Remediation Recommendations

- **HttpOnly Flag** — prevents JavaScript from accessing cookies
- **Secure Flag** — cookies are only sent over HTTPS
  
## Evidence

Full walkthrough with screenshots: [session-hijacking-cookie-injection.pdf](./session-hijacking-cookie-injection.pdf)
