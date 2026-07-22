
# Windows Security Event Investigation Report

## Project

**Windows Security Monitoring and Incident Investigation using Splunk**

---

# Objective

The objective of this investigation was to collect Windows Security Event Logs using Splunk Universal Forwarder and analyze authentication-related events in Splunk Enterprise.

---

# Environment

| Component | Details |
|----------|----------|
| SIEM | Splunk Enterprise |
| Log Collector | Splunk Universal Forwarder |
| Operating System | Windows Virtual Machine |
| Index | main |
| Sourcetype | WinEventLog:Security |

---

# Investigation Steps

## Step 1 – Verify Log Collection

Confirmed that Windows Security Event Logs were successfully forwarded to Splunk Enterprise using:

```spl
index=main
```

Result:

- Successfully received Windows Security Events.

---

## Step 2 – Verify Security Logs

Filtered Windows Security Event Logs.

```spl
index=main sourcetype=WinEventLog:Security
```

Result:

- Windows Security logs were successfully indexed.

---

## Step 3 – Investigate Successful Logins

Query

```spl
index=main EventCode=4624
```

Observation

- Successful authentication events were recorded.
- Verified user login activity.

---

## Step 4 – Investigate Failed Logins

Query

```spl
index=main EventCode=4625
```

Observation

- Failed authentication attempts were identified.
- Useful for detecting incorrect password attempts or unauthorized login activity.

---

## Step 5 – Analyze Event Distribution

Query

```spl
index=main
| stats count by sourcetype
```

Observation

- Displayed the number of events collected for each sourcetype.
- Confirmed successful log collection.

---

## Step 6 – Analyze Failed Login Attempts by User

Query

```spl
index=main EventCode=4625
| stats count by Account_Name
```

Observation

- Identified user accounts with failed login attempts.
- Useful for detecting repeated authentication failures.

---

## Step 7 – Investigate Failed Login Details

Query

```spl
index=main EventCode=4625
| table _time host Account_Name Source_Network_Address
```

Observation

The investigation displayed:

- Event Timestamp
- Hostname
- User Account
- Source Network Address

This information helps identify when the failed login occurred, the affected host, and the source of the authentication attempt.

---

## Step 8 – Monitor User Account Creation

Query

```spl
index=main EventCode=4720
```

Observation

- Detected user account creation events.
- Useful for monitoring administrative activity.

---

## Step 9 – Monitor User Account Deletion

Query

```spl
index=main EventCode=4726
```

Observation

- Detected user account deletion events.
- Useful for tracking account management activities.

---

# Findings

- Successfully configured Splunk Enterprise.
- Successfully configured Splunk Universal Forwarder.
- Windows Security Event Logs were collected successfully.
- Authentication events were monitored.
- Failed login attempts were investigated.
- User account management events were analyzed.
- SPL queries were used to investigate Windows Security Events.

---

# Conclusion

This investigation demonstrated the use of Splunk Enterprise as a SIEM solution for collecting and analyzing Windows Security Event Logs. Authentication monitoring, event analysis, and user account activity were successfully investigated using SPL queries, providing practical experience in SOC monitoring and basic incident investigation.
