<div align="center">

# 🛡️ Penetration Testing Lab Writeups

### `Offensive Security` · `Vulnerability Assessment` · `Network Security`

<img src="https://img.shields.io/badge/CEH-Certified-ff003c?style=for-the-badge&labelColor=0d1117" />
<img src="https://img.shields.io/badge/Penetration%20Testing-Active-00ff9d?style=for-the-badge&labelColor=0d1117" />
<img src="https://img.shields.io/badge/Kali%20Linux-Lab-557c94?style=for-the-badge&labelColor=0d1117" />
<img src="https://img.shields.io/badge/VirtualBox-Isolated%20Environment-8b5cf6?style=for-the-badge&labelColor=0d1117" />

<br><br>

> **A practical cybersecurity portfolio documenting penetration testing, vulnerability assessment, network reconnaissance, web application security, payload analysis, and Windows security labs.**

</div>

---

# 🔐 Lab Overview

<table>
<tr>
<td width="50%" valign="top">

### 🎯 Security Focus

**Penetration Testing**
**Vulnerability Assessment**
**Network Reconnaissance**
**Web Application Security**
**Windows Security**
**OSINT & Reconnaissance**
**Payload & Malware Analysis**
**Post-Exploitation**

</td>

<td width="50%" valign="top">

### 🧪 Laboratory Environment

**Primary OS:** Kali Linux
**Virtualization:** VirtualBox
**Target Systems:** Windows VMs / DVWA
**Network:** Isolated Lab Network
**Analysis:** Wireshark
**Web Testing:** Burp Suite

</td>
</tr>
</table>

<br>

<div align="center">

```text
        🔎 RECON
           │
           ▼
      ENUMERATION
           │
           ▼
   VULNERABILITY ASSESSMENT
           │
           ▼
      EXPLOITATION
           │
           ▼
    POST-EXPLOITATION
           │
           ▼
   EVIDENCE & ANALYSIS
           │
           ▼
      REPORTING
```

</div>

This repository contains structured penetration testing labs completed during cybersecurity training at **Corvit Institute under the NAVTTC-funded program**, alongside self-directed hands-on practice.

All practical work was performed in **controlled and isolated VirtualBox environments** for cybersecurity education and authorized security testing.

---

# ⚔️ Penetration Testing Labs

## 🔴 Exploitation & Vulnerability Assessment

|   ID   | Assessment                                                                               | Technologies                                            |
| :----: | ---------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| **01** | 🔴 **[SMB MS08-067 Vulnerability Assessment](SMB_MS08_067_Vulnerability_Assessment.md)** | `Nmap` · `Metasploit` · `SMB` · `Windows`               |
| **02** | 🔐 **[DVWA Authentication Bypass](dvwa-auth-bypass.md)**                                 | `Burp Suite Proxy` · `Burp Intruder` · `Kali Linux`     |
| **03** | 📤 **[DVWA File Upload Bypass](dvwa-fileupload-bypass.md)**                              | `Burp Suite` · `Metasploit` · `msfvenom` · `Kali Linux` |
| **04** | 🌐 **[DVWA Reflected XSS Assessment](dvwa-reflected-xss-report.md)**                     | `DVWA` · `Burp Suite` · `XSS`                           |

---

## 🧬 Payload Delivery & Malware Research

|   ID   | Assessment                                                                                   | Technologies                                                                    |
| :----: | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **05** | 🧬 **[Fileless Malware Delivery — CAPTCHA Technique](fileless-malware-delivery-captcha.md)** | `Kali Linux` · `Metasploit` · `Apache` · `msfvenom` · `HTA/mshta` · `Windows`   |
| **06** | 📊 **[Macro-Based Malware Delivery](macro-based-malware-delivery.md)**                       | `Kali Linux` · `Unicorn` · `Metasploit` · `Microsoft Excel` · `VBA` · `Windows` |
| **07** | 🎯 **[Meterpreter Payload Delivery Workflow](meterpreter-payload-delivery-workflow.md)**     | `msfvenom` · `Meterpreter` · `Apache2` · `PDF Artifact Preparation`             |

---

## 🌐 Network & Session Security

|   ID   | Assessment                                                                                   | Technologies                                                     |
| :----: | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **08** | 🔎 **[Nmap Network Reconnaissance](nmap-network-reconnaissance-report.md)**                  | `Nmap` · `Wireshark` · `Kali Linux`                              |
| **09** | 🍪 **[Session Hijacking — Cookie Injection](session-hijacking-cookie-injection-report.pdf)** | `Cookie Editor` · `Browser Exploitation` · `Session Tokens`      |
| **10** | 🪟 **[Windows Registry Persistence Assessment](windows-registry-persistence-assessment.md)** | `Windows Registry` · `Persistence Analysis` · `Windows Security` |

---

# 🧰 Tool Arsenal

## 🔎 Reconnaissance & Enumeration

<img src="https://img.shields.io/badge/Nmap-0d1117?style=for-the-badge&logo=nmap&logoColor=00ff9d" />
<img src="https://img.shields.io/badge/Shodan-0d1117?style=for-the-badge&logoColor=00ff9d" />
<img src="https://img.shields.io/badge/Censys-0d1117?style=for-the-badge&logoColor=00ff9d" />
<img src="https://img.shields.io/badge/ZoomEye-0d1117?style=for-the-badge&logoColor=00ff9d" />
<img src="https://img.shields.io/badge/Maltego-0d1117?style=for-the-badge&logoColor=00ff9d" />

`SecurityTrails` · `IntelX` · `Google Dorking` · `WHOIS Analysis` · `wafw00f`

---

## 💥 Exploitation & Penetration Testing

<img src="https://img.shields.io/badge/Metasploit-0d1117?style=for-the-badge&logo=metasploit&logoColor=ff003c" />
<img src="https://img.shields.io/badge/msfvenom-0d1117?style=for-the-badge&logoColor=ff003c" />
<img src="https://img.shields.io/badge/Meterpreter-0d1117?style=for-the-badge&logoColor=ff003c" />
<img src="https://img.shields.io/badge/sqlmap-0d1117?style=for-the-badge&logoColor=ff003c" />

`MS08-067` · `MS17-010 / EternalBlue` · `SMB` · `Post-Exploitation`

---

## 🌐 Web Application Security

<img src="https://img.shields.io/badge/Burp_Suite-0d1117?style=for-the-badge&logo=burpsuite&logoColor=ff6633" />
<img src="https://img.shields.io/badge/DVWA-0d1117?style=for-the-badge&logoColor=ff6633" />

`SQL Injection` · `XSS` · `File Upload Bypass` · `Authentication Testing`
`Burp Proxy` · `Burp Intruder` · `Cluster Bomb` · `Cookie Editor`
`OWASP Top 10`

---

## 🛡️ Vulnerability Assessment

<img src="https://img.shields.io/badge/Nessus-0d1117?style=for-the-badge&logoColor=00ff9d" />
<img src="https://img.shields.io/badge/OpenVAS-0d1117?style=for-the-badge&logoColor=00ff9d" />

`CVE Research` · `Vulnerability Scanning` · `Service Enumeration` · `Risk Identification`

---

## 🌐 Network Security & Traffic Analysis

<img src="https://img.shields.io/badge/Wireshark-0d1117?style=for-the-badge&logo=wireshark&logoColor=00ff9d" />

`Ettercap` · `Bettercap` · `MITM` · `ARP Spoofing` · `DNS Spoofing`
`MAC Spoofing` · `Session Hijacking` · `Network Traffic Analysis`

---

## 🔑 Password & Credential Security

`Hydra` · `Brute Force` · `Dictionary Attacks` · `rockyou.txt`
`Hash Analysis` · `Credential Testing`

---

## 🧬 Malware Analysis & Delivery Research

<img src="https://img.shields.io/badge/Any.run-0d1117?style=for-the-badge&logoColor=ff003c" />
<img src="https://img.shields.io/badge/VirusTotal-0d1117?style=for-the-badge&logo=virustotal&logoColor=ff003c" />

`Unicorn` · `VBA` · `Microsoft Excel` · `HTA / mshta`
`msfvenom` · `Meterpreter` · `Apache2`
`Static Analysis` · `Dynamic Analysis` · `Hybrid Analysis`

---

## 🖥️ Operating Systems & Lab Infrastructure

<img src="https://img.shields.io/badge/Kali_Linux-0d1117?style=for-the-badge&logo=kalilinux&logoColor=557c94" />
<img src="https://img.shields.io/badge/Windows-0d1117?style=for-the-badge&logo=windows&logoColor=00a4ef" />
<img src="https://img.shields.io/badge/VirtualBox-0d1117?style=for-the-badge&logo=virtualbox&logoColor=8b5cf6" />
<img src="https://img.shields.io/badge/Apache2-0d1117?style=for-the-badge&logo=apache&logoColor=ffffff" />

---

# 🧠 Technical Capabilities

<table>
<tr>
<td width="50%" valign="top">

### Offensive Security

* Network reconnaissance
* Service enumeration
* Vulnerability assessment
* Exploitation methodology
* Web application testing
* Payload delivery simulation
* Post-exploitation analysis
* Windows persistence assessment

</td>

<td width="50%" valign="top">

### Security Research

* CVE research
* OWASP Top 10
* OSINT reconnaissance
* Malware analysis
* Network traffic analysis
* Session security testing
* Credential security testing
* Technical security reporting

</td>
</tr>
</table>

---

# 🛰️ Laboratory Architecture

<div align="center">

```text
                         ┌────────────────────┐
                         │     KALI LINUX     │
                         │  SECURITY PLATFORM │
                         └─────────┬──────────┘
                                   │
                           ISOLATED NETWORK
                                   │
                 ┌─────────────────┴─────────────────┐
                 │                                   │
                 ▼                                   ▼
        ┌──────────────────┐                ┌──────────────────┐
        │    WINDOWS VM    │                │    DVWA / WEB    │
        │                  │                │    APPLICATION   │
        │ SMB / Registry   │                │                  │
        │ Security Labs    │                │ Security Testing │
        └──────────────────┘                └──────────────────┘
                 │                                   │
                 └─────────────────┬─────────────────┘
                                   ▼
                         ┌────────────────────┐
                         │     WIRESHARK      │
                         │  TRAFFIC ANALYSIS  │
                         └────────────────────┘
```

</div>

---

# 📊 Skills Demonstrated

<div align="center">

| Security Area            |  Practical Exposure  |
| ------------------------ | :------------------: |
| Network Reconnaissance   | ████████████████████ |
| Vulnerability Assessment | ██████████████████░░ |
| Web Application Security | ██████████████████░░ |
| Exploitation Methodology | █████████████████░░░ |
| Network Security         | ████████████████░░░░ |
| Malware Analysis         | ███████████████░░░░░ |
| Windows Security         | ███████████████░░░░░ |
| Security Documentation   | ██████████████████░░ |

</div>

---

# 🎓 Certification

<div align="center">

## 🛡️ Certified Ethical Hacker — CEH

**EC-Council · Certified 2026**

<br>

**Cisco Junior Cybersecurity Analyst**
Cisco Networking Academy · 2026

<br>

**Cybersecurity Training Program**
NAVTTC · Corvit Institute, Rawalpindi · 2026

</div>

---

# ⚠️ Ethical Use & Disclaimer

> **AUTHORIZED SECURITY TESTING ONLY**

All practical activities documented in this repository were conducted in **isolated, controlled, and authorized training environments**.

This repository is intended for:

`Cybersecurity Education` · `Ethical Hacking` · `Authorized Testing` · `Security Research` · `Defensive Security`

**Never test systems, applications, networks, or accounts without explicit authorization.**

---

# 👨‍💻 About the Author

<div align="center">

## Muhammad Adeel Tariq

**Certified Ethical Hacker (CEH)**
**Cybersecurity Analyst | Penetration Testing | Vulnerability Assessment | OSINT**

Pakistan

<br>

<a href="https://github.com/adeel635">
<img src="https://img.shields.io/badge/GitHub-adeel635-0d1117?style=for-the-badge&logo=github&logoColor=ffffff" />
</a>

<a href="https://linkedin.com/in/muhammad-adeel-tariq56">
<img src="https://img.shields.io/badge/LinkedIn-Muhammad_Adeel_Tariq-0d1117?style=for-the-badge&logo=linkedin&logoColor=0a66c2" />
</a>

</div>

---

<div align="center">

```text
╔══════════════════════════════════════════════╗
║                                              ║
║       🔐 LEARN  •  TEST  •  DOCUMENT        ║
║                      ↓                       ║
║                    SECURE                    ║
║                                              ║
╚══════════════════════════════════════════════╝
```

### Building practical cybersecurity skills through authorized security labs and continuous hands-on learning.

</div>
