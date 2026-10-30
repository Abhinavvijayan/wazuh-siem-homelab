# Phase 2: Agent Deployment

## Environment
- New Ubuntu Server VM (Linux victim) — deployed in VirtualBox
- Windows 10 VM (Windows victim) — deployed in VirtualBox
- Both VMs: Bridged Adapter networking

## Installation Steps

### Windows Victim VM
1. Deployed a Windows 10 VM
2. Installed the Wazuh agent, registered it with the Wazuh manager
3. Downloaded Sysmon from Microsoft Sysinternals:
   https://download.sysinternals.com/files/Sysmon.zip
4. Downloaded Olaf Hartong's sysmon-modular config (`sysmonconfig.xml`) from GitHub
5. Added `sysmonconfig.xml` to the Sysmon folder

6. Opened PowerShell in that folder and installed Sysmon with the config:
   ```powershell
   .\Sysmon64.exe -accepteula -i sysmonconfig.xml
   ```

7. Verified install:
   ```powershell
   Get-Service Sysmon64
   ```

8. Opened Notepad as Administrator, navigated to:
   C:\Program Files (x86)\ossec-agent\ossec.conf

   and modified the file to point to the Sysmon event channel:
   ```xml
   <localfile>
     <location>Microsoft-Windows-Sysmon/Operational</location>
     <log_format>eventchannel</log_format>
   </localfile>
   ```

9. Confirmed agent shows as **Active** in the Wazuh dashboard

### Linux Victim VM
1. Deployed a second Ubuntu Server VM
2. Installed the Wazuh agent, registered it with the Wazuh manager
3. Installed Sysmon for Linux (official Microsoft package):
   ```bash
   wget -q https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
   sudo dpkg -i packages-microsoft-prod.deb
   sudo apt-get update
   sudo apt-get install sysmonforlinux
   ```
4. Downloaded Microsoft's MSTIC-Sysmon Linux config (`collect-all.xml`), sourced via MyDFIR's YouTube tutorial:
   ```bash
   wget https://raw.githubusercontent.com/microsoft/MSTIC-Sysmon/refs/heads/main/linux/configs/collect-all.xml
   ```
5. Applied the config:
   ```bash
   sudo sysmon -i collect-all.xml
   ```
6. Confirmed agent shows as **Active** in the Wazuh dashboard

## Result
Both Linux and Windows victim VMs deployed with Wazuh agents installed 
and reporting as Active. Sysmon installed on both — Sysmon for Linux 
with Microsoft's MSTIC collect-all config on Ubuntu, and Sysmon on 
Windows with Olaf Hartong's sysmon-modular config — providing detailed 
process, network, and system event logging beyond default OS logs, 
ready for attack simulation in Phase 3.
