# Recovery

# Phase 5 — Recovery

> Restore affected systems to full operational status and verify 
> integrity before reconnecting to production networks.

## Recovery Validation Checklist

| Check | Expected Result | Status |
|-------|-----------------|--------|
| All Wazuh agents Active | DC01, FS01, WS-EMP01 green | ✅ Verified |
| No WindowsUpdateHelper task | Task absent on WS-EMP01 | ✅ Verified |
| No invoice_Q3.exe on disk | File absent — hash check clean | ✅ Verified |
| SMB shares accessible by emp01 | Read/write access confirmed | ✅ Verified |
| Domain logon functional | emp01@spider.local authenticates | ✅ Verified |
| No C2 in Wazuh (EID 3) | Zero connections to 10.10.10.40 | ✅ Verified |
| Alert volume at baseline | Matches pre-attack 30-min window | ✅ Verified |
| No .CONTI files on FS01 | FIM query + dir check clean | ✅ Verified |

## Post-Recovery Monitoring (72-hour window)

- Wazuh email alerts enabled for all Level 10+ events
- Manual dashboard review every 4 hours
- Active watch: new scheduled tasks, new AD accounts, SMB anomalies
- Any re-emergence of 10.10.10.40 in Sysmon EID 3 → immediate re-containment

> **HSE Lesson:** The HSE discovered additional Cobalt Strike implants 
> weeks after cleanup as surviving beacons reactivated. Extended 
> post-recovery monitoring would have caught reactivation within minutes.