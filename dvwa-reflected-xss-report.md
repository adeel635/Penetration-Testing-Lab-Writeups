# DVWA Reflected XSS — Cross-Site Scripting

## Overview

Assessment of DVWA's input-handling for a reflected Cross-Site Scripting (XSS) 
vulnerability, performed under the application's High security setting within an 
isolated Metasploitable 2 lab environment.

## Objective

Input `<script>alert(1)</script>` reflects back — identify the vulnerability name and 
its impact.

## Lab Environment

- **Attacker Machine:** Kali Linux
- **Target Machine:** Metasploitable 2
- **Target IP:** 192.168.56.102
- **Web Application:** DVWA (Damn Vulnerable Web Application)
- **Security Level:** High

## Vulnerability Identified

**Reflected Cross-Site Scripting — XSS (CWE-79: Improper Neutralization of Input 
During Web Page Generation)**

**Severity: HIGH**

User input submitted through the "XSS reflected" page's name field is reflected back 
into the response without output encoding or filtering, allowing injected JavaScript 
to execute in the victim's browser.

## Methodology

| Step | Action |
|---|---|
| 1 | Identified target IP via `ifconfig` on Metasploitable 2 (192.168.56.102) |
| 2 | Accessed DVWA login page and confirmed the web server was operational |
| 3 | Navigated to the "XSS reflected" page, which reflects the `name` input unfiltered |
| 4 | Injected the payload `<script>alert(1)</script>` into the input field |
| 5 | Submitted the payload — browser executed the script, confirming the vulnerability |

## Key Findings

- The application reflects user input directly into the HTML response with no 
  encoding — any HTML/JS-bearing input is interpreted, not displayed as text.
- A minimal proof-of-concept payload was sufficient to trigger execution, indicating 
  no filtering, sanitization, or CSP protections were in place even at High security.

## Impact

Reflected XSS of this kind can be used to hijack user sessions, steal credentials, or 
perform actions on a victim's behalf by crafting a malicious link that executes 
attacker-controlled JavaScript in the victim's browser session.

## Remediation Recommendations

- **Output Encoding** — use `htmlspecialchars()` to convert `<` into `&lt;` and `>` into `&gt;`
- **Input Validation** — allowlist only safe characters, reject everything else
- **Content Security Policy (CSP)** — add `Content-Security-Policy: script-src 'self'` to block inline scripts
- **HttpOnly Cookie Flag** — prevent JavaScript access to session cookies
- **X-XSS-Protection Header** — enable browser-based reflected XSS filtering
- **Regular Security Testing** — routine XSS scans using OWASP ZAP or Burp Suite

## Environment Disclaimer

This assessment was performed against DVWA running on an isolated Metasploitable 2 
instance inside a controlled lab environment. No unauthorized systems were accessed.

## Evidence

Full walkthrough with screenshots: [dvwa-reflected-xss-report.pdf](./dvwa-reflected-xss-report.pdf)
