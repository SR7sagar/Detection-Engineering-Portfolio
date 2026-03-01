# 🚀 Azure Sentinel SOC Lab – End-to-End Detection Pipeline

This lab demonstrates a **cloud-native detection engineering workflow** using:

- Azure Monitor (Logs Ingestion API)
- Microsoft Sentinel
- Scheduled Analytics Rules
- Automation Rules
- Logic App Playbooks
- IAM Permission Engineering

This is not a static detection example — it is a full operational SOC pipeline.

---

# 🏗 Architecture Overview


Custom Authentication Logs
↓
Logs Ingestion API
↓
Data Collection Endpoint (DCE)
↓
Data Collection Rule (DCR)
↓
AuthSimulation_CL (Custom Log Table)
↓
Scheduled Analytics Rule (5 min frequency / 15 min lookback)
↓
Incident Creation
↓
Automation Rule (Incident Created Trigger)
↓
Logic App Playbook
↓
Automated Incident Comment Enrichment


---

# ⚙ Environment Configuration

**Resource Group:** `sentinel-lab-rg`  
**Workspace:** `sentinel-lab-workspace`  
**Region:** UK South  

### Data Collection Endpoint (DCE)

- Secure ingestion endpoint  
- Region-aligned with Log Analytics workspace  

### Data Collection Rule (DCR)

- Stream: `Custom-AuthSimulationRaw`  
- Destination: Log Analytics  
- Output table: `AuthSimulation_CL`  
- Schema fields:
  - TimeGenerated
  - EventID
  - AccountName
  - IpAddress
  - LogonType
  - Status

---

# 📥 Custom Log Ingestion Validation

Data sent via Azure Logs Ingestion API:

```bash
curl -X POST https://<dce>.ingest.monitor.azure.com/dataCollectionRules/<dcr-id>/streams/Custom-AuthSimulationRaw?api-version=2023-01-01 \
  -H "Authorization: Bearer <JWT token>" \
  -H "Content-Type: application/json" \
  --data-binary @brute-live.json
```

Successful response:

```bash
HTTP/2 204
```

Validation query:

```bash
AuthSimulation_CL
| order by TimeGenerated desc
| take 20
```

Confirmed ingestion of:

EventID 4625 (Failed logon)

EventID 4624 (Successful logon)

AccountName

IpAddress

LogonType

Status
```

🔎 Detection Engineering – Brute Force Correlation
🎯 Detection Objective

Identify multiple failed authentication attempts followed by a successful login from the same IP and account within a short time window.

🧠 Final Working KQL Query
```bash
AuthSimulation_CL
| where EventID in (4624,4625)
| summarize
    FailCount = countif(EventID == 4625),
    FirstFail = minif(TimeGenerated, EventID == 4625),
    LastFail  = maxif(TimeGenerated, EventID == 4625),
    FirstSuccess = minif(TimeGenerated, EventID == 4624)
  by AccountName, IpAddress
| where FailCount >= 5
| where isnotnull(FirstSuccess)
| where FirstSuccess between (FirstFail .. LastFail + 10m)
| project AccountName, IpAddress, FailCount, FirstFail, LastFail, FirstSuccess
| order by FirstSuccess desc
```

🧩 Detection Logic

Aggregate failed logons (EventID 4625)

Apply threshold (≥ 5 failures)

Identify successful logon (EventID 4624)

Ensure success occurred within 10 minutes after last failure

Correlate on AccountName + IpAddress

MITRE ATT&CK Mapping

T1110 – Brute Force

T1078 – Valid Accounts
```

📊 Analytics Rule Configuration

Rule Name:
Brute Force Followed by Successful Login (Custom Table)

Frequency: 5 minutes
Lookback: 15 minutes
Trigger Condition: Greater than 0 results

Entity Mapping

Account → AccountName

IP → IpAddress

Grouping Behavior

Alerts grouped into a single incident

Incident updated if rule re-triggers within grouping window
```

🤖 Automation & Playbook
Automation Rule

Trigger:
When incident is created

Condition:
Analytic rule name contains
"Brute Force Followed by Successful Login (Custom Table)"

Action:
Run playbook → Sentinel-BruteForce-Notify

Logic App Playbook

Trigger:
Microsoft Sentinel Incident (Preview)

Action:
Add comment to incident

Comment Template
Automated Response Triggered

Detection: Brute Force Followed by Successful Login
Account: dynamic AccountName
IP Address: dynamic IpAddress
Failure Count: dynamic FailCount

This incident was automatically enriched by SOC lab playbook.

Result:
Automated comment appears in the Incident Activity Log.
```

🔐 IAM & Permission Resolution
Problem

Playbook not selectable in automation rule due to insufficient permissions.

Root Cause

Azure Security Insights service principal lacked explicit role assignment at Logic App resource scope.

Fix Implemented

Assigned role:

Microsoft Sentinel Automation Contributor

Assigned to:

Azure Security Insights (Service Principal)

Scope:

Logic App resource (Sentinel-BruteForce-Notify)

Result:
Playbook became selectable and automation executed successfully.
```

🛠 Troubleshooting Log

Resolved the following engineering issues:

InvalidStream error (incorrect DCR stream)

InvalidToken error (expired Azure CLI token)

Tenant mismatch during token generation

Ingestion delay vs time-window mismatch

Incident grouping preventing automation trigger

Playbook permission inheritance issue
```

💰 Cost Control Strategy

No virtual machines used

Limited ingestion volume

Logic App deployed using Consumption plan

No continuous connectors enabled

Estimated total lab cost: < £5
```

✅ Validation Evidence

✔ HTTP 204 ingestion responses
✔ Detection query returned correlated results
✔ Incident created automatically
✔ Automation rule triggered
✔ Logic App executed
✔ Automated comment visible in Incident Activity Log
```

🏁 Conclusion

This lab demonstrates practical cloud-native detection engineering:

Custom ingestion engineering

Correlation-based detection logic

MITRE ATT&CK alignment

Sentinel analytics rule deployment

Automation & playbook integration

Azure IAM troubleshooting

Cost-aware architecture design

This implementation reflects real-world SOC engineering beyond static detection rules.
```
