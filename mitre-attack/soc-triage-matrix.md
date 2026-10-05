\# SOC Triage Matrix

\## Purpose

Summarize the SOC triage decision for each completed security scenario.

| Incident | Activity | Detection | Severity | Triage Decision | Final Status |  
|---|---|---|---|---|---|  
| INC-001 | SSH brute force | Wazuh SSH rules | Medium | Investigate authentication failures and source activity | Controlled lab activity |  
| INC-002 | File modification | Wazuh FIM | Medium | Investigate affected file and responsible user/process | Controlled lab activity |  
| INC-003 | Local account creation | Wazuh Rule 5902 | Medium | Verify account creation and authorization | Controlled lab activity |  
| INC-004 | Authentication activity | Wazuh authentication logs | Medium | Review authentication context and correlate events | Reviewed |  
| INC-005 | Suspicious process execution | Wazuh Rule 80792 + auditd | Medium | Investigate process, parent, user, executable and timeline | Controlled lab activity |

\## INC-001 — SSH Brute Force

\### Triage  
\- Review authentication failures.  
\- Identify affected account.  
\- Correlate repeated SSH events.  
\- Review source activity.  
\- Determine whether activity is authorized.

\### Decision  
Security-relevant authentication activity requiring investigation.

\### Outcome  
The controlled SSH brute-force scenario was detected and documented.

\---

\## INC-002 — File Integrity Violation

\### Triage  
\- Identify the modified file.  
\- Compare original and modified state.  
\- Review the responsible user/process.  
\- Determine whether the modification was authorized.

\### Decision  
Security-relevant file modification requiring investigation.

\### Outcome  
Wazuh FIM successfully detected the controlled modification.

\---

\## INC-003 — Account Creation

\### Triage  
\- Identify the newly created account.  
\- Verify the account owner.  
\- Review privileges and group membership.  
\- Determine whether creation was authorized.

\### Decision  
Security-relevant account activity requiring investigation.

\### Outcome  
Wazuh Rule 5902 detected the controlled account creation.

\---

\## INC-004 — Authentication Activity

\### Triage  
\- Review successful and failed authentication.  
\- Identify affected account.  
\- Review source and timestamp.  
\- Correlate related authentication events.

\### Decision  
Authentication activity requiring contextual review.

\### Outcome  
The activity was reviewed as part of the laboratory monitoring workflow.

\---

\## INC-005 — Suspicious Process Activity

\### Triage  
\- Identify the executable.  
\- Identify the process ID.  
\- Identify the parent process.  
\- Identify the executing user.  
\- Review auditd evidence.  
\- Verify the executable type and hash.  
\- Reconstruct the execution timeline.

\### Decision  
Suspicious process execution requiring investigation.

\### Outcome  
Wazuh Rule 80792 detected the controlled process execution and the investigation confirmed that the executable was an exact copy of \`/usr/bin/sleep\`.

\---

\## Overall Triage Workflow

Security Event  
→ Detection  
→ Initial Triage  
→ Evidence Collection  
→ Investigation  
→ MITRE ATT&CK Assessment  
→ Decision  
→ Documentation  
→ Response/Cleanup