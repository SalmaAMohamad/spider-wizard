# MITRE ATT&CK Mapping

# MITRE ATT&CK Full Mapping

All techniques map directly to documented Wizard Spider / Conti TTPs 
as referenced in CISA Advisory AA21-265A and the PWC Ireland HSE 
Post-Incident Review.

| Phase | Tactic | Technique ID | Technique Name | Tool | Wazuh Detection |
|-------|--------|--------------|----------------|------|-----------------|
| Initial Access | Initial Access | T1204.002 | User Execution: Malicious File | Atomic Red Team — Office macro → PowerShell → Sliver | Sysmon EID 1: WINWORD→cmd→PS chain |
| Initial Access | Initial Access | T1566.001 | Phishing: Spearphishing Attachment | Simulated maldoc delivery | N/A — social engineering vector |
| Persistence | Persistence | T1053.005 | Scheduled Task / Job | schtasks.exe — WindowsUpdateHelper | Windows EID 4698 + Rule 100030 → Level 12 |
| Persistence | Persistence | T1547.001 | Boot/Logon Autostart: Registry Run Keys | HKCU Run key audit | Wazuh FIM (planned) |
| C2 Beaconing | Command & Control | T1071.001 | Application Layer Protocol: Web | Sliver HTTP beacon — 30s interval | Sysmon EID 3: periodic outbound |
| C2 Beaconing | Command & Control | T1105 | Ingress Tool Transfer | PowerShell IEX download from GitHub | Sysmon EID 3: PS → raw.githubusercontent.com |
| Credential Dumping | Credential Access | T1003.001 | OS Credential Dumping: LSASS Memory | Kiwi (Mimikatz) via Sliver — creds_all | Sysmon EID 10 (lsass.exe) + Rule 100010 → Level 15 |
| Lateral Movement | Lateral Movement | T1021.002 | Remote Services: SMB/Windows Admin Shares | CrackMapExec Pass-the-Hash | Windows EID 4624: Logon Type 3, NTLM, src 10.10.10.40 |
| Lateral Movement | Lateral Movement | T1021.006 | Remote Services: WinRM | Evil-WinRM using domain admin credentials | EID 4624 (WinRM) + Sysmon EID 1: wsmprovhost.exe |
| Data Staging | Collection | T1074.001 | Data Staged: Local Data Staging | SMB shares → C:\Windows\Temp\stage + exfil.zip | Wazuh FIM: 50+ alerts across all 4 shares in 60s |
| Data Staging | Exfiltration | T1048 | Exfiltration Over Alternative Protocol | Simulated — archive created, channel not executed | FIM: exfil.zip creation in Temp |
| Ransomware | Impact | T1486 | Data Encrypted for Impact | PowerShell AES encryption → .CONTI + ransom note | FIM burst 20+ modifications in <30s + Rule 100020 → Level 15 |

## Coverage Summary

| Tactic | Techniques Covered |
|--------|--------------------|
| Initial Access | T1204.002, T1566.001 |
| Persistence | T1053.005, T1547.001 |
| Command & Control | T1071.001, T1105 |
| Credential Access | T1003.001 |
| Lateral Movement | T1021.002, T1021.006 |
| Collection | T1074.001 |
| Exfiltration | T1048 |
| Impact | T1486 |
| **Total** | **12 techniques across 8 tactics** |
