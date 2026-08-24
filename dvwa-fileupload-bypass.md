<div align="center">

# 🛡️ DVWA File Upload Security Bypass — Remote Code Execution

### `Web Application Security` · `File Upload Testing` · `Burp Suite` · `Metasploit`

<br>

<img src="https://img.shields.io/badge/DVWA-Web%20Security-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/File%20Upload-Security-9A6700?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Burp%20Suite-Testing-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Metasploit-Framework-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/msfvenom-Payload-1A7F37?style=for-the-badge&logoColor=white" />

<br><br>

> **Assessment of DVWA's file-upload feature under the application's High security setting, to determine whether server-side validation could be bypassed to achieve code execution.**

</div>

---

## Overview

Assessment of DVWA's file-upload feature under the application's High security setting, to determine whether server-side validation could be bypassed to achieve code execution.

---

## Objective

To bypass file upload restrictions implemented at the High security level and achieve remote code execution on the target system.

---

## Lab Environment

| Component | Details |
|---|---|
| **Attacker Machine** | Kali Linux |
| **Target Machine** | Metasploitable 2 |
| **Web Application** | DVWA (Damn Vulnerable Web Application) |
| **Security Level** | High |

---

## Tools Used

<div align="center">

<img src="https://img.shields.io/badge/Burp%20Suite-Testing-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Metasploit-Framework-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/msfvenom-Payload-1A7F37?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Kali-Linux-0969DA?style=for-the-badge&logo=kalilinux&logoColor=white" />

</div>

---

# Vulnerability Identified

<div align="center">

### <img src="https://img.shields.io/badge/CRITICAL-CF222E?style=for-the-badge&logoColor=white" />

## Improper File Upload Validation

### `CWE-434 — Unrestricted Upload of File with Dangerous Type`

</div>

The application failed to properly validate uploaded files on the server side, allowing bypass via a double file extension (e.g., `.php.jpg`).

---

# Methodology

| Step | Action |
|:---:|---|
| **01** | Generated a malicious PHP payload with `msfvenom` (`php/meterpreter/reverse_tcp`) |
| **02** | Configured a listener in `msfconsole` (`exploit/multi/handler`) |
| **03** | Attempted direct upload of the `.php` payload — rejected by server-side filtering |
| **04** | Enabled Burp Suite and turned Intercept ON |
| **05** | Re-uploaded the file and captured the request in Burp |
| **06** | Modified the filename in-flight to `shell.php.jpg` to bypass extension filtering |
| **07** | Forwarded the modified request — upload succeeded |
| **08** | Accessed the uploaded file directly via browser |
| **09** | Payload executed — Meterpreter session established |

---

# Key Findings

| Status | Finding |
|:---:|---|
| <img src="https://img.shields.io/badge/CWE--434-CF222E?style=flat-square&logoColor=white" /> | **Improper File Upload Validation** — server-side validation relied on filename/extension inspection alone, which was bypassed by appending a trailing `.jpg` to a `.php` payload. |
| <img src="https://img.shields.io/badge/CRITICAL-CF222E?style=flat-square&logoColor=white" /> | Once uploaded, the file remained directly web-accessible with no execution restrictions on the uploads directory, allowing immediate code execution on request. |
| <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> | Confirmed post-exploitation access via `sysinfo` in the Meterpreter session (target OS: Metasploitable 2, Linux kernel, PHP/Linux Meterpreter). |

---

# Result

<div align="center">

<img src="https://img.shields.io/badge/SECURITY%20BYPASS-CONFIRMED-9A6700?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/RCE-ACHIEVED-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/METERPRETER-ACCESS-8250DF?style=for-the-badge&logoColor=white" />

</div>

- Successfully bypassed high-level security controls
- Achieved Remote Code Execution (RCE)
- Gained Meterpreter shell access on the target

---

# Remediation Recommendations

| Recommendation | Purpose |
|---|---|
| **Content / MIME-Type Validation** | Validate uploaded files by content/MIME-type inspection (magic bytes), not filename extension |
| **Disable Script Execution** | Store uploads outside the web root, or serve them from a location with script execution disabled |
| **Server-Side File Renaming** | Rename uploaded files server-side and strip/ignore client-supplied extensions |
| **Strict Allow-List** | Apply a strict allow-list of permitted file types rather than a deny-list |

---

# Environment Disclaimer

> **Controlled Web Application Security Laboratory Exercise**

This assessment was performed against DVWA running on an isolated Metasploitable 2 instance inside a controlled VirtualBox lab environment. No unauthorized systems were accessed.

---

# Evidence

Full walkthrough with screenshots:

### [DVWA File Upload Security Bypass — Evidence Report](./dvwa-fileupload-bypass-evidence.pdf)

---

<div align="center">

### Web Application Security · File Upload Testing · Vulnerability Assessment

</div>
