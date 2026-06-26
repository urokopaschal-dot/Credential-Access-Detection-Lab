# Incident Report

## Executive Summary

A credential access simulation was performed using Atomic Red Team to emulate attacker behavior targeting stored Windows credentials.

---

## Detection

Splunk detected execution of rundll32.exe with the command:

rundll32.exe keymgr,KRShowKeyMgr

The process was initiated successfully and recorded by Sysmon Event ID 1.

---

## Investigation

The analyst reviewed:

- Process Creation
- Parent Process
- Command Line
- User Account
- Execution Timeline

No additional malicious activity was observed beyond the controlled simulation.

---

## MITRE Mapping

Credential Access

T1003

---

## Conclusion

The environment successfully detected the simulated credential access technique, demonstrating that Sysmon and Splunk can identify suspicious executions of Windows utilities associated with credential harvesting.