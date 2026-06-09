🛡️ Cloud-Native SIEM — Microsoft Azure Sentinel & Azure Monitor

Internship Project | SMARTOVATE LTD | June – July 2026
Author: Abdelkhalek Bakkari
Duration: 2 months


📌 Project Overview
Designed and deployed a cloud-native Security Information and Event Management (SIEM) infrastructure on Microsoft Azure. The goal was to build a fully operational SOC (Security Operations Center) pipeline — from centralized log ingestion to automated incident response — using Azure Monitor, Microsoft Sentinel, and Azure Logic Apps.
This project addresses real-world cloud security challenges by replacing traditional perimeter-based security with a modern, intelligent, and automated detection and response system.

🎯 Objectives

✅ Deploy and configure a Log Analytics Workspace for centralized log collection
✅ Activate Microsoft Sentinel and connect native Microsoft data sources
✅ Develop custom KQL detection rules for real-world threat scenarios
✅ Build interactive security Workbooks for SOC visibility
✅ Design and deploy SOAR Playbooks for automated incident response


🏗️ Architecture
┌─────────────────────────────────────────────────────┐
│                   Data Sources                       │
│  Azure AD │ Office 365 │ Azure Activity │ VMs/FW    │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│            Azure Monitor & Log Analytics             │
│         (Log collection, storage, indexing)          │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│              Microsoft Sentinel (SIEM)               │
│   Analytics Rules │ Workbooks │ Incident Management  │
└──────────┬──────────────────────────┬───────────────┘
           │                          │
           ▼                          ▼
┌─────────────────┐        ┌─────────────────────────┐
│  KQL Detection  │        │   Azure Logic Apps       │
│     Rules       │        │   (SOAR Playbooks)       │
└─────────────────┘        └──────────┬──────────────┘
                                      │
                           ┌──────────┴──────────┐
                           ▼                     ▼
                     Microsoft Teams       Azure AD
                     (Notifications)   (Account Remediation)

🔧 Technologies Used
CategoryTechnologySIEM PlatformMicrosoft SentinelLog ManagementAzure Monitor & Log AnalyticsQuery LanguageKQL (Kusto Query Language)Automation / SOARAzure Logic AppsIdentity SourceAzure Active Directory (Entra ID)Remediation APIMicrosoft Graph APINotificationMicrosoft Teams / Exchange OnlineInfrastructure as CodeBicep / Terraform

📋 Project Scope
✅ In Scope

Azure Monitor and Log Analytics Workspace configuration
Microsoft Sentinel activation and native connector integration
5–10 custom KQL detection rules
2 Security Workbooks (Security Overview + Identity Analysis)
2 SOAR Playbooks (Teams/Email Notification + Account Disabling)
Full technical documentation

❌ Out of Scope

Complex on-premise data source integration
Custom REST API connectors for third-party tools
Production incident response (sandbox/test environment only)


🔍 Detection Rules (KQL)
Rule 1 — Suspicious Sign-In from Unknown Location
Detects successful logins from IP addresses or countries outside the authorized baseline.
kqlSigninLogs
| where ResultType == "0"
| where Location !in ("TN", "FR", "GB")
| project TimeGenerated, UserPrincipalName, Location, IPAddress
| order by TimeGenerated desc
Rule 2 — Privilege Escalation Detection
Alerts when a user is added to a Global Administrator role in Azure AD.
kqlAuditLogs
| where OperationName == "Add member to role"
| where TargetResources contains "Global Administrator"
| project TimeGenerated, InitiatedBy, TargetResources
| order by TimeGenerated desc

All rules are scheduled (e.g., every hour), mapped to MITRE ATT&CK techniques, and configured with entity mapping (Account, IP, Host).


📊 Security Workbooks
Workbook 1 — Security Overview Dashboard

Failed sign-in trends by reason
Geographic map of login origins
Time-based filters (24h, 7 days, 30 days)
Top targeted accounts

Workbook 2 — Identity Posture Analysis

Authentication failure analysis
Privileged role assignments over time
Risky user behavior summary


⚡ SOAR Playbooks (Azure Logic Apps)
Playbook 1 — High Severity Incident Notification
Trigger: Microsoft Sentinel Incident (Severity = High)
Actions:

Extract incident details (Title, Severity, Description, Link)
Format an Adaptive Card
Post message to dedicated Microsoft Teams channel
Linked via Sentinel Automation Rule

Playbook 2 — Compromised Account Remediation
Trigger: Microsoft Sentinel Alert / Incident (Manual or Automatic)
Actions:

Identify the compromised account entity
Call Microsoft Graph API to revoke all active sessions
Disable the user account in Azure AD
Add a comment to the Sentinel incident confirming the action


🗓️ Project Timeline
WeekPhaseKey Deliverables1–2Setup & OnboardingLog Analytics Workspace, Sentinel activation3–4Data Collection & VisualizationData connectors, Security Workbooks5–6Detection & AlertingKQL rules, Analytics Rules, Incident generation7Automation & SOARLogic Apps Playbooks, end-to-end testing8Documentation & HandoverTechnical docs, final presentation

🐛 Known Issues & Fixes
Issue 1 — Log Ingestion Delay
Problem: Azure AD logs can take 15–30 minutes to appear in Log Analytics, causing missed alerts.
Fix: Use ingestion_time() instead of TimeGenerated in KQL lookback windows.
Issue 2 — Playbook 403 Forbidden Error
Problem: Account remediation Playbook fails with permission error when calling Azure AD.
Fix: Assign User.ReadWrite.All permission to the Logic App Managed Identity and grant the Authentication Administrator role.
Issue 3 — False Positive Overload
Problem: Poorly filtered KQL rules generate hundreds of incidents for legitimate behavior.
Fix: Implement Sentinel Watchlists to exclude known service accounts and trusted IP ranges from detection rules.

📁 Repository Structure
📦 siem-azure-sentinel
 ┣ 📂 detection-rules/        # KQL Analytics Rules (.kql files)
 ┣ 📂 workbooks/              # Workbook JSON templates
 ┣ 📂 playbooks/              # Logic Apps ARM templates
 ┣ 📂 infrastructure/         # Bicep / Terraform IaC files
 ┣ 📂 docs/                   # Technical documentation
 ┃  ┣ 📄 architecture.md
 ┃  ┣ 📄 deployment-guide.md
 ┃  └── 📄 exploitation-guide.md
 ┗ 📄 README.md

📚 References & Resources

Microsoft Sentinel Documentation
KQL Quick Reference
Azure Logic Apps Documentation
MITRE ATT&CK Framework
Microsoft Graph API


🏅 Related Certifications

AZ-900 — Microsoft Azure Fundamentals
SC-900 — Microsoft Security, Compliance and Identity Fundamentals
SC-200 — Microsoft Security Operations Analyst (in progress)


📬 Contact
Abdelkhalek Bakkari
CEO & Founder, SMARTOVATE LTD
📧 [your.email@example.com]
🔗 [linkedin.com/in/yourprofile]

This project was conducted in a sandbox/test environment. No real production data or systems were involved.
