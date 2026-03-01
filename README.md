# 🛡 Detection Engineering Portfolio

This repository showcases practical, production-style detection engineering projects built using structured threat modeling, MITRE ATT&CK alignment, and real-world SOC workflows.

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

Project files:
