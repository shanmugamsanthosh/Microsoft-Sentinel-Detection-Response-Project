# 🛡️ Microsoft Sentinel Detection & Response Projects

## 📖 Overview

This repository contains a collection of **hands-on Microsoft Sentinel projects** that demonstrate practical Security Operations Center (SOC) skills. The labs walk through the full lifecycle of a modern SIEM/SOAR deployment: environment setup, data ingestion, threat intelligence, detection analytics, automated response, and security visualization.

Each project is designed as a self-contained lab you can follow in your own Azure subscription (free trial or paid). Screenshots and step-by-step instructions are included so you can reproduce the configuration and understand the underlying concepts.

**Author:** [Shanmugam Santhosh](https://github.com/shanmugamsanthosh)

---

## 📑 Table of Contents

1. [Initial Azure & Sentinel Setup](Sentinel-Set-Up.md)
2. [Integrating Data Connectors](Data-Connectors-in-Microsoft-Sentinel.md)
3. [Integrating Microsoft Defender & Creating Indicators of Compromise (IoCs)](Integrating-MS-Defender-and-IoC.md)
4. [Threat Detection (Analytics Rules)](Threat-Detection-(Analytics)-in-Sentinel.md)
5. [Playbooks and Logic Apps (SOAR Automation)](Playbooks-and-Logic-Apps-in-Microsoft-Sentinel.md)
6. [Visualizing Security Data with Workbooks](Visualize-Security-Data-in-MS-Sentinel.md)
7. [Real-World Application in a SOC](#-real-world-application-in-a-soc)
8. [Conclusion](#-conclusion)

---

## 🚀 Projects

### 1. ⚙️ [Initial Azure & Sentinel Setup](Sentinel-Set-Up.md)

Foundation of the entire lab environment.

- Create a dedicated resource group (`rg-sentinel-homelab`)
- Deploy a Log Analytics workspace (`law-sentinel-homelabs`)
- Enable Microsoft Sentinel on the workspace
- Verify the SecurityInsights solution and baseline permissions

This project ensures you have a clean, isolated environment ready for data connectors and detection rules.

### 2. 🔗 [Integrating Data Connectors](Data-Connectors-in-Microsoft-Sentinel.md)

Ingest security telemetry from multiple sources.

- Install the Threat Intelligence solution from Content Hub
- Configure TAXII connectors (e.g., Pulsedive) for threat indicators
- Deploy Windows Security Events via Azure Monitor Agent (AMA)
- Create Data Collection Rules (DCRs) for event filtering and routing

After this lab, Sentinel begins receiving continuous security events required for analytics and hunting.

### 3. 🛡️ [Integrating Microsoft Defender & Creating Indicators of Compromise (IoCs)](Integrating-MS-Defender-and-IoC.md)

Enrich detection with threat intelligence.

- Connect Microsoft Defender data into Sentinel
- Manually create and manage Indicators of Compromise (IP, domain, URL, file hash)
- Apply Traffic Light Protocol (TLP) markings
- Correlate indicators with other data sources

You build a living threat-intelligence repository that feeds analytics rules and workbooks.

### 4. 🔍 [Threat Detection (Analytics Rules)](Threat-Detection-(Analytics)-in-Sentinel.md)

Detect malicious activity with KQL-based rules.

- Create scheduled analytics rules (e.g., brute-force detection)
- Configure near-real-time (NRT) rules where appropriate
- Set incident creation, alert grouping, and entity mapping
- Review and tune rule severity, thresholds, and suppression

This project turns raw logs into actionable incidents that SOC analysts can investigate.

### 5. 🤖 [Playbooks and Logic Apps](Playbooks-and-Logic-Apps-in-Microsoft-Sentinel.md)

Automate incident response (SOAR).

- Design automation rules that trigger on specific incidents
- Build Logic Apps playbooks (email notification, enrichment, remediation)
- Grant Microsoft Sentinel the required managed-identity permissions
- Test end-to-end playbook execution and troubleshoot common failures

Automation reduces mean time to respond (MTTR) and frees analysts for higher-value work.

### 6. 📊 [Visualizing Security Data with Workbooks](Visualize-Security-Data-in-MS-Sentinel.md)

Turn data into decision-ready dashboards.

- Create custom workbooks for alert trends, failed logons, and threat intelligence
- Add pie charts, time-series line charts, and bar charts
- Explore built-in Sentinel workbook templates
- Apply best practices for performance (Sentinel data lake, query optimization)

Workbooks provide both operational views for the SOC and executive-ready reporting.

---

## 🌐 Real-World Application in a SOC

These projects mirror day-to-day tasks performed by SOC analysts and detection engineers:

| SOC Task                        | Project that covers it                          |
|---------------------------------|-------------------------------------------------|
| Environment & data onboarding   | Setup + Data Connectors                         |
| Threat intelligence enrichment  | Defender & IoC                                  |
| Detection engineering           | Analytics Rules                                 |
| Incident response automation    | Playbooks / Logic Apps                          |
| Reporting & situational awareness | Workbooks                                     |

Skills gained transfer directly to production Microsoft Sentinel (or Microsoft Defender XDR) deployments.

---

## ✅ Conclusion

By completing this series you will have:

- Deployed a fully functional Microsoft Sentinel workspace
- Connected multiple data sources and threat feeds
- Written and tuned analytics rules
- Built automated response playbooks
- Created security visualization workbooks

The repository is intentionally practical: every major configuration step is documented with screenshots so you can follow along or adapt the labs to your own environment.

Happy hunting!  
Feel free to open issues or submit improvements.

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
├── Visualize-Security-Data-in-MS-Sentinel.md
└── images/
    ├── Sentinel-Set-Up/
    ├── Data-Connectors-in-Microsoft-Sentinel/
    ├── Integrating-MS-Defender-and-IoC/
    ├── Threat-Detection-(Analytics)-in-Sentinel/
    └── Playbooks-and-Logic-Apps-in-Microsoft-Sentinel/
```

## 🔧 Resource Naming Used in Labs

| Resource                    | Name used in screenshots / docs      |
|-----------------------------|--------------------------------------|
| Resource Group              | `rg-sentinel-homelab`                |
| Log Analytics Workspace     | `law-sentinel-homelabs`              |
| Region                      | East US                              |
| Subscription                | Azure subscription 1                 |

> **Note:** Workspace names must be globally unique. If `law-sentinel-homelabs` is already taken, append a unique suffix.
