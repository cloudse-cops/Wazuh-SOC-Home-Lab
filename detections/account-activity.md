# \# Account Activity Detection

## \# 1. Objective

Detect the creation of new local user accounts on a monitored  
Ubuntu endpoint using Wazuh.

## \# 2. Detection Flow

\`\`\`text  
User Account Creation  
        ↓  
Linux useradd Event  
        ↓  
Wazuh Agent Collects Log  
        ↓  
useradd Decoder  
        ↓  
Wazuh Account-Creation Rule  
        ↓  
Rule 5902  
        ↓  
New User Added Alert  
        ↓  
SOC Investigation  
\`\`\`

## \# 3. Detection Rules Observed

| Rule ID | Level | Detection | Purpose |
| :---: | :---: | --- | --- |
| \*\*5901\*\* | \*\*8\*\* | New group added to the system | Detects creation of a new local group |
| \*\*5902\*\* | \*\*8\*\* | New user added to the system | Detects creation of a new local user account |
| \*\*5903\*\* | \*\*3\*\* | Group or user deleted from the system | Detects account or group deletion |
| \*\*5904\*\* | \*\*8\*\* | Information from the user was changed | Detects modification of user-account information |
| \*\*5905\*\* | \*\*0\*\* | Useradd failed | Detects failed user-creation attempts |

## \# 4. Detection Test

A controlled local account named \`soc-test\` was created on  
the monitored endpoint \`arman-VirtualBox\`.

The account was created using the Linux \`useradd\` command.

Account details:

\`\`\`text  
Username: soc-test  
UID: 1001  
GID: 1001  
Home: /home/soc-test  
Shell: /bin/bash  
\`\`\`

## \# 5. Detection Result

Wazuh successfully collected the account-creation event and  
processed it using the \`useradd\` decoder.

Wazuh then generated Rule \*\*5902\*\*:

\> New user added to the system.

The alert was generated with Rule Level \*\*8\*\*.

## \# 6. Detection Pipeline

\`\`\`text  
Linux Account Creation  
        ↓  
useradd  
        ↓  
System Log / Journald  
        ↓  
Wazuh Agent  
        ↓  
useradd Decoder  
        ↓  
Rule 5902  
        ↓  
Account Creation Alert  
\`\`\`

## \# 7. Configuration

The scenario uses Wazuh's built-in account-creation detection  
rules.

The monitored endpoint was configured with:

\- Wazuh Agent active  
\- Linux account-creation logs collected  
\- \`useradd\` decoder enabled  
\- Built-in account-activity rules enabled  
\- Wazuh Manager receiving the events

No custom account-creation detection rule was required.

## \# 8. Evidence

The detection was validated using:

\- Raw Linux account-creation logs  
\- \`soc-test\` account details  
\- Wazuh Rule 5902 alert  
\- Wazuh alert details  
\- MITRE ATT&CK mapping

## \# 9. MITRE ATT&CK

\*\*Tactic:\*\* Persistence

\*\*Technique:\*\* T1136 — Create Account

The Wazuh Rule 5902 alert maps the observed account-creation  
behavior to T1136.

## \# 10. Notes

The account was intentionally created as a controlled SOC  
laboratory test.

The detection demonstrates how a SOC can identify new local  
account creation and investigate the event centrally using  
Wazuh.