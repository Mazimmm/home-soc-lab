# Investigation 03 — Encoded PowerShell Execution (T1059.001)

## Summary
Encoded PowerShell was executed on the Windows victim endpoint.
Default Wazuh rules caught the Sysmon event but only at level 3 — 
not actionable. Custom rule 100100 now elevates this to level 10.

## Environment
- Attacker: Kali Linux (192.168.48.132)
- Victim: Windows 10 (192.168.48.131)
- SIEM: Wazuh 4.9.2 (192.168.48.128)

## Attack Command
```cmd
powershell.exe -NoProfile -ExecutionPolicy Bypass -EncodedCommand
VwByAGkAdABlAC0ASABvAHMAdAAgACIASABlAGwAbABvACAAZgByAG8AbQAgAHQAaABlACAATABhAGIAIQAiAA==
```
Decoded payload: `Write-Host "Hello from the Lab!"` — benign but
identical in structure to real malicious encoded PowerShell.

## Detection Gap
Default rule 92032 fired at level 3 (too low to action).
No semantic meaning was attached to the encoded command flag.

## Custom Rule Deployed
Rule ID: 100100 | Level: 10
Matches Sysmon EID 1 where powershell.exe is launched with
-EncodedCommand, -enc, or -e flags.

## MITRE ATT&CK
- Tactic: Execution
- Technique: T1059.001 — PowerShell

## Timeline
- Sysmon EID 1 generated on victim endpoint
- Event forwarded to Wazuh via agent
- Custom rule 100100 fired at level 10
- Alert visible in Wazuh dashboard

## Lessons Learned
- Default rules are insufficient for obfuscated execution
- Sysmon EID 1 + command line matching is effective
- False positive risk: Chocolatey installer uses -EncodedCommand
  Mitigation: filter by parent process (msiexec.exe)
