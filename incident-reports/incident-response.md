\# Incident Response & Reporting

\## Objective

Document the incident response process used for the security scenarios completed in the Wazuh SOC laboratory.

The response workflow followed:

Detection → Triage → Investigation → Containment/Remediation → Recovery → Documentation → Lessons Learned

\---

\## INC-001 — SSH Brute Force

\### Detection

Wazuh detected SSH authentication failures and brute-force activity.

\### Triage

The authentication failures were reviewed to determine whether the activity represented repeated password-guessing behavior.

\### Investigation

The following evidence was reviewed:

\- SSH authentication logs  
\- Wazuh SSH detection alerts  
\- Invalid-user activity  
\- Brute-force alert details  
\- Incident timeline

\### Response

The activity was contained within the controlled laboratory environment.

The event was documented and reviewed as a simulated brute-force incident.

\### Recovery

The test environment was returned to its normal state after the investigation.

\### Final Status

Closed — Controlled SOC Laboratory Exercise

\---

\## INC-002 — File Integrity Violation

\### Detection

Wazuh File Integrity Monitoring detected a modification to a monitored file.

\### Triage

The affected file and the nature of the modification were reviewed.

\### Investigation

The following evidence was analyzed:

\- Original file state  
\- FIM configuration  
\- File modification evidence  
\- Wazuh alert  
\- Alert details

\### Response

The controlled file modification was investigated and the test environment was restored to its expected state.

\### Recovery

The monitored file was returned to the expected laboratory state.

\### Final Status

Closed — Controlled SOC Laboratory Exercise

\---

\## INC-003 — Account Creation

\### Detection

Wazuh Rule 5902 detected creation of the Linux account \`soc-test\`.

\### Triage

The new account was reviewed to determine whether the account creation was expected and authorized.

\### Investigation

The following were verified:

\- Username  
\- UID/GID  
\- Home directory  
\- Login shell  
\- Wazuh Rule 5902  
\- MITRE ATT&CK mapping

\### Response

The controlled test account was removed:

\`\`\`text  
sudo userdel -r soc-test