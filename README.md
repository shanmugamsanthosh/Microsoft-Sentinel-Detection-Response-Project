# 🛡️ Microsoft Sentinel Threat Detection & Response Lab

## 📖 Overview

This repository contains a complete **hands-on Microsoft Sentinel lab** designed to build practical Security Operations Center (SOC) skills. The lab walks through the full lifecycle of a modern SIEM/SOAR deployment on Azure:

- Environment setup and onboarding
- Data ingestion and connectors
- Threat intelligence and Indicators of Compromise (IoCs)
- Detection engineering with Analytics Rules
- Automated response using Playbooks and Automation Rules
- Real-world KQL hunting queries
- Security visualization with Workbooks and Watchlists

Every major step is documented with screenshots so you can follow along in your own Azure subscription (free trial or paid) and adapt the configuration to real environments.

---

## 📑 Table of Contents

1. [Initial Azure & Sentinel Setup](Sentinel-Set-Up.md)
2. [Integrating Data Connectors](Data-Connectors-in-Microsoft-Sentinel.md)
3. [Integrating Microsoft Defender & Creating Indicators of Compromise (IoCs)](Integrating-MS-Defender-and-IoC.md)
4. [Threat Detection (Analytics Rules)](Threat-Detection-(Analytics)-in-Sentinel.md)
5. [Playbooks and Logic Apps (SOAR Automation)](Playbooks-and-Logic-Apps-in-Microsoft-Sentinel.md)
6. [Automation Rules and Playbooks](Automation-Rules-and-Playbooks.md)
7. [Real-World KQL Queries](KQL-Queries-for-Microsoft-Sentinel.md)
8. [Visualizing Security Data with Workbooks](Visualize-Security-Data-in-MS-Sentinel.md)
9. [Real-World Application in a SOC](#-real-world-application-in-a-soc)
10. [Conclusion](#-conclusion)

---

## 🚀 Lab Modules

### 1. ⚙️ [Initial Azure & Sentinel Setup](Sentinel-Set-Up.md)

Foundation of the entire lab environment.

- Create a dedicated resource group (`rg-sentinel-homelab`)
- Deploy a Log Analytics workspace
- Enable Microsoft Sentinel on the workspace
- Create Windows and Linux virtual machines as log sources
- Configure Network Security Group (NSG) rules for RDP and SSH
- Verify the SecurityInsights solution and baseline permissions

This module produces a clean, isolated environment ready for data connectors and detection rules.

### 2. 🔗 [Integrating Data Connectors](Data-Connectors-in-Microsoft-Sentinel.md)

Ingest security telemetry from multiple sources.

- Install solutions from the Content Hub
- Configure Microsoft Defender for Cloud plans and monitoring
- Deploy Windows Security Events via Azure Monitor Agent (AMA)
- Create Data Collection Rules (DCRs) for event filtering and routing
- Configure Syslog via AMA for Linux sources

After this module, Sentinel begins receiving continuous security events required for analytics and hunting.

### 3. 🛡️ [Integrating Microsoft Defender & Creating Indicators of Compromise (IoCs)](Integrating-MS-Defender-and-IoC.md)

Enrich detection with Microsoft Defender and threat intelligence.

- Enable Microsoft Defender for Cloud plans
- Onboard Content Hub solutions (Defender, Azure Activity, Syslog, and others)
- Configure Windows Security Events and Syslog data connectors
- Create and verify Indicators of Compromise (IoCs)
- Validate that security events appear in Sentinel Logs

### 4. 🔍 [Threat Detection (Analytics Rules)](Threat-Detection-(Analytics)-in-Sentinel.md)

Build scheduled analytics rules that generate incidents.

- Use the Analytics rule wizard
- Write and test KQL detection queries
- Configure query scheduling, incident settings, and alert grouping
- Review and enable rules so they produce actionable incidents for the SOC

### 5. 🤖 [Playbooks and Logic Apps (SOAR Automation)](Playbooks-and-Logic-Apps-in-Microsoft-Sentinel.md)

Automate incident response with Logic Apps / Playbooks.

- Create incident-triggered playbooks
- Retrieve incident details, perform optional enrichment, create comments, and send email notifications
- Link playbooks to analytics rules for automated response

### 6. ⚡ [Automation Rules and Playbooks](Automation-Rules-and-Playbooks.md)

Additional automation capabilities for SOC efficiency.

- Create automation rules (for example, automatically change severity)
- Use and customize Sentinel Automation templates
- Automate incident status changes and other repetitive tasks

### 7. 📝 [Real-World KQL Queries](KQL-Queries-for-Microsoft-Sentinel.md)

Practical KQL queries used for threat hunting and detection engineering:

1. Azure Sign-In Brute Force Detection
2. Unusual User Sign-in Locations
3. Elevation of Privileges in Azure AD
4. Linux SSH Brute Force (VM)
5. Windows Brute Force (VM)

Each query includes simulation guidance and verification screenshots.

### 8. 📊 [Visualizing Security Data with Workbooks](Visualize-Security-Data-in-MS-Sentinel.md)

- Create watchlists (sample geo-IP CSV files are included in the repository root)
- Build and use Security Operations Overview workbooks
- View metrics, severity breakdowns, trends, and geographic attack maps

---

## 🌐 Real-World Application in a SOC

These modules mirror day-to-day tasks performed by SOC analysts and detection engineers:

| SOC Task                          | Module that covers it                           |
|-----------------------------------|-------------------------------------------------|
| Environment & data onboarding     | Setup + Data Connectors                         |
| Threat intelligence enrichment    | Defender & IoC                                  |
| Detection engineering             | Analytics Rules + KQL Queries                   |
| Incident response automation      | Playbooks / Logic Apps + Automation Rules       |
| Reporting & situational awareness | Workbooks + Watchlists                          |

Skills gained transfer directly to production Microsoft Sentinel and Microsoft Defender XDR deployments.

---

## ✅ What You Will Have Completed

By finishing this lab you will have:

- Deployed a fully functional Microsoft Sentinel workspace
- Connected multiple data sources and threat feeds
- Written and tuned analytics rules and hunting queries
- Built automated response playbooks and automation rules
- Created security visualization workbooks and watchlists

The repository is intentionally practical: every major configuration step is documented with screenshots so you can follow along or adapt the labs to your own environment.

Happy hunting!

---

## 📁 Repository Structure

```
.
├── README.md
├── Sentinel-Set-Up.md
├── Data-Connectors-in-Microsoft-Sentinel.md
├── Integrating-MS-Defender-and-IoC.md
├── Threat-Detection-(Analytics)-in-Sentinel.md
├── Playbooks-and-Logic-Apps-in-Microsoft-Sentinel.md
├── Automation-Rules-and-Playbooks.md
├── KQL-Queries-for-Microsoft-Sentinel.md
├── Visualize-Security-Data-in-MS-Sentinel.md
├── geoip-summarized-1.csv          # Sample watchlist data
├── geoip-summarized-2.csv          # Sample watchlist data
└── images/
    ├── Sentinel-Set-Up/
    ├── Data-Connectors-in-Microsoft-Sentinel/
    ├── Integrating-MS-Defender-and-IoC/
    ├── Threat-Detection-(Analytics)-in-Sentinel/
    ├── Playbooks-and-Logic-Apps-in-Microsoft-Sentinel/
    ├── Visualize-Security-Data-in-MS-Sentinel/
    └── KQL-Queries/
```

## 🔧 Resource Naming Used in the Lab

| Resource                    | Name used in screenshots / docs      |
|-----------------------------|--------------------------------------|
| Resource Group              | `rg-sentinel-homelab`                |
| Log Analytics Workspace     | `law-sentinel-homelabs` / `loganalysis-homelab2` |
| Region                      | East US                              |
| Subscription                | Azure subscription 1                 |

> **Note:** Workspace names must be globally unique. If a name is already taken, append a unique suffix.
