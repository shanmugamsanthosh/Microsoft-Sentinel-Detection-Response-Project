# Threat Detection (Analytics) in Microsoft Sentinel

## Overview

Microsoft Sentinel Analytics Rules are used to detect suspicious activity in collected security data and generate alerts or incidents for investigation.

Analytics rules can use Kusto Query Language (KQL) queries to identify patterns such as:

- Brute-force login attempts
- Security audit log clearing
- Suspicious activity
- Known attack techniques
- Time-sensitive events

This document covers two rule types:

1. Scheduled Query Rule
2. Near-Real-Time (NRT) Rule

---

## Part 1: Analytics Rule Types

### Scheduled Query Rules

Scheduled rules run on a defined schedule and are useful for historical or batch-oriented detection.

Example from this project:

- Rule: **Brute Force Attack Detection**
- Data: `SecurityEvent`
- Event ID: `4625`
- Detection: 5+ failed logins from the same IP in 1 minute
- Schedule: Every 5 hours
- Severity: High
- MITRE ATT&CK: `T1110`

### Near-Real-Time (NRT) Rules

NRT rules are designed for time-sensitive detections and can evaluate events within approximately one minute.

Example from this project:

- Rule: **Audit Logs Cleared in Critical Server**
- Data: `Event`
- Event ID: `1102`
- Detection: Security audit log clearing
- Schedule: NRT
- Severity: High
- MITRE ATT&CK: `T1070.001`, `T0872`, `T1630`, `TA0005`

### Other Analytics Capabilities

Also note:

- Fusion — ML-based detection of advanced multistage attacks
- Anomaly — ML-based unusual pattern detection

---

# Part 2: Create a Scheduled Query Rule

The first detection rule is a brute-force detection rule based on failed Windows logons.

## Step 1: Configure General Settings

In Microsoft Sentinel:

1. Open **Analytics** under **Configuration**.
2. Create a new scheduled query rule.
3. Enter the rule name:

   `Brute Force Attack Detection`

4. Add the description:

   `Detects multiple failed login attempts from the same IP.`

5. Set severity to **High**.
6. Keep the rule enabled.

![Analytics rule general settings](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-81.png)

---

## Step 2: Add the Detection Query

Use the following KQL query:

```kql
SecurityEvent
| where EventID == 4625
| where TimeGenerated > ago(1m)
| summarize FailedAttempts = count(), Account = any(Account), IpAddress = any(IpAddress)
    by Computer, bin(TimeGenerated, 1m)
| where FailedAttempts >= 5
```

The query:

- Filters Windows failed-logon events.
- Uses Event ID `4625`.
- Looks at a one-minute window.
- Counts failed attempts.
- Identifies systems/accounts involved.
- Detects five or more failures.

![Scheduled analytics rule query](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-82.png)

---

## Step 3: Configure Incident Settings

Configure the rule so that a detected match creates an incident.

Recommended settings:

- Create incidents from alerts triggered by this rule
- Enable incident creation
- Use entity mappings to provide useful investigation context

![Analytics incident settings](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-83.png)

---

## Step 4: Configure Alert Grouping

Alert grouping can reduce alert fatigue by consolidating similar alerts.

For the brute-force rule, configure grouping according to the investigation requirement. Group related alerts into a single incident for easier investigation.

![Analytics alert grouping](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-84.png)

---

## Step 5: Review the Rule

Review the rule before enabling it.

Verify:

- Rule name
- Description
- Severity
- KQL query
- Query frequency
- Incident settings
- Alert grouping
- Rule status

![Analytics rule review](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-85.png)

![Analytics rule review details](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-86.png)

---

## Step 6: Verify the Active Rule

After saving the rule, return to **Analytics** and verify that the rule is enabled.

Key points include the resulting rule as:

**Brute Force Attack Detection**

- Type: Scheduled
- Detection: 5+ failed logins from the same IP in 1 minute
- Status: Enabled
- Severity: High

![Analytics dashboard showing active rules](images/Threat-Detection-(Analytics)-in-Sentinel/screenshot-87.png)

---

# Part 3: Create a Near-Real-Time Rule

The second detection scenario detects security audit log clearing.

Key points include this as an NRT rule.

## Detection Scenario

- Rule: **Audit Logs Cleared in Critical Server**
- Event ID: `1102`
- Rule type: NRT
- Severity: High
- MITRE ATT&CK mappings:
  - `T1070.001`
  - `T0872`
  - `T1630`
  - `TA0005`

## Query

Key points include `Event` with Event ID `1102` for this detection.

A representative query is:

```kql
Event
| where EventID == 1102
```

# Part 4: Analytics Rule Comparison

| Feature | Brute Force Detection | Audit Log Clearing |
|---|---|---|
| Rule Type | Scheduled Query | NRT |
| Data | `SecurityEvent` | `Event` |
| Event ID | `4625` | `1102` |
| Schedule | Every 5 hours | Within approximately 1 minute |
| Alert Grouping | Group related events | Trigger per event according to configuration |
| Severity | High | High |
| MITRE ATT&CK | `T1110` | `T1070.001`, `T0872`, `T1630`, `TA0005` |

---

# Part 5: KQL Best Practices

Key points include the following KQL practices:

### Use `where` early

Filter data as early as possible to reduce the amount of data processed.

### Use `project`

Select only the columns required by the detection.

### Use `summarize`

Aggregate events when the detection depends on counts or grouped activity.

### Set appropriate time ranges

Avoid scanning unnecessarily large time periods.

### Test queries in Logs

Validate the query before converting it into an analytics rule.

### Use `extend`

Add calculated columns when additional context is required.

---

# Part 6: Alert Fatigue Prevention

Use:

- Alert grouping
- Appropriate severity levels
- Entity mappings
- Suppression rules for known false positives
- Testing before enabling rules in production

The goal is to produce actionable incidents rather than overwhelming analysts with duplicate alerts.

---

# Part 7: SOC Analyst Response

When an analytics rule creates an incident:

1. Review the alert and incident details.
2. Identify affected accounts, hosts, and IP addresses.
3. Validate whether the activity is expected.
4. Check related events around the detection time.
5. Search for additional indicators of compromise.
6. Map the behavior to the relevant MITRE ATT&CK technique.
7. Determine whether the activity is benign, suspicious, or malicious.
8. Document investigation findings.
9. Contain or remediate when required.
10. Close the incident only after the investigation is complete.

---

# Summary

You have successfully:

- Created a Scheduled Query Rule for brute-force detection.
- Configured incident settings and alert grouping.
- Created a Near-Real-Time rule for audit log clearing.
- Understood MITRE ATT&CK technique mappings.
- Learned SOC analyst response steps.
- Documented investigation procedures.

## Analytics Rules

| Rule | Type | Detection | Status |
|---|---|---|---|
| Brute Force Attack Detection | Scheduled | 5+ failed logins from same IP in 1 minute | Enabled |
| Audit Logs Cleared in Critical Server | NRT | Security audit log clearing | Enabled |

## Next Steps

After creating analytics rules:

1. Playbooks and Logic Apps
2. Visualize Security Data in Microsoft Sentinel

## References

- Microsoft Sentinel Analytics
- MITRE ATT&CK Framework
- Kusto Query Language (KQL)
- Microsoft Sentinel NRT Rules
- Microsoft Sentinel Scheduled Rules