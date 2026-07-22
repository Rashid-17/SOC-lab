# 🛡️ Windows Security Monitoring and Incident Investigation using Splunk

## Overview

This project demonstrates the implementation of a Security Operations Center (SOC) lab using **Splunk Enterprise**, **Splunk Universal Forwarder**, and a **Windows Virtual Machine** to collect, monitor, and investigate Windows Security Event Logs.

The objective of this project is to centralize Windows Security logs, monitor authentication activities, investigate security-related events, and gain hands-on experience with Security Information and Event Management (SIEM) technologies using Splunk.

---

# Lab Architecture

```text
           Windows Virtual Machine
      (Windows Security Event Logs)
                    │
                    │
    Splunk Universal Forwarder
                    │
              TCP Port 9997
                    │
                    ▼
           Splunk Enterprise
              (index=main)
                    │
      Searches • Reports • Analysis
```

---

# Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Windows Virtual Machine
- Windows Event Viewer
- Windows Security Logs
- Splunk Search Processing Language (SPL)

---

# Project Objectives

- Configure centralized Windows Security log collection.
- Forward Windows Security logs to Splunk Enterprise.
- Monitor Windows authentication events.
- Investigate successful and failed login attempts.
- Analyze Windows Security Event IDs.
- Perform security investigations using SPL queries.
- Document security findings.

---

# Security Scenario

## Authentication Monitoring

### Objective

Monitor Windows authentication events to identify successful and failed login attempts.

### Activities Performed

- Installed and configured Splunk Enterprise.
- Configured Splunk Universal Forwarder on the Windows machine.
- Forwarded Windows Security Event Logs to Splunk Enterprise.
- Generated authentication events for analysis.
- Investigated security events using SPL queries.
- Documented findings with screenshots.

---

# Windows Security Events Monitored

| Event ID | Description |
|----------|-------------|
| **4624** | Successful Logon |
| **4625** | Failed Logon |
| **4720** | User Account Created |
| **4726** | User Account Deleted |
| **5379** | Credential Manager Credentials Read |

---

# Splunk Searches

## View All Events

```spl
index=main
```

## Windows Security Logs

```spl
index=main sourcetype=WinEventLog:Security
```

## Successful Login Detection

```spl
index=main EventCode=4624
```

## Failed Login Detection

```spl
index=main EventCode=4625
```

## Failed Login Investigation

```spl
index=main EventCode=4625
| table _time host Account_Name Source_Network_Address
```

## Failed Login Statistics

```spl
index=main EventCode=4625
| stats count by Account_Name
```

## User Account Created

```spl
index=main EventCode=4720
```

## User Account Deleted

```spl
index=main EventCode=4726
```

## Credential Manager Access

```spl
index=main EventCode=5379
```

---

# Screenshots

The repository contains screenshots demonstrating:

- Splunk Enterprise Search & Reporting
- Windows Security Event Log Collection
- All Indexed Events
- Windows Security Log Source
- Successful Login Investigation (Event ID 4624)
- Failed Login Investigation (Event ID 4625)
- Failed Login Statistics
- User Account Creation (Event ID 4720)
- User Account Deletion (Event ID 4726)
- Credential Manager Access (Event ID 5379)

---

# Skills Demonstrated

- Security Information and Event Management (SIEM)
- Windows Event Log Analysis
- Log Collection and Forwarding
- Splunk Search Processing Language (SPL)
- Authentication Monitoring
- Security Monitoring
- Event Investigation
- Incident Analysis
- Security Documentation

---

# Learning Outcomes

Through this project, I gained hands-on experience in:

- Deploying Splunk Enterprise.
- Configuring Splunk Universal Forwarder.
- Centralizing Windows Security Event Logs.
- Monitoring authentication activities.
- Investigating Windows Security Event IDs.
- Writing SPL queries for log analysis.
- Performing basic SOC-style incident investigations.

---

# Future Enhancements

- Create interactive Splunk Dashboards.
- Configure Alerts for repeated failed login attempts.
- Monitor additional Windows Event IDs (4688, 4672, 4634).
- Integrate Sysmon for enhanced endpoint visibility.
- Add multiple Windows endpoints.
- Perform network reconnaissance using Nmap.
- Create correlation searches for threat detection.

---

# Repository Structure

```text
windows-security-monitoring-splunk/
│
├── README.md
│
├── screenshots/
│   ├── 01_All_Events.png
│   ├── 02_Windows_Security_Logs.png
│   ├── 03_Sourcetype_Count.png
│   ├── 04_Failed_Login_4625.png
│   ├── 05_Successful_Login_4624.png
│   ├── 06_Failed_Login_Table.png
│   ├── 07_Failed_Login_Statistics.png
│   ├── 08_User_Created_4720.png
│   ├── 09_User_Deleted_4726.png
│   └── 10_Credential_Manager_5379.png
│
├── splunk_queries/
│   └── authentication_queries.md
│
└── reports/
    └── investigation_notes.md
```

---

# Conclusion

This project demonstrates practical experience in configuring a SIEM environment using Splunk Enterprise, collecting Windows Security Event Logs through Splunk Universal Forwarder, and investigating authentication-related events using SPL queries. It showcases foundational SOC Analyst skills in log collection, security monitoring, event analysis, and incident investigation within a controlled lab environment.

---
## Author

**Rashid K**

Cybersecurity | SOC Analyst | Splunk | Windows Security Monitoring
