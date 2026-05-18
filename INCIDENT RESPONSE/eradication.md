# Eradication

# Phase 4 — Eradication

> Remove every attacker artefact — payloads, persistence mechanisms, 
> and stolen credentials.

## WS-EMP01

| Task | Status |
|------|--------|
| Terminate Sliver beacon (invoice_Q3.exe) | ✅ Done |
| Delete scheduled task WindowsUpdateHelper | ✅ Done |
| Remove payload from C:\Users\Public\ | ✅ Done |
| Remove C:\RansomSimLab directory | ✅ Done |
| Audit Run / RunOnce registry keys | ✅ Done |
| Atomic Red Team cleanup (T1204.002) | ✅ Done |
| Verify no connections to port 4444 | ✅ Done |

## FS01

| Task | Status |
|------|--------|
| Remove C:\Windows\Temp\stage\ | ✅ Done |
| Delete exfil.zip | ✅ Done |
| Audit share access logs (EID 4663) | ✅ Done |
| Confirm OSTap artefacts removed | ✅ Done |

## Active Directory — Credential Eradication

- 🔑 Reset Domain Administrator password
- 🔑 Reset emp01 password and re-enable account
- 🔑 Purge all Kerberos tickets across domain (klist purge)
- 🔑 Verify no rogue accounts created during attack window
