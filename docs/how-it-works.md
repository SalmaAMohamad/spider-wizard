# Lab Architecture

# Lab Architecture

## Network Design

| Detail | Value |
|--------|-------|
| Network | 10.10.10.0/24 (VMware Host-Only) |
| Remote access | Tailscale VPN (subnet router on WAZUH01) |
| Attack host | ATTACK01 — isolated, simulation phases only |

## Asset Register

| Asset | Hostname | Role | IP | OS | Criticality |
|-------|----------|------|----|----|-------------|
| SRV-DC01 | DC01 | Domain Controller / DNS | 10.10.10.10 | Windows Server 2022 | CRITICAL |
| SRV-FS01 | FS01 | File Server / FIM Target | 10.10.10.20 | Windows Server 2022 | HIGH |
| SRV-WAZUH01 | WAZUH01 | SIEM Manager + Router | 10.10.10.30 | Ubuntu 24.04 LTS | HIGH |
| CL-EMP01 | WS-EMP01 | Employee Workstation | Tailscale VPN | Windows 10 22H2 | MEDIUM |
| PLN-ATK01 | ATTACK01 | Red Team Host (isolated) | 10.10.10.40 | Kali Linux 2026.1 | N/A |

## SOC Technology Stack

| Component | Tool | Purpose |
|-----------|------|---------|
| SIEM | Wazuh 4.7 | Central log management, alerting, dashboards |
| Endpoint Logging | Sysmon v15 | Process, network, file, registry telemetry |
| FIM | Wazuh FIM (realtime) | File Integrity Monitoring on C:\Shares |
| C2 Simulation | Sliver C2 / Metasploit | Beacon generation and post-exploitation |
| ATT&CK Emulation | Atomic Red Team | MITRE-mapped TTP execution |
| Network | VMware + Tailscale VPN | Isolated lab + remote access simulation |
