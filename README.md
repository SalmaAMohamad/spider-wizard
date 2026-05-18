# 🕷️ Spider Wizard SOC Home Lab

> Adversarial emulation of the **Wizard Spider / Conti ransomware attack**  
> against HSE Ireland (May 2021) — built as a DEPI SOC Analyst 2026 deliverable.

---

## 📌 Overview

Spider Wizard is a fully functional SOC home lab that simulates a real-world  
nation-disrupting ransomware campaign from initial phishing to full domain  
encryption — and detects every phase using a custom-tuned Wazuh SIEM.

| Detail | Value |
|--------|-------|
| **Threat Actor** | Wizard Spider (Conti ransomware) |
| **Real Incident** | HSE Ireland — May 14, 2021 |
| **Framework** | PICERL Incident Response |
| **SIEM** | Wazuh 4.7 |
| **Domain** | spider.local — 10.10.10.0/24 |
| **Team Leader** | Salma Ali Mohamed |

> ⚠️ **SIMULATION NOTICE:** All techniques were executed exclusively within  
> an isolated lab environment against systems owned by the analyst.

---

## 🏗️ Lab Architecture

| Asset | Role | IP | OS |
|-------|------|----|----|
| DC01 | Domain Controller / DNS | 10.10.10.10 | Windows Server 2022 |
| FS01 | File Server / FIM Target | 10.10.10.20 | Windows Server 2022 |
| WAZUH01 | SIEM Manager + Router | 10.10.10.30 | Ubuntu 24.04 LTS |
| WS-EMP01 | Employee Workstation | Tailscale VPN | Windows 10 22H2 |
| ATTACK01 | Red Team Host (isolated) | 10.10.10.40 | Kali Linux 2026.1 |

---

## ⚔️ Attack Chain — 7 Phases

| # | Phase | MITRE ID | Tool | Detection |
|---|-------|----------|------|-----------|
| 1 | Initial Access | T1204.002 | Office macro → Sliver | Sysmon EID 1 |
| 2 | Persistence | T1053.005 | schtasks.exe | Windows EID 4698 |
| 3 | C2 Beaconing | T1071.001 | Sliver HTTP beacon | Sysmon EID 3 |
| 4 | Credential Dumping | T1003.001 | Mimikatz / Kiwi | Sysmon EID 10 + Rule 100010 |
| 5 | Lateral Movement | T1021.002 | CrackMapExec PtH | Windows EID 4624 |
| 6 | Data Staging | T1074.001 | SMB copy + zip | Wazuh FIM burst |
| 7 | Ransomware | T1486 | PowerShell AES | FIM + Rule 100020 |

---

## 🛡️ Custom Wazuh Rules

| Rule ID | Trigger | Level | Phase |
|---------|---------|-------|-------|
| 100010 | Sysmon EID 10 — lsass.exe access | 15 CRITICAL | Credential Dumping |
| 100020 | FIM burst — 20+ events in 30s | 15 CRITICAL | Ransomware |
| 100030 | Windows EID 4698 — scheduled task | 12 HIGH | Persistence |

---

## 📊 Key Results

| Metric | Result |
|--------|--------|
| Kill-chain phases detected | **7 / 7** |
| C2 beacon identified within | **< 30 minutes** |
| Custom rules engineered | **3** |
| MITRE ATT&CK techniques mapped | **12 across 8 tactics** |
| Environment restored from snapshot | **< 10 minutes** |

---

## 📁 Repository Structure
