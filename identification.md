# Identification

# Phase 2 — Identification

> Determine with confidence that a security incident is underway and 
> collect sufficient evidence to establish a complete attack timeline.

## Kill Chain Timeline

| Phase | MITRE ID | T+ | Action | Wazuh Detection |
|-------|----------|----|--------|-----------------|
| Initial Access | T1204.002 | T+0 | Office macro → cmd → PowerShell → Sliver beacon | Sysmon EID 1: WINWORD→cmd→PowerShell chain |
| Persistence | T1053.005 | T+15 | Scheduled task 'WindowsUpdateHelper' created | Windows EID 4698 |
| C2 Beaconing | T1071.001 | T+30 | Sliver HTTP beacon every 30 seconds | Sysmon EID 3: periodic outbound |
| Credential Dumping | T1003.001 | T+60 | Mimikatz/Kiwi — LSASS memory access | Sysmon EID 10 + Custom Rule 100010 → Level 15 |
| Lateral Movement | T1021.002 | T+90 | Pass-the-Hash via CrackMapExec to FS01 & DC01 | Windows EID 4624: NTLM Logon Type 3 |
| Data Staging | T1074.001 | T+120 | All 4 SMB shares copied to C:\Windows\Temp\stage | Wazuh FIM: 50+ alerts in 60s |
| Ransomware | T1486 | T+150 | 30 files encrypted → .CONTI extension | FIM burst + Custom Rule 100020 → Level 15 |

## Incident Classification

| Attribute | Value |
|-----------|-------|
| Type | Targeted Ransomware / APT |
| Severity | CRITICAL |
| Scope | WS-EMP01 → FS01 → DC01 |
| Initial Vector | Phishing — Office macro (T1204.002) |
| Dwell Time (lab) | T+0 to T+150 minutes |
| Credential Exposure | Domain Admin NTLM hash |
