# Detection Engineering Portfolio

---

## 🚀 SOC Lab — End-to-End Sentinel Implementation

This repository now includes a full Azure Sentinel SOC lab implementation:

- Custom log ingestion via Logs Ingestion API (DCE + DCR)
- Custom table ingestion validation (HTTP 204)
- Correlation-based brute force detection (KQL)
- Scheduled analytics rule (5-minute frequency)
- Automation rule (incident-created trigger)
- Logic App playbook with automated enrichment
- IAM troubleshooting and permission resolution

📂 Full lab documentation available here:
➡️ [SOC Lab Implementation](./soc-lab/README.md)

---
This repository contains structured detection engineering projects aligned with MITRE ATT&CK and real-world SOC investigation workflows.

Each project includes:
- Detection rule (Sigma format)
- Behavioral logic explanation
- Investigation methodology
- Validation & tuning considerations
- MITRE ATT&CK mapping

---

# Project 01 – Authentication Abuse Detection Engineering

## Objective

Design and document a behavioral detection rule to identify brute force and password spraying activity using Windows Security logs.

## Detection Logic

Correlates multiple failed logon attempts (Event ID 4625) followed by a successful logon (Event ID 4624) from the same IP address within a 5-minute window.

## MITRE Mapping

- T1110 – Brute Force  
- T1078 – Valid Accounts  

## Project Structure

```text
detections/
│
├── authentication_multiple_failures_then_success.yml
├── authentication_multiple_failures_then_success_investigation.md
└── README.md
```



