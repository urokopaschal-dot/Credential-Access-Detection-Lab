# MITRE ATT&CK Mapping

Technique:
OS Credential Dumping

Technique ID:
T1003

Sub-technique:
Credential Manager

Description:

This Atomic Red Team test executed
rundll32.exe keymgr,KRShowKeyMgr
to simulate access to Windows Credential Manager.

Although this specific test did not dump credentials from LSASS memory, it demonstrated a credential access technique that defenders should monitor.

Detection Source

Sysmon Event ID 1

Splunk

Windows Process Creation Logs