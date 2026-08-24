<div align="center">

# 🛡️ DVWA Reflected XSS — Cross-Site Scripting

### `Web Application Security` · `XSS Testing` · `Input Validation` · `DVWA`

<br>

<img src="https://img.shields.io/badge/DVWA-Web%20Security-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Reflected-XSS-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/CWE--79-Improper%20Neutralization-9A6700?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Severity-HIGH-CF222E?style=for-the-badge&logoColor=white" />

<br><br>

> **Assessment of DVWA's input-handling for a reflected Cross-Site Scripting (XSS) vulnerability, performed under the application's High security setting within an isolated Metasploitable 2 lab environment.**

</div>

---

## Overview

Assessment of DVWA's input-handling for a reflected Cross-Site Scripting (XSS) vulnerability, performed under the application's High security setting within an isolated Metasploitable 2 lab environment.

---

## Objective

Input `<script>alert(1)</script>` reflects back — identify the vulnerability name and its impact.

---

## Lab Environment

| Component | Details |
|---|---|
| **Attacker Machine** | Kali Linux |
| **Target Machine** | Metasploitable 2 |
| **Target IP** | `192.168.56.102` |
| **Web Application** | DVWA (Damn Vulnerable Web Application) |
| **Security Level** | High |

---

# Vulnerability Identified

<div align="center">

<img src="https://img.shields.io/badge/SEVERITY-HIGH-CF222E?style=for-the-badge&logoColor=white" />

<br><br>

## Reflected Cross-Site Scripting — XSS

### `CWE-79 — Improper Neutralization of Input During Web Page Generation`

</div>

User input submitted through the "XSS reflected" page's name field is reflected back into the response without output encoding or filtering, allowing injected JavaScript to execute in the victim's browser.

---

# Methodology

| Step | Action |
|:---:|---|
| **01** | Identified target IP via `ifconfig` on Metasploitable 2 (`192.168.56.102`) |
| **02** | Accessed DVWA login page and confirmed the web server was operational |
| **03** | Navigated to the "XSS reflected" page, which reflects the `name` input unfiltered |
| **04** | Injected the payload `<script>alert(1)</script>` into the input field |
| **05** | Submitted the payload — browser executed the script, confirming the vulnerability |

---

# Key Findings

| Status | Finding |
|:---:|---|
| <img src="https://img.shields.io/badge/VULNERABLE-CF222E?style=flat-square&logoColor=white" /> | The application reflects user input directly into the HTML response with no encoding — any HTML/JS-bearing input is interpreted, not displayed. |
| <img src="https://img.shields.io/badge/CONFIRMED-CF222E?style=flat-square&logoColor=white" /> | A minimal proof-of-concept payload was sufficient to trigger execution, indicating no filtering, sanitization, or CSP protections were in place even at High security. |

---

# Impact

<div align="center">

<img src="https://img.shields.io/badge/IMPACT-USER%20SESSION%20COMPROMISE-CF222E?style=for-the-badge&logoColor=white" />

</div>

Reflected XSS of this kind can be used to hijack user sessions, steal credentials, or perform actions on a victim's behalf by crafting a malicious link that executes attacker-controlled JavaScript in the victim's browser session.

---

# Remediation Recommendations

| Recommendation | Purpose |
|---|---|
| **Output Encoding** | Use `htmlspecialchars()` to convert `<` into `&lt;` and `>` into `&gt;` |
| **Input Validation** | Allowlist only safe characters, reject everything else |
| **Content Security Policy (CSP)** | Add `Content-Security-Policy: script-src 'self'` to block inline scripts |
| **HttpOnly Cookie Flag** | Prevent JavaScript access to session cookies |
| **X-XSS-Protection Header** | Enable browser-based reflected XSS filtering |
| **Regular Security Testing** | Routine XSS scans using OWASP ZAP or Burp Suite |

---

# Environment Disclaimer

> **Controlled Web Application Security Laboratory Exercise**

This assessment was performed against DVWA running on an isolated Metasploitable 2 instance inside a controlled lab environment. No unauthorized systems were accessed.

---

# Evidence

Full walkthrough with screenshots:

### [DVWA Reflected XSS — Evidence Report](./dvwa-reflected-xss-report.pdf)

---

<div align="center">

<img src="https://img.shields.io/badge/Web%20Application-Security-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/XSS-Testing-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Security-Assessment-8250DF?style=for-the-badge&logoColor=white" />

<br><br>

### Web Application Security · XSS Testing · Vulnerability Assessment

</div>
