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
- **MITRE ATT&CK** — planned investigation and technique mapping
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
