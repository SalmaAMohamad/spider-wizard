# Introduction

# Spider Wizard SOC Home Lab

A high-fidelity adversarial emulation of the Wizard Spider / Conti 
ransomware attack against HSE Ireland (May 2021), built as a DEPI 
SOC Analyst 2026 program deliverable.

## What is Spider Wizard?

Spider Wizard is a SOC home lab that simulates a real-world 
ransomware attack from initial phishing to full domain encryption — 
and detects every phase using Wazuh SIEM.

**Threat Actor:** Wizard Spider (Conti ransomware)  
**Real Incident:** HSE Ireland — May 14, 2021  
**Framework:** PICERL (Preparation → Identification → Containment → 
Eradication → Recovery → Lessons Learned)  
**SIEM:** Wazuh 4.7  
**Domain:** spider.local | 10.10.10.0/24  

> ⚠️ SIMULATION NOTICE: All techniques were executed exclusively 
> within an isolated lab environment against systems owned by the analyst.

## Real-World Impact (HSE 2021)

| Metric | Value |
|--------|-------|
| Endpoints encrypted | 80,000+ |
| Patients affected | 1,000,000 |
| Undetected dwell time | 57 days |
| Remediation cost | €100M+ |
| Recovery time | 6+ months |
