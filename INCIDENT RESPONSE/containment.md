# Containment

# Phase 3 — Containment

> Prevent the attack from propagating further. Speed takes precedence 
> — every minute of uncontained C2 risks additional credential theft 
> and encryption.

## Short-Term Actions (<15 Minutes)

| Action | Method | Rationale |
|--------|--------|-----------|
| Isolate WS-EMP01 | Disable VMware NIC / Tailscale | Severs active C2 channel |
| Disable compromised AD account | Disable emp01 in ADUC | Invalidates session tokens |
| Block ATTACK01 at SIEM | iptables DROP on WAZUH01 | Protects SIEM logs from tampering |
| Preserve volatile memory | VM snapshot (live state) | Captures in-memory forensic artefacts |
| Open incident ticket | Document T0, IOCs, scope | Establishes chain of custody |

## Long-Term Actions

- Reset Domain Administrator password — invalidates all NTLM hashes
- Disable WinRM on FS01 and DC01 (TCP 5985/5986)
- Enforce SMB signing on all domain members
- Restrict anonymous share access
- Enable Wazuh Level 10+ email notifications
- Verify DC01 and FS01 telemetry continuity

> ⚠️ **CRITICAL:** Do NOT reimage WS-EMP01 before forensic evidence 
> collection. Reimaging destroys volatile memory, registry persistence 
> keys, and prefetch artefacts essential for the attack timeline.
