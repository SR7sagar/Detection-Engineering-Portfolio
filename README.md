# 🛡 Detection Engineering Portfolio

## 👤 Professional Profile

Security engineer focused on detection engineering, threat-informed analytics, and cloud-native SOC architecture.

Specialized in:

- Behavioral detection design (correlation-based logic)
- MITRE ATT&CK-aligned threat modeling
- Azure Sentinel analytics engineering
- Custom telemetry ingestion (DCE + DCR)
- SOAR automation design (Logic Apps)
- Azure IAM and service principal role scoping
- Cost-efficient cloud security architecture

This repository documents production-style detection engineering implementations aligned to structured threat modeling and real-world SOC operations.

It demonstrates capabilities across:

- Behavioral detection engineering
- Correlation-based analytics (KQL)
- Custom log ingestion (Azure Logs Ingestion API)
- Microsoft Sentinel analytics rules
- SOAR automation with Logic Apps
- Azure IAM troubleshooting
- Cost-aware cloud architecture design

---

# 🚀 Featured Project: End-to-End SOC Lab (Azure Sentinel)

A full cloud-native detection pipeline including ingestion, detection, incident creation, and automated enrichment.

📂 View full implementation:
➡️ [Azure Sentinel SOC Lab](./soc-lab/README.md)

### Key Capabilities Demonstrated

✔ Custom Data Collection Endpoint (DCE)  
✔ Data Collection Rule (DCR) engineering  
✔ Logs Ingestion API validation (HTTP 204)  
✔ Correlation-based brute force detection  
✔ Scheduled analytics rule deployment  
✔ Entity mapping for investigation graph  
✔ Automation rule (incident-created trigger)  
✔ Logic App playbook integration  
✔ IAM permission scoping & service principal role assignment  
✔ Detection coverage matrix (MITRE-aligned)  
✔ Operational metrics & reliability analysis  

This project reflects production-style SOC engineering beyond static detection examples.

---

# 📂 Detection Engineering Projects

## 1️⃣ Authentication Abuse – Multiple Failures Followed by Success

Detects brute force and password spraying behavior using Windows authentication telemetry.

- Correlation logic (4625 → 4624)
- Threshold-based aggregation
- IP + Account correlation
- MITRE ATT&CK: T1110, T1078

# Project files:

Project structure:

```
detections/
│
├── authentication_multiple_failures_then_success.yml
├── authentication_multiple_failures_then_success_investigation.md
└── README.md
```

---

# 📌 Investigation & Detection Approach

Each detection project includes:

- Behavioral logic explanation
- Detection methodology
- MITRE ATT&CK mapping
- Investigation guidance
- Tuning & validation considerations

This ensures detections are not just rule-based, but operationally actionable within a SOC environment.

---

# 📈 Portfolio Focus

This portfolio emphasizes:

- Detection engineering over alert volume
- Correlation logic over single-event matching
- Automation & SOAR integration
- Cloud-native architecture
- IAM and operational troubleshooting
- Threat coverage awareness

---

# 🧠 Engineering Philosophy

Effective detection engineering requires:

- Understanding attacker behavior
- Modeling realistic detection logic
- Validating ingestion pipelines
- Ensuring automation reliability
- Designing cost-efficient architectures

This repository reflects applied engineering principles, not theoretical examples.

---

## Technical Blog

I documented the complete implementation of this SOC detection engineering project in a technical article.

🔗 **Read the full article on Medium:**  
[Building a Cloud-Native SOC Detection Pipeline with Microsoft Sentinel](https://medium.com/@sagarsina58/building-a-cloud-native-soc-detection-pipeline-with-microsoft-sentinel-from-log-ingestion-to-9b29e21acf74)

---

# Author
Sagar Timalsina
