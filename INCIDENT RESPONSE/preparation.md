# Preparation

# Phase 1 — Preparation

> Establish the people, processes, and technology required to detect 
> and respond to a targeted ransomware intrusion before any attack occurs.

## Team Roles

| Role | Tier | Assigned To |
|------|------|-------------|
| Team Leader | N/A | Salma Ali Mohamed |
| SOC Analyst | Tier 1 | Mohamed Atef |
| Incident Responder | Tier 2 | Youssef Sharqawy |

## Alert Triage Policy

| Wazuh Level | Severity | Response Time |
|-------------|----------|---------------|
| 5–7 | Informational | Next business day |
| 8–11 | Low / Medium | Within 4 hours |
| 12–14 | High | Within 30 minutes |
| 15 | CRITICAL | Within 15 minutes |

## Pre-Attack Checklist

- ✅ All Wazuh agents Active (DC01, FS01, WS-EMP01)
- ✅ Sysmon v15 running on all Windows VMs
- ✅ FIM configured on C:\Shares (realtime)
- ✅ Security + Sysmon event channels in ossec.conf
- ✅ 30-minute clean alert baseline captured
- ✅ VM snapshots taken on all machines
- ✅ Wazuh credentials stored offline (encrypted vault)
- ✅ Attack scope agreement signed
