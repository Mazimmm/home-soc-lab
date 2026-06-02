# Investigation 04 — LSASS Memory Access (T1003.001)

## Summary
Detected suspicious LSASS process access consistent with credential
dumping behavior. Custom rule 100101 fired at level 12.

## Environment
- Victim: Windows 10 (192.168.48.131)
- SIEM: Wazuh 4.9.2 (192.168.48.128)

## Trigger
PowerShell opened a handle to LSASS process (PID 708)
with GrantedAccess: 0x101000

## Detection
- Sysmon EID 10 (ProcessAccess) generated on endpoint
- Forwarded to Wazuh via agent
- Custom rule 100101 fired at level 12
- MITRE T1003.001 tagged automatically

## Lessons Learned
- Windows Defender (MsMpEng.exe) also accesses LSASS legitimately
- Production rule should filter MsMpEng.exe to reduce false positives
- Rule chained off group sysmon_eid10_detections for reliability
