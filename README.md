# Wazuh SOC Home Lab

A hands-on Security Operations Center (SOC) home lab built with **Wazuh**, **Ubuntu Linux**, **VirtualBox**, and **Linux auditd**.

This project demonstrates a practical defensive security workflow from **security event generation and log collection to detection, alert analysis, investigation, MITRE ATT&CK mapping, incident response, and documentation**.

---

## Project Overview

This project was developed as a controlled security laboratory to practice practical SOC analyst activities.

The lab focuses on:

- SIEM monitoring and alert analysis
- Security event and log analysis
- Detection engineering
- Linux security monitoring
- File Integrity Monitoring (FIM)
- Authentication and account activity investigation
- Suspicious process detection
- SOC alert triage
- MITRE ATT&CK mapping
- Incident response and documentation

The objective was to build and document an end-to-end defensive security workflow rather than simply generate security alerts.

---

## Security Workflow

    Security Event
          ↓
    Log Collection
          ↓
    Detection
          ↓
    Wazuh Alert
          ↓
    SOC Triage
          ↓
    Investigation
          ↓
    Evidence Collection
          ↓
    MITRE ATT&CK Mapping
          ↓
    Incident Response
          ↓
    Documentation

---

## Lab Architecture

The lab consists of a main Ubuntu host running the Wazuh infrastructure and an isolated Ubuntu VirtualBox endpoint running the Wazuh Agent.

    Main Ubuntu Host
    ┌─────────────────────────┐
    │     Wazuh Manager       │
    │     Wazuh Indexer       │
    │     Wazuh Dashboard     │
    └────────────┬────────────┘
                 │
            Wazuh Agent
                 │
    ┌────────────▼────────────┐
    │    Ubuntu VirtualBox    │
    │      arman-VirtualBox   │
    │                         │
    │  Linux Logs             │
    │  Authentication Events  │
    │  File Activity          │
    │  Process Activity       │
    │  auditd                 │
    └─────────────────────────┘

### Lab Components

| Component | Purpose |
|---|---|
| Wazuh 4.14.7 | SIEM, security monitoring and alerting |
| Wazuh Manager | Event processing and detection |
| Wazuh Indexer | Security event storage and search |
| Wazuh Dashboard | Alert investigation and visualization |
| Ubuntu Linux | Monitored endpoint |
| VirtualBox | Isolated laboratory environment |
| Linux auditd | Process and command auditing |
| Git / GitHub | Version control and documentation |
| Joplin | Investigation and incident documentation |

---

## Security Scenarios

The lab includes multiple controlled security scenarios designed to represent common SOC investigation tasks.

### 1. SSH Brute Force

A controlled SSH authentication attack was generated against the monitored Linux endpoint.

The investigation covered:

- Failed SSH authentication attempts
- Invalid/non-existent user attempts
- Wazuh SSH detection rules
- Brute-force alert analysis
- Timeline reconstruction
- Evidence collection

Relevant Wazuh detections included:

- Rule 5710
- Rule 5715
- Rule 5716
- Rule 5720
- Rule 5763

Detailed documentation:

[SSH Brute Force Detection](detections/ssh-bruteforce.md)

[INC-001 — SSH Brute Force](incident-reports/INC-001-SSH-Bruteforce.md)

---

### 2. File Integrity Monitoring

Wazuh File Integrity Monitoring (FIM) was configured and tested to detect controlled file modifications.

The investigation covered:

- FIM configuration
- File baseline
- Controlled file modification
- Wazuh alert generation
- Alert detail analysis
- Investigation and documentation

Detailed documentation:

[File Integrity Monitoring](detections/file-integrity.md)

[INC-002 — File Integrity Violation](incident-reports/INC-002-File-Integrity-Violation.md)

---

### 3. Account & Authentication Activity

A controlled test account was created to investigate account-management activity.

The investigation covered:

- New local account creation
- Account information verification
- Wazuh account-activity detection
- Rule 5902 analysis
- Evidence collection
- Account removal and cleanup

Detailed documentation:

[Account Activity Detection](detections/account-activity.md)

[INC-003 — Account Creation](incident-reports/INC-003-Account-Creation.md)

---

### 4. Suspicious Process Activity

Linux `auditd` was integrated with Wazuh to monitor command execution and investigate suspicious process activity.

The investigation covered:

- `auditd` configuration
- Wazuh audit log collection
- Audit key configuration
- Wazuh Rule 80792
- Suspicious executable creation
- Process execution monitoring
- Parent process investigation
- File analysis
- SHA-256 hash verification
- Execution timeline analysis
- Cleanup and remediation

The controlled executable was created from `/usr/bin/sleep` and executed from `/tmp` to simulate suspicious process activity in the isolated laboratory environment.

Detailed documentation:

[Suspicious Process Detection](detections/suspicious-process.md)

[INC-005 — Suspicious Process](incident-reports/INC-005-Suspicious-Process.md)

---

## Detection Engineering

The project included examination and validation of Wazuh's built-in detection rules and decoders.

Detection engineering activities included:

- Reviewing Wazuh rules
- Understanding rule IDs and rule levels
- Examining alert fields
- Reviewing decoder output
- Validating raw event data
- Comparing security events with generated alerts
- Confirming detection behavior using controlled activity

Examples of investigated detections:

    SSH Authentication / Brute Force
    Rule 5710
    Rule 5715
    Rule 5716
    Rule 5720
    Rule 5763

    Account Activity
    Rule 5902

    Auditd Command Monitoring
    Rule 80792

Detection documentation:

- [SSH Brute Force](detections/ssh-bruteforce.md)
- [File Integrity Monitoring](detections/file-integrity.md)
- [Account Activity](detections/account-activity.md)
- [Suspicious Process Activity](detections/suspicious-process.md)

---

## SOC Investigation & MITRE ATT&CK

The completed investigations were reviewed from a SOC triage perspective and mapped to MITRE ATT&CK where the available evidence supported the mapping.

| Incident | Activity | ATT&CK Mapping |
|---|---|---|
| INC-001 | SSH brute force | T1110.001 — Password Guessing |
| INC-002 | Controlled file modification | T1565.001 considered, but not asserted as confirmed adversary behavior |
| INC-003 | Local account creation | T1136.001 — Local Account |
| INC-004 | Authentication activity | No specific technique asserted solely from the available evidence |
| INC-005 | Suspicious process execution | No specific technique asserted without sufficient supporting evidence |

The project intentionally avoids over-mapping MITRE ATT&CK techniques when the evidence does not clearly support them.

Detailed analysis:

[MITRE ATT&CK Mapping](mitre-attack/attack-mapping.md)

[SOC Triage Matrix](mitre-attack/soc-triage-matrix.md)

---

## SOC Triage

The investigations followed a structured SOC-style triage workflow:

    Alert
      ↓
    Validate Event
      ↓
    Determine Context
      ↓
    Assess Severity
      ↓
    Collect Evidence
      ↓
    Investigate Activity
      ↓
    Determine Impact
      ↓
    Contain / Remediate
      ↓
    Document Findings

The repository includes a dedicated triage matrix covering the investigated incidents.

[SOC Triage Matrix](mitre-attack/soc-triage-matrix.md)

---

## Incident Response

The project follows a structured incident-response workflow:

    Detection
       ↓
    Triage
       ↓
    Investigation
       ↓
    Containment / Remediation
       ↓
    Recovery
       ↓
    Documentation
       ↓
    Lessons Learned

The incident-response process and response summaries are documented in:

[Incident Response Process](incident-reports/incident-response.md)

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

---

## Security Skills Demonstrated

- SIEM monitoring with Wazuh
- SOC alert triage
- Security log analysis
- Detection engineering
- Linux security monitoring
- SSH brute-force detection
- File Integrity Monitoring (FIM)
- Authentication and account investigation
- Linux auditd monitoring
- Suspicious process investigation
- Evidence collection
- Timeline analysis
- MITRE ATT&CK mapping
- Incident response
- Security documentation
- Git and GitHub workflow

---

## Technologies & Tools

### SIEM / Security Monitoring

- Wazuh 4.14.7
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### Operating Systems

- Ubuntu Linux

### Security Tools

- Linux auditd
- Wazuh Rules & Decoders
- MITRE ATT&CK

### Environment & Documentation

- VirtualBox
- Git
- GitHub
- Markdown
- Joplin

---

## Repository Structure

    Wazuh-SOC-Home-Lab/
    │
    ├── README.md
    │
    ├── architecture/
    │   └── architecture.png
    │
    ├── configurations/
    │   └── wazuh-config-notes.md
    │
    ├── detections/
    │   ├── ssh-bruteforce.md
    │   ├── file-integrity.md
    │   ├── account-activity.md
    │   └── suspicious-process.md
    │
    ├── incident-reports/
    │   ├── INC-001-SSH-Bruteforce.md
    │   ├── INC-002-File-Integrity-Violation.md
    │   ├── INC-003-Account-Creation.md
    │   ├── INC-005-Suspicious-Process.md
    │   └── incident-response.md
    │
    ├── mitre-attack/
    │   ├── attack-mapping.md
    │   └── soc-triage-matrix.md
    │
    ├── screenshots/
    │   └── SOC investigation and evidence screenshots
    │
    └── lessons-learned.md

---

## Key Documentation

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

### Supporting Documentation

- [Wazuh Configuration Notes](configurations/wazuh-config-notes.md)
- [Lessons Learned](lessons-learned.md)

---

## Evidence & Investigation

The `screenshots/` directory contains selected evidence collected throughout the lab.

Examples include:

- Wazuh dashboard state
- Wazuh detection rules
- Raw security events
- Alert details
- SSH brute-force activity
- FIM events
- Account creation events
- Auditd command activity
- Suspicious process execution
- Investigation evidence
- Incident timelines
- Cleanup and remediation evidence

The screenshots are included to support the documented investigations and demonstrate the evidence used during analysis.

---

## Lessons Learned

The project provided practical experience in:

- Understanding how endpoint security events reach a SIEM
- Analyzing Linux security logs
- Understanding Wazuh rules and alerts
- Validating alerts against raw event data
- Distinguishing expected activity from suspicious activity
- Investigating authentication events
- Monitoring file changes with FIM
- Using auditd for process-level visibility
- Investigating suspicious process execution
- Building incident timelines
- Applying MITRE ATT&CK based on available evidence
- Performing SOC triage
- Documenting incident response
- Organizing technical security work into a professional portfolio

Detailed notes:

[Lessons Learned](lessons-learned.md)

---

## Final Outcome

This project demonstrates an end-to-end defensive security workflow in a controlled Linux-based SOC environment:

**Security Event → Log Collection → Detection → Alert → Triage → Investigation → Evidence → MITRE ATT&CK → Incident Response → Documentation**

The final repository contains:

- Wazuh configuration notes
- Detection documentation
- Incident reports
- SOC triage analysis
- MITRE ATT&CK mapping
- Investigation evidence
- Incident response documentation
- Lessons learned

The project was built as a practical cybersecurity learning environment focused on **SOC operations, blue-team monitoring, detection analysis, investigation, and incident response**.

---

## Disclaimer

This project was conducted in a controlled home-lab environment using isolated virtual machines and intentionally generated security events.

The scenarios were created for defensive security learning, SOC investigation practice, and detection validation.
