# Lessons Learned

# Phase 6 — Lessons Learned

> Convert reactive incident response experience into proactive 
> defensive improvement. Every finding must produce a specific, 
> measurable, assigned remediation action.

## What Worked

- ✅ Sysmon + Wazuh produced full process-level telemetry — complete 
  attack chain reconstructed from a single query interface
- ✅ FIM on C:\Shares detected both data staging and ransomware burst
- ✅ WAZUH01 dual-NIC kept SIEM operational throughout WS-EMP01 isolation
- ✅ Custom rules 100010 and 100020 closed two critical detection gaps
- ✅ VM snapshots enabled clean environment restore in under 10 minutes

## Detection Gaps Identified

| Gap | Phase | Fix Applied |
|-----|-------|-------------|
| LSASS access not auto-escalated to Critical | Phase 4 | Custom Rule 100010 → Level 15 |
| Pass-the-Hash indistinguishable from normal logon | Phase 5 | EID 4624 + NTLM + baseline correlation |
| FIM burst not auto-escalated | Phase 6–7 | Custom Rule 100020 (frequency rule) |
| Office macro chain not correlated as single event | Phase 1 | Planned: parent-child chain rule |

## Remediation Register

| Action | Priority | Status |
|--------|----------|--------|
| Deploy Rule 100010 (LSASS → Level 15) | CRITICAL | ✅ Deployed |
| Deploy Rule 100020 (FIM burst → Level 15) | CRITICAL | ✅ Deployed |
| Deploy Rule 100030 (Scheduled task → Level 12) | HIGH | ✅ Deployed |
| Enable SMB signing on DC01 and FS01 | HIGH | 📋 Planned |
| Enable Credential Guard on WS-EMP01 | HIGH | 📋 Planned |
| Wazuh email alerting for Level 10+ | HIGH | 📋 Planned |
| Restrict WinRM to admin subnet only | MEDIUM | 📋 Planned |