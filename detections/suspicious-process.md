\# Suspicious Process Activity Detection

\## Objective

Detect and investigate suspicious process execution on the Ubuntu endpoint using Linux auditd and Wazuh.

\## Environment

\- Wazuh: 4.14.7  
\- Endpoint: Ubuntu VirtualBox VM  
\- Agent: 001 — arman-VirtualBox  
\- Audit Log: /var/log/audit/audit.log

\## Detection Setup

Linux auditd was configured to monitor process execution using:

\-a always,exit -F arch=b64 -S execve -k audit-wazuh-c

Wazuh monitors the audit log and detects command execution using Rule 80792.

Rule description:

Audit: Command: \$(audit.exe)

\## Test Scenario

A controlled test executable was created by copying:

/usr/bin/sleep

to:

/tmp/.system-update

The file was made executable and executed with:

/tmp/.system-update 120

\## Wazuh Detection

Wazuh detected the execution with:

Rule ID: 80792

Rule Description:  
Audit: Command: /tmp/.system-update

Agent:  
001 — arman-VirtualBox

Audit Key:  
audit-wazuh-c

\## Process Investigation

Process:

/tmp/.system-update

PID:  
16436

Parent PID:  
4984

Parent Process:  
bash

User:  
arman

UID:  
1000

EUID:  
1000

The audit event confirmed:

exe="/tmp/.system-update"

key="audit-wazuh-c"

\## File Investigation

File:

/tmp/.system-update

The file was:

\- Located in /tmp  
\- Executable  
\- Owned by arman  
\- An ELF 64-bit x86-64 executable

\## Hash Verification

SHA-256 of /usr/bin/sleep:

06d3927480c7554337818dbf5d91d78689bc8321237280e3d452028d5d1c3f43

SHA-256 of /tmp/.system-update:

06d3927480c7554337818dbf5d91d78689bc8321237280e3d452028d5d1c3f43

The hashes matched, confirming that /tmp/.system-update was an exact copy of /usr/bin/sleep.

\## Execution Timeline

1\. /usr/bin/sleep was copied to /tmp/.system-update.  
2\. Execute permission was added.  
3\. /tmp/.system-update 120 was executed.  
4\. auditd recorded the process execution.  
5\. Wazuh Rule 80792 detected the execution.  
6\. The process and file were investigated.  
7\. The test file was removed.

\## Cleanup

The controlled test file was removed after investigation.

The file was verified to no longer exist.

\## Result

The test successfully demonstrated the complete suspicious-process detection workflow:

Process Execution  
→ auditd  
→ /var/log/audit/audit.log  
→ Wazuh Agent  
→ Wazuh Manager  
→ Rule 80792  
→ Wazuh Alert  
→ Investigation  
→ Cleanup

This was a controlled SOC laboratory simulation and not a real compromise.