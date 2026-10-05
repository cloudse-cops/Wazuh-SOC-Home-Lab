\# INC-005 — Suspicious Process Activity

\## Incident Type

Suspicious Process Execution

\## Status

Closed — Controlled SOC Lab Simulation

\## Affected Host

\- Agent ID: 001  
\- Host: arman-VirtualBox  
\- Operating System: Ubuntu

\## Detection Source

\- Wazuh Rule ID: 80792  
\- Rule Description: Audit: Command: /tmp/.system-update  
\- Audit Key: audit-wazuh-c  
\- Log Source: /var/log/audit/audit.log

\## Detected Process

Executable:

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

\## Detection

A controlled executable named \`/tmp/.system-update\` was executed on the monitored Ubuntu endpoint.

Linux auditd recorded the execution and Wazuh received the audit event.

Wazuh Rule 80792 generated an alert for the execution.

\## Investigation

The process was traced to:

/tmp/.system-update

The parent process was:

bash

The process ran under the user:

arman

UID:

1000

The file was located in \`/tmp\` and had executable permissions.

The file was identified as an ELF 64-bit x86-64 executable.

\## Hash Verification

SHA-256 of \`/usr/bin/sleep\`:

06d3927480c7554337818dbf5d91d78689bc8321237280e3d452028d5d1c3f43

SHA-256 of \`/tmp/.system-update\`:

06d3927480c7554337818dbf5d91d78689bc8321237280e3d452028d5d1c3f43

The hashes matched.

This confirmed that \`/tmp/.system-update\` was an exact copy of \`/usr/bin/sleep\`.

\## Timeline

1\. \`/usr/bin/sleep\` was copied to \`/tmp/.system-update\`.  
2\. Execute permission was added to the file.  
3\. \`/tmp/.system-update 120\` was executed.  
4\. auditd recorded the process execution.  
5\. Wazuh Rule 80792 detected the execution.  
6\. The Wazuh alert was investigated.  
7\. The parent process and user context were identified.  
8\. The executable type and SHA-256 hash were verified.  
9\. The controlled test file was removed.

\## Response

The test artifact was removed after the investigation.

The file was verified to no longer exist.

\## Conclusion

This event was a controlled SOC laboratory simulation and not a real compromise.

The exercise demonstrated that Wazuh can monitor Linux process execution through auditd, generate an alert, provide process and user context, and support investigation using audit evidence.

\## Evidence

\- 05-Suspicious-Process-Running.png  
\- 06-Suspicious-Process-Audit-Evidence.png  
\- 07-Wazuh-Suspicious-Process-Detection.png  
\- 08-Suspicious-Process-Alert-Details.png  
\- 09-Suspicious-Process-Investigation-Evidence.png  
\- 10-Suspicious-Process-Audit-Timeline-1.png  
\- 10-Suspicious-Process-Audit-Timeline-2.png  
\- 11-Suspicious-Process-Cleanup.png