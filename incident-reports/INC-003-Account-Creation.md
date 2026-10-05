# \# INC-003 — New Account Creation

## \# 1. Incident Overview

| Field | Details |  
|---|---|  
| Incident ID | INC-003 |  
| Incident Title | New Account Creation |  
| Date | 2026-10-01 |  
| Status | Closed |  
| Severity | Medium |  
| Classification | True Positive — Controlled Lab Activity |  
| Affected Asset | arman-VirtualBox |  
| Agent ID | 001 |  
| Account Created | \`soc-test\` |  
| UID | 1001 |  
| GID | 1001 |  
| Home Directory | \`/home/soc-test\` |  
| Shell | \`/bin/bash\` |  
| Detection Source | Wazuh |  
| Wazuh Rule | 5902 |  
| Wazuh Rule Level | 8 |  
| Decoder | \`useradd\` |

## \# 2. Executive Summary

A controlled account-creation test was performed on the  
monitored Ubuntu endpoint \`arman-VirtualBox\`.

A temporary test account named \`soc-test\` was created using  
the Linux \`useradd\` command.

Wazuh collected the resulting system event and detected the  
new account using Rule 5902:

\> New user added to the system.

The investigation confirmed the account details, including  
the UID, GID, home directory, and login shell.

The account was intentionally created as part of the  
controlled SOC laboratory exercise. No evidence of  
unauthorized access or system compromise was identified.

## \# 3. Detection

Wazuh detected the account creation through the \`useradd\`  
decoder and Rule 5902.

| Field | Details |  
|---|---|  
| Rule ID | 5902 |  
| Rule Level | 8 |  
| Description | New user added to the system |  
| Decoder | \`useradd\` |  
| MITRE ATT&CK | T1136 — Create Account |

## \# 4. Test Scenario

A controlled test account was created on the endpoint:

\`\`\`text  
Username: soc-test  
UID: 1001  
GID: 1001  
Home: /home/soc-test  
Shell: /bin/bash  
\`\`\`

The purpose of the test was to validate that Wazuh could  
detect new local account creation.

## \# 5. Investigation Timeline

| Time | Event |  
|---|---|  
| 04:42:58 | Pre-test state checked |  
| 04:43:08 | \`useradd\` command executed |  
| 04:43:08 | New group \`soc-test\` created |  
| 04:43:08 | New user \`soc-test\` created |  
| 04:43:10 | Wazuh Rule 5902 alert observed |

## \# 6. Raw System Evidence

Linux recorded the following account-creation information:

\- New group: \`soc-test\`  
\- GID: \`1001\`  
\- New user: \`soc-test\`  
\- UID: \`1001\`  
\- Home directory: \`/home/soc-test\`  
\- Shell: \`/bin/bash\`

## \# 7. Wazuh Detection Evidence

Wazuh generated:

\> \*\*Rule 5902 — New user added to the system\*\*

with:

\`\`\`text  
Rule Level: 8  
Decoder: useradd  
\`\`\`

The Wazuh alert details also identified the MITRE ATT&CK  
mapping as:

\`\`\`text  
T1136 — Create Account  
\`\`\`

## \# 8. Investigation Findings

The account was created intentionally as part of the  
controlled SOC testing environment.

The Wazuh alert accurately reflected the underlying Linux  
account-creation event.

There was no evidence that the account was created by an  
unauthorized actor or used to compromise the system.

## \# 9. MITRE ATT&CK Mapping

| Field | Details |  
|---|---|  
| Tactic | Persistence |  
| Technique | T1136 — Create Account |  
| Wazuh Mapping | T1136 |  
| Observed Behavior | Creation of the \`soc-test\` account |

\### Rationale

The observed behavior was the creation of a new local user  
account. Wazuh maps this event to the MITRE ATT&CK  
Create Account technique.

In this project, the account was intentionally created as a  
controlled detection test rather than as a real malicious  
persistence action.

## \# 10. Classification

\*\*True Positive — Controlled Lab Activity\*\*

Wazuh correctly detected the account-creation event.

\### Impact Assessment

\- Successful compromise: No  
\- Unauthorized access: No evidence  
\- System compromise: No evidence  
\- Data compromise: No evidence  
\- Account purpose: Temporary SOC test account

## \# 11. Response

### \# Detection

Wazuh generated an alert for the creation of the new account.

### \# Investigation

The raw Linux logs and Wazuh alert details were reviewed to  
verify the account name, UID, GID, home directory, shell, and  
timestamp.

### \# Containment

The controlled test activity was stopped after the detection  
was confirmed.

### \# Recovery

No recovery action was required because this was a controlled  
test and no compromise occurred.

## \# 12. Lessons Learned

This exercise demonstrated how account-creation activity can  
be monitored and detected centrally using Wazuh.

It also demonstrated the importance of correlating the Wazuh  
alert with the underlying operating-system event before  
classifying an account-creation event as suspicious.

## \# 13. Final Status

\*\*Closed — Controlled Lab Exercise\*\*