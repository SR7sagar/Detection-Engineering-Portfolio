# SOC Lab (Azure Sentinel) — End-to-End Detection Engineering

This folder documents the complete SOC lab implementation:
custom log ingestion via Logs Ingestion API (DCE/DCR) into Log Analytics,
a scheduled analytics rule in Microsoft Sentinel, and automated response using
an automation rule + Logic App playbook.

## What’s Included
- Ingestion pipeline (DCE, DCR, custom stream → custom table)
- Test data simulation and validation (HTTP 204, KQL confirmation)
- Detection logic (KQL rule) and analytics rule configuration
- Automation rule and playbook (Logic App) with IAM permission fix
- Troubleshooting notes and cost control decisions

## Lab Resources (High Level)
- Log Analytics Workspace: `sentinel-lab-workspace`
- Resource Group: `sentinel-lab-rg`
- DCE: `sentinel-lab-dce`
- DCR (custom ingestion): `sentinel-lab-dcr-direct`
- Custom table: `AuthSimulation_CL`
- Playbook: `Sentinel-BruteForce-Notify`
- Automation rule: `BruteForce-Incident-AutoComment`
