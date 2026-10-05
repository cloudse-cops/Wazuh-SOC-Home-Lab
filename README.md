# Enterprise Wazuh SOC Home Lab

A hands-on Security Operations Center (SOC) home lab built with Wazuh, Ubuntu, VirtualBox, Linux auditd, and controlled security scenarios.

The project demonstrates an end-to-end defensive security workflow:

**Security Event → Log Collection → Detection → Alert → Investigation → Evidence → Incident Documentation**

---

## Project Overview

This project was built to simulate practical SOC analyst activities in a controlled laboratory environment.

The lab uses:

- **Wazuh 4.14.7** — SIEM / security monitoring platform
- **Ubuntu** — monitored Linux endpoint
- **VirtualBox** — isolated lab environment
- **Linux auditd** — process and command monitoring
- **Wazuh Rules & Decoders** — security event detection
- **MITRE ATT&CK** — investigation and technique mapping
- **GitHub** — project documentation and evidence

---

## Lab Architecture

The environment consists of:

```text
                    Main Ubuntu Host
             ┌───────────────────────────┐
             │       Wazuh Manager       │
             │       Wazuh Indexer       │
             │       Wazuh Dashboard     │
             └─────────────┬─────────────┘
                           │
                    Wazuh Agent
                           │
             ┌─────────────▼─────────────┐
             │     Ubuntu VirtualBox     │
             │       arman-VirtualBox    │
             │                           │
             │  Linux Logs               │
             │  auditd                   │
             │  Process Activity         │
             │  Authentication Events    │
             └───────────────────────────┘

---

## Project Phases

| Phase | Activity | Status |
|---|---|---|
| 1 | Lab Setup & Verification | ✅ Complete |
| 2 | Baseline & Normal Activity | ✅ Complete |
| 3 | Detection Engineering | ✅ Complete |
| 4 | SSH Brute Force Detection & Investigation | ✅ Complete |
| 5 | File Integrity Monitoring & Investigation | ✅ Complete |
| 6 | Account & Authentication Activity | ✅ Complete |
| 7 | Suspicious Process Detection & Investigation | ✅ Complete |
| 8 | SOC Investigation & MITRE ATT&CK Mapping | ✅ Complete |
| 9 | Incident Response & Reporting | ✅ Complete |
| 10 | GitHub Portfolio & Documentation | ✅ Complete |

## Documentation

### Detection Engineering

- [SSH Brute Force](detections/ssh-bruteforce.md)
- [File Integrity Monitoring](detections/file-integrity.md)
- [Account Activity](detections/account-activity.md)
- [Suspicious Process Activity](detections/suspicious-process.md)

### Incident Reports

- [INC-001 — SSH Brute Force](incident-reports/INC-001-SSH-Bruteforce.md)
- [INC-002 — File Integrity Violation](incident-reports/INC-002-File-Integrity-Violation.md)
- [INC-003 — Account Creation](incident-reports/INC-003-Account-Creation.md)
- [INC-005 — Suspicious Process](incident-reports/INC-005-Suspicious-Process.md)
- [Incident Response Process](incident-reports/incident-response.md)

### SOC Investigation

- [MITRE ATT&CK Mapping](mitre-attack/attack-mapping.md)
- [SOC Triage Matrix](mitre-attack/soc-triage-matrix.md)

## Final Outcome

The completed lab demonstrates an end-to-end defensive security workflow:

**Security Event → Log Collection → Detection → Alert → Investigation → MITRE ATT&CK Mapping → Incident Response → Evidence → Documentation**

The project provides practical experience with Wazuh SIEM, Linux security monitoring, auditd, detection analysis, SOC triage, incident investigation, and incident response in a controlled laboratory environment.
