# Home SOC Lab with Wazuh

A hands-on SOC lab built to practice detection engineering and incident 
analysis — simulating real attack techniques and building/tuning Wazuh 
detections to catch them.

## 🎯 Goal
Build a working SIEM environment, simulate common attack techniques 
mapped to MITRE ATT&CK, and document what gets detected out-of-the-box 
vs. what requires custom detection rules.

## 🏗️ Architecture
*(diagram coming soon)*

- **Wazuh Server** (Ubuntu Server 24.04) — manager, indexer, dashboard
- **Windows Victim VM** — Windows 10 monitored via Wazuh agent
- **Kali Linux VM** — attack simulation

## 🛠️ Tools Used
- VirtualBox
- Wazuh 4.x
- Ubuntu Server 24.04 LTS
- Windows 10
- Kali Linux

## 📋 Project Phases
- [x] Phase 1: Deploy Wazuh server
- [ ] Phase 2: Deploy and connect Windows agent
- [ ] Phase 3: Simulate attacks and document detections
- [ ] Phase 4: Write custom detection rules
- [ ] Phase 5: Final write-up and summary table

## 📁 Repo Structure
