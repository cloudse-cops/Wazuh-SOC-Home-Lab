# \# INC-002 — File Integrity Violation

## \# 1. Incident Overview

| Field | Details |
| --- | --- |
| Incident ID | INC-002 |
| Incident Title | File Integrity Violation |
| Date | 2026-09-30 |
| Status | Closed |
| Severity | Medium |
| Classification | True Positive — Controlled Lab Activity |
| Affected Asset | arman-VirtualBox |
| Agent ID | 001 |
| File | \`/home/arman/wazuh-fim-test/fim-test.txt\` |
| Detection Source | Wazuh File Integrity Monitoring |
| Wazuh Rule | 550 |
| Wazuh Rule Level | 7   |
| Monitoring Mode | Realtime |

## \# 2. Executive Summary

A controlled file modification was performed on the monitored  
Ubuntu endpoint \`arman-VirtualBox\` to validate Wazuh File  
Integrity Monitoring (FIM).

The monitored file \`fim-test.txt\` was modified by appending  
controlled test content. Wazuh detected the modification and  
generated Rule 550:

\> Integrity checksum changed.

The investigation confirmed changes to the file size,  
modification time, MD5, SHA-1, and SHA-256 values.

The activity was intentionally performed as part of the  
controlled SOC laboratory and there was no evidence of  
unauthorized access or system compromise.

## \# 3. Detection

Wazuh FIM was configured for realtime monitoring of:

\`/home/arman/wazuh-fim-test\`

The modification of \`fim-test.txt\` triggered:

| Field | Details |
| --- | --- |
| Rule ID | 550 |
| Rule Level | 7   |
| Event | Integrity checksum changed |
| FIM Event | modified |
| Monitoring Mode | realtime |

## \# 4. Test Scenario

The original file state was recorded before modification.

### \# Before Modification

| Attribute | Value |
| --- | --- |
| Content | \`This is my first FIM test\` |
| Size | 26 bytes |
| SHA-256 | \`2fb0ae1b6fa87e40e5002d366deb72f3f68b2dcfc759da499fd599297a2a6b4c\` |

A controlled line was then appended to the file:

\`Controlled FIM modification for INC-002\`

### \# After Modification

| Attribute | Value |
| --- | --- |
| Content | Original content + controlled modification |
| SHA-256 | \`8e3d90ffafef3c0414ab2bf924b64fc0999446bc795c368b1a301e05a4371b6e\` |

## \# 5. Investigation Findings

Wazuh reported that the following file attributes changed:

\- Size  
\- Modification time  
\- MD5  
\- SHA-1  
\- SHA-256

The SHA-256 value reported by Wazuh after the modification  
matched the SHA-256 value independently calculated on the  
endpoint.

This confirms that the file content was actually changed and  
that Wazuh successfully detected the integrity modification.

## \# 6. Evidence

The investigation was supported by:

\- Original file state and SHA-256 hash  
\- Modified file and new SHA-256 hash  
\- Wazuh FIM alert  
\- Wazuh Rule 550 event details  
\- Realtime FIM monitoring evidence

## \# 7. MITRE ATT&CK Mapping

| Field | Details |
| --- | --- |
| Tactic | Impact |
| Technique | T1565 — Data Manipulation |
| Sub-technique | T1565.001 — Stored Data Manipulation |
| Wazuh Mapping | T1565.001 |

### \# Rationale

Wazuh mapped the observed file modification to  
T1565.001 — Stored Data Manipulation.

In this project, however, the file modification was  
intentionally generated as a controlled FIM test and was not  
performed by a real attacker.

## \# 8. Classification

\*\*True Positive — Controlled Lab Activity\*\*

Wazuh correctly detected the file integrity change.

### \# Impact Assessment

\- Successful compromise: No  
\- Unauthorized access: No evidence  
\- System compromise: No evidence  
\- Data compromise: No evidence

## \# 9. Response

### \# Detection

Wazuh FIM detected the monitored file modification.

### \# Containment

The controlled test activity was stopped after the detection  
was confirmed.

### \# Investigation

The original and modified file states were compared using  
content, metadata, and SHA-256 hashes.

### \# Recovery

No recovery action was required because this was a controlled  
test and no system compromise occurred.

## \# 10. Lessons Learned

This exercise demonstrated how File Integrity Monitoring can  
identify changes to protected or monitored files.

The investigation also demonstrated the importance of comparing  
before-and-after file hashes and metadata instead of relying  
only on the alert description.

## \# 11. Final Status

\*\*Closed — Controlled Lab Exercise\*\*