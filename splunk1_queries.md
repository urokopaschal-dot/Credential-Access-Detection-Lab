# Process Creation

index=sysmon EventCode=1 Image="*rundll32.exe"

---

# Command Line Detection

index=sysmon EventCode=1 CommandLine="*KRShowKeyMgr*"

---

# Timeline

index=sysmon Image="*rundll32.exe"
| table _time User Computer Image CommandLine ParentImage
| sort _time

---

# Process Statistics

index=sysmon EventCode=1
| stats count by Image