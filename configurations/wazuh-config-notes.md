# Wazuh Configuration Notes

## Wazuh Environment

- Wazuh Version: 4.14.7
- Wazuh Manager: Main Ubuntu Host
- Wazuh Agent ID: 001
- Agent Name: arman-VirtualBox
- Monitored OS: Ubuntu 24.04 LTS

## Agent Log Monitoring

The Wazuh Agent monitors relevant Linux log sources, including:

- `/var/log/auth.log`
- `/var/log/audit/audit.log`

## Linux Auditd Monitoring

Linux auditd was enabled on the monitored Ubuntu VM.

Process execution monitoring was configured with:

-a always,exit -F arch=b64 -S execve -k audit-wazuh-c

This records Linux process execution events.

## Wazuh Audit Key Mapping

The Wazuh Manager audit key list contains:

audit-wazuh-c:command

This mapping allows Wazuh Rule 80792 to detect command execution events.

## Wazuh Rule 80792

Rule ID:

80792

Description:

Audit: Command: $(audit.exe)

The rule was successfully verified through the Wazuh Threat Hunting dashboard.

## Important Configuration Notes

The monitored endpoint is the Ubuntu VirtualBox VM.

The Wazuh Manager, Indexer, and Dashboard run on the main Ubuntu host.

The configuration was tested using controlled SOC laboratory activity.

No production systems were involved.
