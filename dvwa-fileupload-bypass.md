# DVWA File Upload Security Bypass — Remote Code Execution

## Overview

Assessment of DVWA's file-upload feature under the application's High security setting, 
to determine whether server-side validation could be bypassed to achieve code execution.

## Objective

To bypass file upload restrictions implemented at the High security level and achieve 
remote code execution on the target system.

## Lab Environment

- **Attacker Machine:** Kali Linux
- **Target Machine:** Metasploitable 2
- **Web Application:** DVWA (Damn Vulnerable Web Application)
- **Security Level:** High

## Tools Used

`Burp Suite` · `Metasploit Framework (msfconsole)` · `msfvenom` · `Kali Linux`

## Vulnerability Identified

**Improper File Upload Validation (CWE-434: Unrestricted Upload of File with 
Dangerous Type)**

The application failed to properly validate uploaded files on the server side, allowing 
bypass via a double file extension (e.g., `.php.jpg`).

## Methodology

| Step | Action |
|---|---|
| 1 | Generated a malicious PHP payload with `msfvenom` (`php/meterpreter/reverse_tcp`) |
| 2 | Configured a listener in `msfconsole` (`exploit/multi/handler`) |
| 3 | Attempted direct upload of the `.php` payload — rejected by server-side filtering |
| 4 | Enabled Burp Suite and turned Intercept ON |
| 5 | Re-uploaded the file and captured the request in Burp |
| 6 | Modified the filename in-flight to `shell.php.jpg` to bypass extension filtering |
| 7 | Forwarded the modified request — upload succeeded |
| 8 | Accessed the uploaded file directly via browser |
| 9 | Payload executed — Meterpreter session established |

## Key Findings

- Server-side validation relied on filename/extension inspection alone, which was 
  bypassed by appending a trailing `.jpg` to a `.php` payload.
- Once uploaded, the file remained directly web-accessible with no execution 
  restrictions on the uploads directory, allowing immediate code execution on request.
- Confirmed post-exploitation access via `sysinfo` in the Meterpreter session 
  (target OS: Metasploitable 2, Linux kernel, PHP/Linux Meterpreter).

## Result

- Successfully bypassed high-level security controls
- Achieved Remote Code Execution (RCE)
- Gained Meterpreter shell access on the target

## Remediation Recommendations

- Validate uploaded files by content/MIME-type inspection (magic bytes), not filename extension
- Store uploads outside the web root, or serve them from a location with script execution disabled
- Rename uploaded files server-side and strip/ignore client-supplied extensions
- Apply a strict allow-list of permitted file types rather than a deny-list

## Environment Disclaimer

This assessment was performed against DVWA running on an isolated Metasploitable 2 
instance inside a controlled VirtualBox lab environment. No unauthorized systems were 
accessed.

## Evidence

Full walkthrough with screenshots: [dvwa-fileupload-bypass-evidence.pdf](./dvwa-fileupload-bypass-evidence.pdf)
