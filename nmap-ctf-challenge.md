# Nmap CTF — Academic Network Reconnaissance Lab

## Overview

A structured, flag-based Nmap challenge completed as part of academic cybersecurity 
training, focused on progressively advanced network scanning techniques — from basic 
host discovery to firewall evasion and web-service enumeration.

## Objective

Perform a complete reconnaissance workflow against a lab target using Nmap: discover 
live hosts, enumerate services, fingerprint the OS, evade basic filtering, and identify 
web-application attack surface — capturing a flag at each stage to validate findings.

## Lab Environment

- **Target:** Metasploitable (isolated VirtualBox lab)
- **Target IPs:** 192.168.88.20 / 192.168.88.253
- **Attacker Host:** Kali Linux
- **Setting:** Controlled Lab Environment — NAVTTC-funded academic training, Corvit Institute

## Tools Used

`Nmap` · `Wireshark` · `Kali Linux`

## Methodology & Results

| # | Task | Command | Finding | Flag |
|---|---|---|---|---|
| 1 | Basic host discovery | `nmap -sn 192.168.88.20` | Host confirmed up (0.094s latency) | `host-up` |
| 2 | Identify web services | `nmap -p 21,80,443 192.168.88.20` | Port 21/tcp (ftp) open | `Open_port: 21/tcp` |
| 3 | Full port sweep | `nmap -p- 192.168.88.20` | 25 open ports found, including 5 hidden high ports | `HIDDEN_PORT: 8180, 39837, 44440, 46088, 54154` |
| 4 | Service version detection | `nmap -sV 192.168.88.20` | Port 8180 running Apache Tomcat/Coyote JSP engine 1.1 | `SERVICE_VERSION: Apache Tomcat/Coyote JSP engine 1.1` |
| 5 | OS fingerprinting | `nmap -O 192.168.88.20` | Target running Linux kernel 2.6.9 – 2.6.33 | `SERVICE_VERSION: linux 2.6.9 - 2.6.33` |
| 6 | Aggressive recon | `nmap -A 192.168.88.253` | Hostname resolved via SMB/NetBIOS enumeration | `host-name: metasploitable` |
| 7 | Save results | `nmap -oX m-adeel-tariq.xml ...` | Full scan results exported to XML for reporting | `m-adeel-tariq.xml` |
| 8 | — | — | *(not captured in source document)* | — |
| 9 | Firewall evasion | `nmap -f 192.168.88.253` | Packet fragmentation successfully bypassed filtering on port 8180 | `EVADED: 8180` |
| 10 | NSE script enumeration | `nmap --script http-enum` | Discovered multiple admin-panel paths and vulnerable file-upload endpoints (FCKeditor) | 9/10 flags — enumeration complete |

## Key Findings

- Target exposed an unusually high number of open services (25) for a hardened system — 
  consistent with an intentionally vulnerable lab host.
- Version detection revealed **Apache Tomcat/Coyote 1.1** on a non-standard port (8180), 
  and an outdated **Linux 2.6.x kernel** — both indicative of legacy, unpatched software.
- NSE `http-enum` scan surfaced several **exposed admin login paths** and a **FCKeditor 
  file-upload endpoint** — a common vector for unauthenticated remote file upload attacks.
- Basic packet fragmentation (`-f`) was sufficient to bypass the target's filtering rules, 
  highlighting the limits of simple firewall configurations against evasion techniques.

## What I Learned

Practical application of Nmap's full scanning lifecycle — from stealth discovery to 
aggressive service fingerprinting — and how output formats (XML) and evasion flags 
support both reporting and real-world reconnaissance workflows.

## Environment Disclaimer

All scanning was performed against an isolated, intentionally vulnerable lab target 
(Metasploitable) inside a controlled VirtualBox environment as part of structured 
academic training. No unauthorized systems were accessed.

## Evidence

Full terminal screenshots for all tasks: [nmap-ctf-week3-evidence.pdf](./nmap-ctf-week3-evidence.pdf)
