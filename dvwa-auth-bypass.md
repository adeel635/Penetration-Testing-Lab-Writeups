# DVWA Authentication Bypass — Brute Force Attack

## Overview

Assessment of DVWA's login mechanism for resistance against automated credential 
guessing, performed under the application's Low security setting to evaluate baseline 
authentication controls.

## Objective

To identify weak authentication controls and perform a brute-force attack to obtain 
valid login credentials.

## Lab Environment

- **Attacker Machine:** Kali Linux
- **Target Machine:** Metasploitable 2
- **Web Application:** DVWA (Damn Vulnerable Web Application)
- **Security Level:** Low

## Tools Used

`Burp Suite (Proxy & Intruder)` · `Kali Linux`

## Vulnerability Identified

**Weak Authentication Mechanism (CWE-307: Improper Restriction of Excessive 
Authentication Attempts)**

The application does not implement rate-limiting, account lockout, or CAPTCHA 
protections, allowing unlimited login attempts against the same account.

## Methodology

| Step | Action |
|---|---|
| 1 | Accessed the DVWA login page |
| 2 | Enabled Burp Suite and intercepted the login request |
| 3 | Identified POST parameters: `username`, `password` |
| 4 | Sent the captured request to Burp Intruder |
| 5 | Configured a **Cluster Bomb** attack — known username (`admin`) against a password wordlist (rockyou.txt) |
| 6 | Analyzed Intruder results by response length and status code to isolate anomalies |
| 7 | Identified the response with a distinct length/status, confirming a successful login |

## Key Findings

- The absence of attempt-throttling made the login form fully susceptible to automated 
  credential stuffing/brute-force via a standard wordlist.
- Response-length differential analysis was sufficient to distinguish a successful login 
  from failed attempts — the application does not obscure this signal.

## Result

- Successfully cracked the login credentials
- Gained unauthorized access to the admin panel

## Remediation Recommendations

- Implement account lockout or exponential back-off after repeated failed attempts
- Add CAPTCHA or similar challenge after N failed logins
- Return uniform response length/timing for both valid and invalid login attempts
- Enforce strong password policy to reduce wordlist-based attack success

## Environment Disclaimer

This assessment was performed against DVWA running on an isolated Metasploitable 2 
instance inside a controlled VirtualBox lab environment. No unauthorized systems were 
accessed.

## Evidence

Full walkthrough with screenshots: [dvwa-auth-bypass-report.pdf](./dvwa-auth-bypass-report.pdf)
