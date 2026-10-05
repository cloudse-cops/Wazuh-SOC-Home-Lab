# \# MITRE ATT&CK Mapping & SOC Triage

\## Objective

Map the completed Wazuh security scenarios to relevant MITRE ATT&CK techniques where the evidence supports the mapping, and record the SOC triage decision for each incident.

\---

\## INC-001 — SSH Brute Force

\### Activity

Repeated SSH authentication failures and brute-force activity were generated against the Ubuntu endpoint.

\### Detection

\- Wazuh SSH detection rules  
\- Rule 5710 for invalid/nonexistent-user activity  
\- SSH brute-force alert evidence  
\- Authentication failure logs  
\- Incident timeline

\### MITRE ATT&CK

\*\*T1110.001 — Password Guessing\*\*

The scenario involved repeated attempts to guess SSH authentication credentials.

\### SOC Triage

\- Activity: SSH authentication failures / password guessing  
\- Host: arman-VirtualBox  
\- Decision: Security-relevant  
\- Investigation: Review authentication failures, identify the affected account and source activity, correlate repeated events, and determine whether the behavior is authorized.

\### Outcome

Controlled laboratory brute-force activity was successfully detected and investigated.

\---

\## INC-002 — File Integrity Violation

\### Activity

A controlled modification was made to a file monitored by Wazuh File Integrity Monitoring.

\### Detection

\- FIM configuration  
\- Original file state  
\- File modification evidence  
\- Wazuh FIM alert  
\- Alert details

\### MITRE ATT&CK

\*\*Potentially relevant: T1565.001 — Stored Data Manipulation\*\*

This technique can describe unauthorized modification of stored data.

However, this laboratory event was intentionally generated for testing, so it is \*\*not treated as a confirmed adversary technique\*\*.

\### SOC Triage

\- Activity: File modification  
\- Detection source: Wazuh FIM  
\- Decision: Investigate  
\- Investigation: Compare original and modified state, identify the affected file, determine the responsible user/process, and verify whether the change was authorized.

\### Outcome

Wazuh successfully detected the controlled file modification.

\---

\## INC-003 — Account Creation

\### Activity

A Linux user account named \`soc-test\` was created on the monitored endpoint.

\### Detection

Wazuh Rule 5902 detected the new account.

The alert included:

\- Rule ID: 5902  
\- MITRE ID: T1136  
\- Tactic: Persistence  
\- Technique: Create Account

\### MITRE ATT&CK

\*\*T1136.001 — Create Account: Local Account\*\*

The activity involved creation of a local Linux account.

\### SOC Triage

\- Activity: Local account creation  
\- Account: \`soc-test\`  
\- Host: arman-VirtualBox  
\- Decision: Security-relevant  
\- Investigation: Verify who created the account, review privileges and group membership, and determine whether the account was authorized.

\### Response

The controlled test account was removed after investigation.

\### Outcome

Wazuh successfully detected and provided context for Linux account creation.

\---

\## INC-004 — Authentication Activity

\### Activity

Linux authentication events were monitored using Wazuh.

\### MITRE ATT&CK

No specific ATT&CK technique is asserted from the authentication evidence alone.

Relevant ATT&CK techniques depend on the actual behavior observed.

For example, compromised or misused existing credentials may fall under:

\*\*T1078 — Valid Accounts\*\*

However, the laboratory evidence does not establish credential compromise or malicious use of a valid account.

\### SOC Triage

\- Review successful and failed authentication  
\- Identify affected account  
\- Identify source and timestamp  
\- Correlate repeated events  
\- Determine whether the authentication is expected or suspicious

\### Outcome

Authentication monitoring provides supporting context for SOC investigations but is not automatically mapped to an ATT&CK technique without sufficient evidence.

\---

\## INC-005 — Suspicious Process Activity

\### Activity

A controlled executable named:

\`/tmp/.system-update\`

was executed on the Ubuntu endpoint.

\### Detection

Wazuh Rule 80792 detected the execution using Linux auditd.

\### Evidence

\- Auditd execution event  
\- \`key="audit-wazuh-c"\`  
\- PID 16436  
\- Parent PID 4984  
\- Parent process \`bash\`  
\- User \`arman\`  
\- Executable \`/tmp/.system-update\`  
\- File/type analysis  
\- SHA-256 verification  
\- Execution timeline  
\- Cleanup evidence

\### MITRE ATT&CK

\*\*No specific adversary technique is asserted for this laboratory event.\*\*

Although the process was launched from a Bash shell, the test did not demonstrate malicious abuse of the Unix shell. It demonstrated process-execution monitoring and investigation.

\### SOC Triage

\- Activity: Suspicious executable execution from \`/tmp\`  
\- Host: arman-VirtualBox  
\- Process: \`/tmp/.system-update\`  
\- PID: 16436  
\- Parent: bash  
\- User: arman  
\- Detection: Wazuh Rule 80792  
\- Decision: Investigate  
\- Investigation: Examine process context, parent process, user, executable type, hash, audit records, and execution timeline.

\### Response

The controlled test executable was removed after investigation.

\### Outcome

The exercise demonstrated end-to-end process-execution detection and investigation using auditd and Wazuh.

\---

\# Overall SOC Triage Summary

| Incident | Activity | Detection | MITRE Mapping | Triage |  
|---|---|---|---|---|  
| INC-001 | SSH brute force | Wazuh SSH rules | T1110.001 | Investigated |  
| INC-002 | File modification | Wazuh FIM | Potential T1565.001 | Investigated |  
| INC-003 | Local account creation | Rule 5902 | T1136.001 | Investigated |  
| INC-004 | Authentication activity | Wazuh/authentication logs | No specific technique asserted | Reviewed |  
| INC-005 | Suspicious process execution | Rule 80792 + auditd | No specific technique asserted | Investigated |

\## Overall SOC Assessment

The completed scenarios demonstrate a defensive SOC workflow:

Security Event  
→ Log Collection  
→ Detection  
→ Alert  
→ Investigation  
→ MITRE ATT&CK Assessment  
→ Triage Decision  
→ Evidence  
→ Documentation

MITRE ATT&CK mappings are only assigned where the observed behavior provides enough evidence to support the technique. Controlled laboratory activity is explicitly distinguished from confirmed adversary behavior.