# \# SSH Brute Force Detection

## 1\. Objective

Detect repeated failed SSH authentication attempts against  
a monitored Ubuntu endpoint using Wazuh.

## 2\. Detection Flow

\`\`\`text  
SSH Authentication Attempt  
          ↓  
SSH Authentication Log  
          ↓  
Wazuh Agent Collects Event  
          ↓  
Wazuh SSH Decoder Parses Event  
          ↓  
Wazuh SSH Detection Rules Evaluate Event  
          ↓  
Repeated Failures Are Correlated  
          ↓  
Wazuh Rule 5763 Generates Brute-Force Alert  
\`\`\`

## 3\. Detection Rules Observed

| Rule ID | Level | Detection | Purpose |
| :---: | :---: | --- | --- |
| \*\*5710\*\* | \*\*5\*\* | SSH: Attempt to log in using a non-existent user | Detects login attempts against invalid or non-existent accounts |
| \*\*5716\*\* | \*\*5\*\* | SSH: Authentication failed | Detects an individual failed SSH authentication attempt |
| \*\*5720\*\* | \*\*10\*\* | SSH: Multiple authentication failures | Detects repeated SSH authentication failures |
| \*\*5763\*\* | \*\*10\*\* | SSH: Brute force trying to get access to the system — Authentication failed | Correlates repeated authentication failures and identifies possible SSH brute-force activity |

## 4\. Detection Test

A controlled SSH authentication test was performed against  
the \`arman-VirtualBox\` endpoint.

Eight incorrect password attempts were generated against  
the \`arman\` account within the configured detection window.

## 5\. Detection Result

Wazuh successfully collected the SSH authentication events  
and processed them using the built-in SSH detection rules.

After repeated authentication failures were observed,  
Wazuh triggered Rule \*\*5763\*\* with Rule Level \*\*10\*\*:

\> sshd: brute force trying to get access to the system. Authentication failed.

## 6\. Detection Pipeline

\`\`\`text  
SSH Authentication Attempt  
          ↓  
SSH Service / Authentication Logs  
          ↓  
Wazuh Agent  
          ↓  
SSH Decoder  
          ↓  
Wazuh SSH Rules  
          ↓  
Repeated Failure Correlation  
          ↓  
Rule 5763  
          ↓  
Brute-Force Alert  
\`\`\`

## 7\. Configuration

The SSH brute-force detection scenario uses Wazuh's  
built-in SSH detection rules.

The monitored endpoint was configured with:

\- OpenSSH server enabled and running  
\- SSH listening on TCP port 22  
\- Wazuh Agent connected to the Wazuh Manager  
\- SSH authentication logs collected by Wazuh  
\- Built-in SSH decoder and detection rules enabled

No custom SSH detection rule was required for this scenario.

## 8\. Evidence

The detection was validated using:

\- Raw SSH authentication failure logs  
\- Wazuh Rule 5710 alert  
\- Wazuh Rule 5763 brute-force alert  
\- Wazuh alert details  
\- Brute-force investigation timeline  
\- Endpoint SSH authentication logs

## 9\. MITRE ATT&CK

\*\*Tactic:\*\* Credential Access

\*\*Technique:\*\* T1110 — Brute Force

\*\*Sub-technique:\*\* T1110.001 — Password Guessing

## 10\. Notes

This project uses Wazuh's built-in SSH detection rules.

No custom SSH detection rule was required for this  
brute-force detection scenario.