# \# File Integrity Monitoring Detection

## \# 1. Objective

Detect unauthorized or unexpected modifications to monitored  
files using Wazuh File Integrity Monitoring (FIM).

## \# 2. FIM Configuration

The Wazuh Agent monitors the following directory in realtime:

\`\`\`text  
/home/arman/wazuh-fim-test  
\`\`\`

The monitored test file is:

\`\`\`text  
/home/arman/wazuh-fim-test/fim-test.txt  
\`\`\`

## \# 3. Detection Flow

\`\`\`text  
File Modification  
        ↓  
Wazuh FIM / Syscheck  
        ↓  
File Attributes Compared  
        ↓  
Hash / Metadata Change Detected  
        ↓  
Wazuh Rule 550  
        ↓  
Integrity Checksum Changed Alert  
        ↓  
SOC Analyst Investigation  
\`\`\`

## \# 4. Detection Rule

| Rule ID | Level | Detection |  
|:---:|:---:|---|  
| \*\*550\*\* | \*\*7\*\* | Integrity checksum changed |

\## 5. Test Scenario

A controlled modification was made to the monitored file:

\`\`\`text  
fim-test.txt  
\`\`\`

The original file contained:

\`\`\`text  
This is my first FIM test  
\`\`\`

A controlled test line was then appended:

\`\`\`text  
Controlled FIM modification for INC-002  
\`\`\`

## \# 6. Hash Comparison

| State | SHA-256 |  
|---|---|  
| Before modification | \`2fb0ae1b6fa87e40e5002d366deb72f3f68b2dcfc759da499fd599297a2a6b4c\` |  
| After modification | \`8e3d90ffafef3c0414ab2bf924b64fc0999446bc795c368b1a301e05a4371b6e\` |

The difference between the two SHA-256 values confirms that  
the file contents changed.

## \# 7. Attributes Monitored

Wazuh reported changes to:

\- File size  
\- Modification time  
\- MD5  
\- SHA-1  
\- SHA-256

## \# 8. Detection Result

Wazuh successfully detected the file modification and  
generated Rule \*\*550\*\* with Level \*\*7\*\*.

The event was reported as:

\> Integrity checksum changed.

## \# 9. Configuration

The FIM scenario uses Wazuh's built-in File Integrity  
Monitoring functionality.

Configuration includes:

\- Realtime FIM monitoring  
\- Monitored directory configured  
\- Wazuh Agent active  
\- Syscheck/FIM module enabled  
\- Wazuh Manager receiving FIM events

No custom FIM detection rule was required.

## \# 10. Evidence

The detection was validated using:

\- Original file state  
\- Original SHA-256 hash  
\- Modified file state  
\- New SHA-256 hash  
\- Wazuh Rule 550 alert  
\- Wazuh FIM event details

## \# 11. MITRE ATT&CK

Wazuh mapped the observed file modification to:

\*\*T1565.001 — Stored Data Manipulation\*\*

The modification in this project was intentionally generated  
as a controlled FIM test.