<div align="center">

# 🔐 DVWA Authentication Bypass — Brute Force Attack

### `Web Application Security` · `Authentication Testing` · `Burp Suite` · `DVWA`

<br>

<img src="https://img.shields.io/badge/DVWA-Web%20Security-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Authentication-Testing-9A6700?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Burp%20Suite-Intruder-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Kali-Linux-1A7F37?style=for-the-badge&logo=kalilinux&logoColor=white" />

<br><br>

> **Assessment of DVWA's login mechanism for resistance against automated credential guessing, performed under the application's Low security setting to evaluate baseline authentication controls.**

</div>

---

## Overview

Assessment of DVWA's login mechanism for resistance against automated credential guessing, performed under the application's Low security setting to evaluate baseline authentication controls.

---

## Objective

To identify weak authentication controls and perform a brute-force attack to obtain valid login credentials.

---

## Lab Environment

| Component | Details |
|---|---|
| **Attacker Machine** | Kali Linux |
| **Target Machine** | Metasploitable 2 |
| **Web Application** | DVWA (Damn Vulnerable Web Application) |
| **Security Level** | Low |

---

## Tools Used

<div align="center">

<img src="https://img.shields.io/badge/Burp%20Suite-Proxy%20%26%20Intruder-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Kali-Linux-1A7F37?style=for-the-badge&logo=kalilinux&logoColor=white" />

</div>

---

# Vulnerability Identified

### Weak Authentication Mechanism

**CWE-307: Improper Restriction of Excessive Authentication Attempts**

The application does not implement rate-limiting, account lockout, or CAPTCHA protections, allowing unlimited login attempts against the same account.

---

# Methodology

| Step | Action |
|:---:|---|
| **01** | Accessed the DVWA login page |
| **02** | Enabled Burp Suite and intercepted the login request |
| **03** | Identified POST parameters: `username`, `password` |
| **04** | Sent the captured request to Burp Intruder |
| **05** | Configured a **Cluster Bomb** attack — known username (`admin`) against a password wordlist (`rockyou.txt`) |
| **06** | Analyzed Intruder results by response length and status code to isolate anomalies |
| **07** | Identified the response with a distinct length/status, confirming a successful login |

---

# Key Findings

| Status | Finding |
|:---:|---|
| <img src="https://img.shields.io/badge/VULNERABLE-CF222E?style=flat-square&logoColor=white" /> | The absence of attempt-throttling made the login form fully susceptible to automated credential stuffing/brute-force via a standard wordlist. |
| <img src="https://img.shields.io/badge/DETECTED-9A6700?style=flat-square&logoColor=white" /> | Response-length differential analysis was sufficient to distinguish a successful login from failed attempts — the application does not obscure this signal. |

---

# Result

- Successfully cracked the login credentials
- Gained unauthorized access to the admin panel

---

# Remediation Recommendations

| Recommendation | Purpose |
|---|---|
| **Account Lockout / Exponential Back-off** | Implement after repeated failed authentication attempts |
| **CAPTCHA** | Add a challenge after N failed login attempts |
| **Uniform Responses** | Return consistent response length/timing for valid and invalid login attempts |
| **Strong Password Policy** | Reduce the success of wordlist-based attacks |

---

# Environment Disclaimer

> **Controlled Web Application Security Laboratory Exercise**

This assessment was performed against DVWA running on an isolated Metasploitable 2 instance inside a controlled VirtualBox lab environment. No unauthorized systems were accessed.

---

# Evidence

Full walkthrough with screenshots:

### [DVWA Authentication Bypass — Brute Force Attack Report](./dvwa-auth-bypass-report.pdf)

---

<div align="center">

### Web Application Security · Authentication Testing · Security Assessment

</div>
