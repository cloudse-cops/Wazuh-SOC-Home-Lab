# Lessons Learned

## 1. SIEM Setup Requires Verification

A SOC platform is only useful when the manager, indexer, dashboard, and endpoint agent are communicating correctly. Service status and agent connectivity were verified before detection testing.

## 2. Baseline Activity Matters

Normal authentication and system activity were observed first. This provides a reference point for distinguishing expected behavior from suspicious activity.

## 3. Detection Rules Need Validation

Built-in Wazuh rules were examined and tested rather than assuming that every event would automatically generate the expected alert.

## 4. Log Sources Must Be Correctly Configured

Linux authentication logs, auditd, and Wazuh Agent log collection were verified so that security events reached the Wazuh Manager.

## 5. Audit Key Mapping Is Important

During process-monitoring work, the audit key initially did not match the Wazuh audit-key mapping. Changing the audit rule to use `audit-wazuh-c` allowed Rule 80792 to detect command execution correctly.

## 6. Alerts Need Investigation

A Wazuh alert alone is not enough. Process ID, parent process, user, executable path, file type, hash, and execution timeline were examined to understand the event.

## 7. Controlled Testing Improves Detection Validation

Security scenarios were generated in an isolated VirtualBox environment so that detections could be tested safely and repeatedly.

## 8. Evidence and Documentation Are Part of SOC Work

Raw logs, Wazuh alerts, investigation details, screenshots, detection notes, and incident reports were collected throughout the project.

## 9. Cleanup Is Important

Controlled test accounts, files, and suspicious-process artifacts were removed after investigation so the laboratory environment could return to a clean state.

## 10. Main Takeaway

The project demonstrated the complete defensive monitoring workflow:

Security Event → Collection → Detection → Alert → Investigation → Evidence → Documentation
