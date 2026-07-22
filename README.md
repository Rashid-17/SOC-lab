# SOC-lab
# 🛡️ Windows Security Monitoring and Incident Investigation using Splunk

## Overview

This project demonstrates the implementation of a Security Operations Center (SOC) lab using **Splunk Enterprise**, **Splunk Universal Forwarder**, **Windows Virtual Machine**, and **Kali Linux**.

The primary objective of this project is to centralize Windows Security Event Logs, monitor authentication events, detect suspicious activities, and perform basic incident investigations using a Security Information and Event Management (SIEM) platform.

In addition to authentication monitoring, the lab includes basic network reconnaissance using Nmap to demonstrate how reconnaissance activities can be documented as part of a SOC workflow.

---

# Lab Architecture

```text
                 Kali Linux
          (Network Reconnaissance)
                     │
              Nmap Scan
                     │
                     ▼
              Windows VM
        (Security Event Logs)
                     │
      Splunk Universal Forwarder
                     │
              TCP Port 9997
                     │
                     ▼
          Splunk Enterprise
             (index=main)
                     │
     Searches • Dashboards • Alerts
```

---

# Technologies Used

* Splunk Enterprise
* Splunk Universal Forwarder
* Windows Virtual Machine
* Kali Linux
* Nmap
* Windows Event Viewer
* Splunk Search Processing Language (SPL)

---

# Project Objectives

* Configure centralized Windows log collection.
* Forward Windows Security logs to Splunk Enterprise.
* Monitor authentication-related security events.
* Investigate failed and successful login attempts.
* Create dashboards for security monitoring.
* Configure alerts for suspicious authentication activity.
* Perform basic network reconnaissance using Nmap.
* Document findings and recommendations.

---

# Security Scenarios

## Authentication Monitoring

### Objective

Monitor Windows authentication events and investigate login activities.

### Activities Performed

* Configured Splunk Universal Forwarder on the Windows VM.
* Forwarded Windows Security logs to Splunk Enterprise.
* Generated successful and failed login events.
* Investigated authentication events using Splunk searches.
* Created dashboards for authentication monitoring.
* Configured alerts for repeated failed login attempts.

### Windows Event IDs Monitored

| Event ID | Description      |
| -------- | ---------------- |
| 4624     | Successful Logon |
| 4625     | Failed Logon     |

---

## Network Reconnaissance

### Objective

Identify exposed services running on the Windows VM.

### Activities Performed

* Performed network reconnaissance using Nmap.
* Identified open ports and running services.
* Documented network findings.
* Included reconnaissance activity as part of the security investigation.

Example command:

```bash
nmap -sV <Target-IP>
```

---

# Splunk Searches

## Successful Login Detection

```spl
index=main EventCode=4624
```

## Failed Login Detection

```spl
index=main EventCode=4625
```

## Authentication Activity by User

```spl
index=main (EventCode=4624 OR EventCode=4625)
| stats count by Account_Name
```

## Failed Login Trend

```spl
index=main EventCode=4625
| timechart count
```

## Successful Login Trend

```spl
index=main EventCode=4624
| timechart count
```

---

# Dashboard

The Splunk dashboard includes:

* Failed Login Attempts
* Successful Login Attempts
* Authentication Activity by User
* Security Events Overview
* Login Activity Timeline

---

# Alert Configuration

### Alert Name

Multiple Failed Login Attempts

### Detection Logic

```spl
index=main EventCode=4625
| stats count by Account_Name
```

### Trigger Condition

Trigger an alert when failed login attempts exceed the configured threshold.

---

# Screenshots

The repository contains screenshots demonstrating:

* Splunk Enterprise configuration
* Universal Forwarder configuration
* Windows Security log collection
* Successful login investigation (Event ID 4624)
* Failed login investigation (Event ID 4625)
* Splunk dashboard
* Alert configuration
* Nmap reconnaissance activity

---

# Skills Demonstrated

* Security Information and Event Management (SIEM)
* Windows Event Log Analysis
* Log Collection and Forwarding
* Splunk Search Processing Language (SPL)
* Security Monitoring
* Authentication Monitoring
* Threat Detection
* Incident Investigation
* Dashboard Development
* Alert Configuration
* Network Reconnaissance
* Security Documentation

---

# Learning Outcomes

Through this project, I gained hands-on experience in:

* Deploying Splunk Enterprise and Splunk Universal Forwarder.
* Centralizing Windows Security Event Logs.
* Monitoring authentication events using SPL.
* Creating dashboards for security visibility.
* Configuring alerts for suspicious authentication activity.
* Performing basic network reconnaissance using Nmap.
* Documenting findings using a SOC-style investigation workflow.

---

# Future Enhancements

* Monitor additional Windows Event IDs (4720, 4726, 4688).
* Integrate Sysmon for enhanced endpoint visibility.
* Configure email notifications for alerts.
* Add multiple Windows endpoints to simulate an enterprise environment.
* Develop correlation searches for advanced threat detection.

---

# Repository Structure

```text
windows-security-monitoring-splunk/
│
├── README.md
├── docs/
├── reports/
├── screenshots/
├── splunk_queries/
└── sample_logs/
```

---

# Conclusion

This project demonstrates practical experience in configuring a SIEM environment, collecting and analyzing Windows Security Event Logs, investigating authentication events, and creating dashboards and alerts for security monitoring. It reflects foundational SOC Analyst skills in log management, incident investigation, and security operations within a controlled lab environment.
