
<div align="center">

# 🔐 Session Hijacking via Cookie Injection

### `Session Security` · `Cookie Handling` · `Authentication Bypass` · `Browser Security`

<br>

<img src="https://img.shields.io/badge/Controlled-Lab%20Assessment-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Session-Hijacking-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Cookie-Injection-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Browser-Security-9A6700?style=for-the-badge&logoColor=white" />

<br><br>

> **A hands-on demonstration of session hijacking by extracting an authenticated session cookie from one browser and injecting it into a second browser to demonstrate authentication bypass.**

</div>

---

## Overview

This practical demonstrates a session-hijacking workflow in which an authenticated session cookie is extracted from one browser and injected into a second, unauthenticated browser.

The exercise demonstrates how possession and replay of authentication session cookies can allow an attacker to impersonate an already-authenticated session without entering the account password again.

---

## Objective

Demonstrate session hijacking by:

- Extracting an authenticated session cookie.
- Transferring the cookie set to another browser.
- Injecting the cookies into a fresh browser session.
- Validating whether authentication is preserved.
- Documenting the resulting session access.

---

## Lab Environment

| Component | Configuration |
|---|---|
| **Test Target** | Facebook — session/cookie handling demonstration |
| **Browser A** | Firefox — authenticated session |
| **Browser B** | Chrome — fresh, unauthenticated session |
| **Tool Used** | Cookie-Editor browser extension |
| **Environment** | Controlled security demonstration |

---

## Tool Used

<div align="center">

<img src="https://img.shields.io/badge/Cookie--Editor-Browser%20Extension-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Firefox-Authenticated%20Session-0969DA?style=for-the-badge&logo=firefox&logoColor=white" />
<img src="https://img.shields.io/badge/Chrome-Validation%20Browser-1A7F37?style=for-the-badge&logo=googlechrome&logoColor=white" />

</div>

---

# Vulnerability Classification

<div align="center">

<img src="https://img.shields.io/badge/SESSION%20SECURITY-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/COOKIE%20REPLAY-8250DF?style=for-the-badge&logoColor=white" />

</div>

### Insecure Session Cookie Handling

The documented workflow demonstrates that an obtained authentication session cookie can be replayed in another browser context to preserve the authenticated state.

> **CWE Reference:** `CWE-384` was identified in the original practical material; however, the demonstrated behavior is more specifically described as **session-cookie theft/replay or session hijacking** rather than classic session fixation.

The key security issue demonstrated is that possession of a valid authentication cookie may be sufficient to impersonate the associated authenticated session.

---

# Methodology

| # | Stage | Action | Result |
|:---:|---|---|---|
| **01** | **Authentication** | Logged into the target account in Browser A (Firefox) with valid credentials | Authenticated session established |
| **02** | **Cookie Extraction** | Extracted session cookies using Cookie-Editor | Authentication cookie set obtained |
| **03** | **Cookie Transfer** | Copied the required cookie values | Cookie data prepared for replay |
| **04** | **Fresh Session** | Opened Browser B (Chrome) with an unauthenticated session | Clean browser context established |
| **05** | **Cookie Injection** | Injected the copied cookies into Browser B using Cookie-Editor | Session state replaced |
| **06** | **Validation** | Refreshed the page | Browser B inherited the authenticated session |

---

# Workflow at a Glance

```text
Authenticated Browser
        ↓
Session Cookie Extraction
        ↓
Cookie Transfer
        ↓
Fresh Browser Session
        ↓
Cookie Injection
        ↓
Session Replay
        ↓
Authentication State Validation
````

---

# Key Findings

|                                                 Status                                                 | Finding                                                                                                                                |
| :----------------------------------------------------------------------------------------------------: | -------------------------------------------------------------------------------------------------------------------------------------- |
|  <img src="https://img.shields.io/badge/SESSION%20REPLAY-CF222E?style=flat-square&logoColor=white" />  | The demonstrated cookie set was sufficient to reproduce the authenticated session in the second browser.                               |
|    <img src="https://img.shields.io/badge/AUTH%20BYPASS-9A6700?style=flat-square&logoColor=white" />   | Browser B inherited the authenticated state without requiring the account password again.                                              |
| <img src="https://img.shields.io/badge/SESSION%20BOUNDARY-8250DF?style=flat-square&logoColor=white" /> | The practical demonstrated that the authentication state could be replayed across browser contexts using the obtained session cookies. |

---

# Result

<div align="center">

<img src="https://img.shields.io/badge/SESSION%20HIJACKING-DEMONSTRATED-CF222E?style=for-the-badge&logoColor=white" />

</div>

The documented practical successfully demonstrated session hijacking through cookie injection.

Browser B gained access to the authenticated session without requiring the account password again.

---

# Security Impact

Successful session-cookie replay can allow an attacker who obtains valid authentication cookies to impersonate the associated user session.

Depending on the application's session controls and the privileges associated with the compromised account, this may result in unauthorized access to account functionality and sensitive information.

---

# Remediation Recommendations

| Control                       | Security Purpose                                                                |
| ----------------------------- | ------------------------------------------------------------------------------- |
| **HttpOnly Flag**             | Prevent client-side JavaScript from directly accessing authentication cookies   |
| **Secure Flag**               | Ensure sensitive cookies are transmitted only over HTTPS                        |
| **SameSite Attribute**        | Reduce certain cross-site request and cookie abuse scenarios                    |
| **Short Session Lifetime**    | Reduce the useful lifetime of compromised session tokens                        |
| **Session Rotation**          | Rotate session identifiers after authentication and sensitive security events   |
| **Session Revocation**        | Provide mechanisms to invalidate active sessions when compromise is suspected   |
| **Additional Authentication** | Require re-authentication or step-up verification for sensitive account actions |

---

# What I Learned

This practical demonstrated the importance of treating authentication session cookies as highly sensitive credentials.

It also reinforced how session security depends not only on passwords, but also on secure cookie handling, session lifecycle management, token protection, and effective session invalidation.

---

# Environment Disclaimer

> **Controlled Security Demonstration**

This write-up documents a controlled cybersecurity demonstration using an isolated and authorized testing context.

Session cookies and authentication tokens should only be handled within systems and accounts for which explicit authorization has been obtained.

No unauthorized production account access is claimed.

---

# Evidence

Full walkthrough with screenshots:

### [Session Hijacking via Cookie Injection — Evidence Report](./session-hijacking-cookie-injection.pdf)

---

<div align="center">

<img src="https://img.shields.io/badge/Session-Security-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Web-Application%20Security-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Technical-Documentation-8250DF?style=for-the-badge&logoColor=white" />

<br><br>

### Web Security · Session Management · Practical Testing

</div>
