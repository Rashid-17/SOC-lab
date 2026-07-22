# Splunk Search Processing Language (SPL) Queries

This document contains the SPL queries used throughout the Windows Security Monitoring SOC Lab.

---

## 1. View All Indexed Events

```spl
index=main
```

**Description**

Displays all events stored in the `main` index.

---

## 2. View Windows Security Logs

```spl
index=main sourcetype=WinEventLog:Security
```

**Description**

Filters and displays only Windows Security Event Logs.

---

## 3. Successful Login Events (Event ID 4624)

```spl
index=main EventCode=4624
```

**Description**

Retrieves all successful Windows logon events.

---

## 4. Failed Login Events (Event ID 4625)

```spl
index=main EventCode=4625
```

**Description**

Displays all failed Windows logon attempts for security analysis.

---

## 5. Count Events by Sourcetype

```spl
index=main
| stats count by sourcetype
```

**Description**

Displays the number of events grouped by their source type.

---

## 6. Failed Login Count by User

```spl
index=main EventCode=4625
| stats count by Account_Name
```

**Description**

Counts failed login attempts for each user account.

---

## 7. Failed Login Investigation

```spl
index=main EventCode=4625
| table _time host Account_Name Source_Network_Address
```

**Description**

Displays detailed information about failed login attempts, including:

- Timestamp
- Hostname
- User Account
- Source Network Address

---

## 8. User Account Created (Event ID 4720)

```spl
index=main EventCode=4720
```

**Description**

Displays user account creation events.

---

## 9. User Account Deleted (Event ID 4726)

```spl
index=main EventCode=4726
```

**Description**

Displays user account deletion events.

---

# Summary

These SPL queries were used to monitor Windows Security Event Logs, investigate authentication events, and perform basic security analysis using Splunk Enterprise.
