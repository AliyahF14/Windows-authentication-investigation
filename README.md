# Project 3 — Windows Authentication Investigation

## Overview

This project demonstrates a controlled Windows security-log investigation using **Event Viewer**. The exercise focuses on identifying repeated failed authentication attempts, correlating them with a later successful logon, and determining whether the activity was local or remote.

> **Important:** All suspicious-looking authentication activity in this project was intentionally generated on a personal Windows lab system. It is not evidence of a real compromise.

## Objectives

- Investigate Windows Security Event ID **4625** (failed logon)
- Investigate Windows Security Event ID **4624** (successful logon)
- Identify the targeted account and logon type
- Correlate authentication events into a timeline
- Determine whether the activity originated locally or remotely
- Document findings using a SOC-style incident report

## Tools

- Windows 10
- Windows Event Viewer
- Windows Security event logs
- Command Prompt
- Microsoft Windows Security Auditing

## Investigation Scenario

A test account named `LabTest` was created specifically for this lab. Five incorrect password attempts were intentionally made against the account to generate Event ID 4625 records. A later successful sign-in generated Event ID 4624.

## Key Findings

### Failed authentication activity

Five Event ID 4625 records were observed for `LabTest`:

| Time | Event | Result |
|---|---:|---|
| 10:50:03 AM | 4625 | Failed |
| 10:50:10 AM | 4625 | Failed |
| 10:50:17 AM | 4625 | Failed |
| 10:50:22 AM | 4625 | Failed |
| 10:50:31 AM | 4625 | Failed |

The five failures occurred within approximately **28 seconds**.

The detailed events showed:

- Logon Type: **2 — Interactive**
- Status: **0xC000006D**
- SubStatus: **0xC000006A**
- Authentication Package: **Negotiate**
- IP Address: **127.0.0.1**
- IP Port: **0**

### Successful authentication

A later Event ID 4624 showed a successful interactive logon for `LabTest` at approximately **10:58:20 AM**.

The event also showed:

- Logon Type: **2 — Interactive**
- Authentication Package: **Negotiate**
- IP Address: **127.0.0.1**
- IP Port: **0**

## Analyst Assessment

The evidence demonstrates a cluster of failed authentication attempts followed by a successful authentication. However, the activity was deliberately generated as part of a controlled lab exercise.

The local address **127.0.0.1** and interactive logon type indicate that the observed authentication activity occurred locally on the Windows system. Therefore, this project does **not** claim detection of a remote brute-force attack or compromise.

The appropriate analyst conclusion is:

> Repeated failed local authentication attempts against a test account were successfully identified and correlated with a later successful local authentication. The activity was confirmed as controlled lab activity, with no evidence in this dataset of a remote source or external compromise.

## Security Concepts Demonstrated

- Windows Security event monitoring
- Authentication log analysis
- Event ID 4625
- Event ID 4624
- Logon Type analysis
- Authentication failure codes
- Timeline correlation
- Local vs. remote source analysis
- Evidence-based incident assessment
- Avoiding unsupported conclusions

## Evidence

Sanitized screenshots are included in the `screenshots/` directory.

- `failed-logon-cluster.png` — Event ID 4625 cluster and detailed fields
- `successful-logon-details.png` — Event ID 4624 detailed fields
- `successful-logon-general.png` — Event ID 4624 general event summary

## Lessons Learned

This investigation reinforced the importance of validating individual event fields before labeling activity malicious. A cluster of failed logons can look suspicious, but source address, logon type, account context, and lab conditions must be considered before determining severity.

## Portfolio Value

This project demonstrates practical entry-level SOC skills:

**Collect → Filter → Investigate → Correlate → Assess → Document**

