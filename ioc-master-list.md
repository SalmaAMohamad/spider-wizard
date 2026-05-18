# IOC Master List

# IOC Master List

In a production SOC environment these IOCs would be ingested into a 
threat intelligence platform (MISP / OpenCTI), shared with sector 
ISACs, and used to generate blocking rules at the perimeter firewall, 
DNS sinkhole, and email gateway.

| IOC Type | Value | Description | Phase | Confidence | Action |
|----------|-------|-------------|-------|------------|--------|
| IP Address | 10.10.10.40 | ATTACK01 — C2 source / attacker host | 1–7 | High | Block at perimeter; alert on any internal contact |
| Network Port | TCP 4444 | Sliver / Meterpreter C2 default port | 1, 3 | High | Alert on any outbound non-standard port |
| File Name | invoice_Q3.exe | Initial reverse shell / beacon payload | 1 | High | Blocklist hash; alert on filename pattern |
| Process Chain | WINWORD.EXE → cmd.exe → powershell.exe | Office macro execution chain | 1 | High | Alert on Office → scripting host parent-child |
| Process | cscript.exe //E:jscript art.jse | OSTap payload execution | 1 | High | Alert: cscript.exe executing JS from Temp/Public |
| Scheduled Task | WindowsUpdateHelper | Persistence — disguised as Windows update | 2 | High | Alert: EID 4698 with task name not in approved list |
| NTLM Hash | Domain Admin hash (see Wazuh EID 10 alert) | Stolen Domain Admin credential | 4 | High | Invalidated via password reset; monitor re-use |
| File Extension | .CONTI | Ransomware encryption marker — Conti signature | 7 | High | FIM alert on mass extension change |
| File Name | HOW_TO_DECRYPT.txt | Conti ransomware note | 7 | High | FIM alert on creation; correlate with extension burst |
| Tool | cscript //E:jscript OSTapGet.js | OSTap downloader script | 1, 5 | High | Alert on cscript + OSTap filename combination |
| File Path | C:\Users\Public\art.jse | Attacker-dropped JS payload | 1 | High | FIM alert: file creation in C:\Users\Public\*.js |
| Archive | C:\Windows\Temp\exfil.zip | Data staging archive | 6 | High | FIM alert: zip creation in system Temp directory |

## Detection Rules Engineered

| Rule ID | Trigger | Level | Phase Covered |
|---------|---------|-------|---------------|
| 100010 | Sysmon EID 10 — TargetImage: lsass.exe | 15 CRITICAL | Credential Dumping |
| 100020 | FIM: 20+ events in 30 seconds | 15 CRITICAL | Data Staging / Ransomware |
| 100030 | Windows EID 4698 — scheduled task created | 12 HIGH | Persistence |