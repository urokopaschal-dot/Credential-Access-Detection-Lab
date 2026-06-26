# LSASS Credential Access Investigation Lab

## Project Overview

This project demonstrates how a Security Operations Center (SOC) analyst can detect and investigate a credential access technique using Splunk, Sysmon, and Atomic Red Team.

The objective was to simulate attacker behavior targeting Windows credentials, generate endpoint telemetry, investigate the activity, and map the findings to the MITRE ATT&CK framework.

---

# Lab Environment

* Windows 10 Virtual Machine
* Splunk Enterprise
* Sysmon
* PowerShell 7
* Atomic Red Team

---

# Objective

The goal of this lab was to:

* Simulate a credential access technique.
* Generate Windows event logs.
* Detect the activity using Splunk.
* Investigate the executed process.
* Build an investigation timeline.
* Map the activity to MITRE ATT&CK.
* Document the findings in an incident report.

---

# Attack Simulation

Atomic Red Team Test Executed:

**Technique:** T1003 – OS Credential Dumping

**Atomic Test Number:** 6

Command executed:

```powershell
Invoke-AtomicTest T1003 -TestNumbers 6 -PathToAtomicsFolder "C:\AtomicRedTeam\atomics"
```

This test launched the following Windows command:

```cmd
rundll32.exe keymgr,KRShowKeyMgr
```

The command opens the Windows Credential Manager interface, demonstrating a credential access technique that defenders should be able to detect and investigate.

---

# Detection

### Process Creation Detection

Splunk Query:

```spl
index=sysmon EventCode=1 Image="*rundll32.exe"
```

### Command Line Detection

```spl
index=sysmon EventCode=1 CommandLine="*KRShowKeyMgr*"
```

### Investigation Timeline

```spl
index=sysmon Image="*rundll32.exe"
| table _time User Computer Image CommandLine ParentImage
| sort _time
```

---

# Investigation Findings

The investigation confirmed that the Atomic Red Team simulation successfully executed `rundll32.exe` with the `keymgr,KRShowKeyMgr` argument.

Sysmon recorded the process creation event, and Splunk successfully collected and displayed the telemetry. The command line clearly identified the execution of the Credential Manager function, allowing the activity to be investigated through process details and timeline analysis.

Because this was a controlled simulation performed in a lab environment, no malicious changes were made to the system.

---

# MITRE ATT&CK Mapping

| Tactic            | Technique             | Technique ID |
| ----------------- | --------------------- | ------------ |
| Credential Access | OS Credential Dumping | T1003        |

---

# Skills Demonstrated

* Threat Detection
* Splunk Log Analysis
* Sysmon Event Analysis
* PowerShell Investigation
* Atomic Red Team Simulation
* MITRE ATT&CK Mapping
* Incident Investigation
* Process Analysis
* Timeline Analysis
* SOC Analyst Workflow

---

# Project Structure

```text
LSASS-Credential-Access-Investigation-Lab
│
├── README.md
├── Screenshots
├── Queries
├── Reports
└── MITRE
```

---

# Screenshots

Include the following screenshots in the `Screenshots` folder:

* Atomic Red Team execution
* Credential Manager window
* Splunk process creation detection
* Process details
* Investigation timeline

---

# Lessons Learned

This project demonstrated how Atomic Red Team can safely simulate attacker techniques in a controlled environment. It also reinforced the importance of endpoint telemetry collected by Sysmon and how Splunk can be used to identify, investigate, and analyze suspicious process execution associated with credential access techniques.

---

# Conclusion

This lab successfully demonstrated the detection and investigation of a simulated credential access technique. By combining Atomic Red Team, Sysmon, and Splunk, the project showed how a SOC analyst can identify suspicious process execution, analyze command-line activity, and map findings to the MITRE ATT&CK framework. The investigation process reflects a practical workflow that can be applied to real-world security monitoring and incident response.
