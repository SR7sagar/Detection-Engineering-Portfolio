# Azure Sentinel SOC Lab – End-to-End Detection Pipeline

This lab demonstrates a complete cloud-native detection engineering workflow using Azure Monitor, Microsoft Sentinel, and automated response via Logic Apps.

---

# 1. Architecture Overview

Custom Authentication Logs  
        ↓  
Logs Ingestion API  
        ↓  
Data Collection Endpoint (DCE)  
        ↓  
Data Collection Rule (DCR)  
        ↓  
Custom Log Table (AuthSimulation_CL)  
        ↓  
Scheduled Analytics Rule (5 min frequency / 15 min lookback)  
        ↓  
Incident Creation  
        ↓  
Automation Rule (Trigger: Incident Created)  
        ↓  
Logic App Playbook  
        ↓  
Automated Incident Comment Enrichment  

---

# 2. Environment Configuration

Resource Group: `sentinel-lab-rg`  
Workspace: `sentinel-lab-workspace`  
Region: UK South  

Data Collection Endpoint (DCE):  
- Used for secure ingestion endpoint  
- Region-aligned with workspace  

Data Collection Rule (DCR):  
- Stream: `Custom-AuthSimulationRaw`  
- Destination: Log Analytics  
- Table: `AuthSimulation_CL`  

---

# 3. Custom Log Ingestion Validation

Data was sent using Azure Logs Ingestion API:

```bash
curl -X POST https://<dce>.ingest.monitor.azure.com/dataCollectionRules/<dcr-id>/streams/Custom-AuthSimulationRaw?api-version=2023-01-01 \
  -H "Authorization: Bearer <JWT token>" \
  -H "Content-Type: application/json" \
  --data-binary @brute-live.json

Successful ingestion response:

HTTP/2 204

Validation Query:

AuthSimulation_CL
| order by TimeGenerated desc
| take 20

Confirmed:

EventID 4625 (failed logon)

EventID 4624 (successful logon)

AccountName

IpAddress

LogonType

Status

---
