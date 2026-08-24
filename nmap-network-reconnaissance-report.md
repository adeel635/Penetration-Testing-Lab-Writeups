
<div align="center">

# 🔎 Nmap CTF — Academic Network Reconnaissance Lab

### `Network Reconnaissance` · `Nmap` · `Service Enumeration` · `Firewall Evasion`

<br>

<img src="https://img.shields.io/badge/Controlled-Lab%20Assessment-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Nmap-Reconnaissance-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/CTF-Academic%20Challenge-9A6700?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Environment-VirtualBox%20Lab-1A7F37?style=for-the-badge&logoColor=white" />

<br><br>

> **A structured, flag-based Nmap challenge completed as part of academic cybersecurity training, progressing from basic host discovery to service enumeration, OS fingerprinting, firewall evasion, and web-service reconnaissance.**

</div>

---

## Overview

A structured, flag-based Nmap challenge completed as part of academic cybersecurity training.

The practical focuses on progressively advanced network reconnaissance techniques — from basic host discovery and port scanning to service detection, OS fingerprinting, firewall evasion, and web-service enumeration.

---

## Objective

Perform a complete reconnaissance workflow against a controlled lab target using Nmap:

- Discover live hosts
- Identify open ports
- Enumerate services and versions
- Fingerprint the operating system
- Perform aggressive reconnaissance
- Test basic firewall-evasion techniques
- Enumerate web application attack surface
- Export scan results for reporting
- Capture a flag at each stage to validate findings

---

## Lab Environment

| Component | Configuration |
|---|---|
| **Target** | Metasploitable — isolated VirtualBox lab |
| **Target IPs** | `192.168.88.20` / `192.168.88.253` |
| **Attacker Host** | Kali Linux |
| **Primary Tool** | Nmap |
| **Traffic Analysis** | Wireshark |
| **Setting** | Controlled Lab Environment |
| **Training Context** | NAVTTC-funded academic training, Corvit Institute |

---

## Tools Used

<div align="center">

<img src="https://img.shields.io/badge/Nmap-Network%20Scanning-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Wireshark-Traffic%20Analysis-0969DA?style=for-the-badge&logo=wireshark&logoColor=white" />
<img src="https://img.shields.io/badge/Kali-Linux-1A7F37?style=for-the-badge&logo=kalilinux&logoColor=white" />

</div>

---

# Methodology & Results

| # | Task | Command | Finding | Flag |
|:---:|---|---|---|---|
| **01** | **Basic Host Discovery** | `nmap -sn 192.168.88.20` | Host confirmed up with `0.094s` latency | `host-up` |
| **02** | **Identify Web Services** | `nmap -p 21,80,443 192.168.88.20` | `21/tcp` (`ftp`) identified as open | `Open_port: 21/tcp` |
| **03** | **Full Port Sweep** | `nmap -p- 192.168.88.20` | 25 open ports identified, including 5 high-numbered ports | `HIDDEN_PORT: 8180, 39837, 44440, 46088, 54154` |
| **04** | **Service Version Detection** | `nmap -sV 192.168.88.20` | Port `8180` running Apache Tomcat/Coyote JSP engine 1.1 | `SERVICE_VERSION: Apache Tomcat/Coyote JSP engine 1.1` |
| **05** | **OS Fingerprinting** | `nmap -O 192.168.88.20` | Linux kernel `2.6.9 – 2.6.33` identified | `SERVICE_VERSION: linux 2.6.9 - 2.6.33` |
| **06** | **Aggressive Recon** | `nmap -A 192.168.88.253` | Hostname identified through SMB/NetBIOS enumeration | `host-name: metasploitable` |
| **07** | **Save Results** | `nmap -oX m-adeel-tariq.xml ...` | Scan results exported to XML for reporting | `m-adeel-tariq.xml` |
| **08** | **—** | — | Not captured in the source document | — |
| **09** | **Firewall Evasion** | `nmap -f 192.168.88.253` | Packet fragmentation bypassed filtering on port `8180` | `EVADED: 8180` |
| **10** | **NSE Script Enumeration** | `nmap --script http-enum` | Multiple admin-panel paths and FCKeditor file-upload endpoints identified | `9/10 flags — enumeration complete` |

---

# Reconnaissance Progression

```text
Host Discovery
      ↓
Port Enumeration
      ↓
Service Detection
      ↓
OS Fingerprinting
      ↓
Aggressive Reconnaissance
      ↓
Result Export
      ↓
Firewall Evasion
      ↓
Web / NSE Enumeration
````

---

# Key Findings

|                                                  Status                                                 | Finding                                                                                                                    |
| :-----------------------------------------------------------------------------------------------------: | -------------------------------------------------------------------------------------------------------------------------- |
|  <img src="https://img.shields.io/badge/25%20OPEN%20PORTS-9A6700?style=flat-square&logoColor=white" />  | The target exposed an unusually high number of open services, consistent with an intentionally vulnerable laboratory host. |
|   <img src="https://img.shields.io/badge/LEGACY%20SERVICE-8250DF?style=flat-square&logoColor=white" />  | Version detection identified **Apache Tomcat/Coyote JSP engine 1.1** on non-standard port `8180`.                          |
|     <img src="https://img.shields.io/badge/LEGACY%20OS-8250DF?style=flat-square&logoColor=white" />     | OS fingerprinting indicated an outdated **Linux 2.6.x kernel** range.                                                      |
|  <img src="https://img.shields.io/badge/WEB%20ENUMERATION-0969DA?style=flat-square&logoColor=white" />  | NSE `http-enum` surfaced multiple exposed administrative paths and an FCKeditor file-upload endpoint.                      |
| <img src="https://img.shields.io/badge/EVASION%20VALIDATED-CF222E?style=flat-square&logoColor=white" /> | Packet fragmentation using `-f` was reported as sufficient to bypass filtering on port `8180` in the lab environment.      |
|      <img src="https://img.shields.io/badge/REPORTING-1A7F37?style=flat-square&logoColor=white" />      | Nmap results were exported to XML, providing structured output for later analysis and reporting.                           |

---

# CTF Flag Summary

| Stage                | Flag / Evidence                       |
| -------------------- | ------------------------------------- |
| **Host Discovery**   | `host-up`                             |
| **Open Port**        | `Open_port: 21/tcp`                   |
| **Hidden Ports**     | `8180, 39837, 44440, 46088, 54154`    |
| **Service Version**  | `Apache Tomcat/Coyote JSP engine 1.1` |
| **OS Fingerprint**   | `linux 2.6.9 - 2.6.33`                |
| **Hostname**         | `metasploitable`                      |
| **XML Output**       | `m-adeel-tariq.xml`                   |
| **Firewall Evasion** | `EVADED: 8180`                        |
| **NSE Enumeration**  | `9/10 flags — enumeration complete`   |

---

# What I Learned

This practical demonstrated the progressive application of Nmap across a complete reconnaissance lifecycle:

```text
Discovery → Enumeration → Fingerprinting → Evasion → Web Recon
```

It reinforced how different Nmap scan types provide progressively deeper visibility into a target and how structured output formats such as XML can support technical reporting and evidence preservation.

---

# Environment Disclaimer

> **Controlled Cybersecurity Laboratory Exercise**

All scanning was performed against an isolated, intentionally vulnerable **Metasploitable** lab target inside a controlled VirtualBox environment as part of structured academic training.

No unauthorized systems were accessed.

---

# Evidence

Full walkthrough with screenshots:

### [Nmap Network Reconnaissance Report](./nmap-network-reconnaissance-report.pdf)

---

<div align="center">

<img src="https://img.shields.io/badge/Network-Reconnaissance-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Nmap-CTF%20Lab-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Technical-Documentation-9A6700?style=for-the-badge&logoColor=white" />

<br><br>

### Network Security · Reconnaissance · Practical Testing

</div>
