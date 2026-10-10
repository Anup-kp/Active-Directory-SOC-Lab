# Enterprise Active Directory & Splunk SOC Lab (`MyDFIR`)

## 🚀 Project Overview
This project simulates an on-premise corporate network environment to practice security monitoring, Active Directory administration, adversary emulation, and SIEM log analysis. The lab is built from scratch to observe real-world attack telemetry and triage alerts using Splunk Enterprise.

## 🏗️ Architecture & Topology
* **Domain Name:** `MyDFIR`
* **Network Subnet:** `192.168.10.0/24`
* **Splunk SIEM Server (Ubuntu 22.04):** `192.168.10.10` (Port 9997 data ingestion)
* **Active Directory Domain Controller (Windows Server 2022):** `192.168.10.7`
* **Target Endpoint (Windows 10 Pro):** `192.168.10.100`
* **Attacker Machine (Kali Linux):** `192.168.10.250`

![Network Architecture Diagram](images/architecture.png)

## 🛠️ Implementation Steps
1. **Network Configuration:** Configured static IP addressing across all VMs within a dedicated VirtualBox internal network segment (`192.168.10.0/24`).
2. **Active Directory Deployment:** Promoted Windows Server to a Domain Controller (`MyDFIR`), created organizational units (OUs), and joined the Windows 10 target machine to the domain.
3. **Telemetry & Forwarding:** Installed **Splunk Universal Forwarders** and **Sysmon** (with Olaf's configuration) on Windows endpoints. Configured custom `inputs.conf` files to ingest Application, Security, System, and Sysmon event logs directly into a custom `endpoint` index.
4. **Service Hardening:** Modified the SplunkForwarder service account from `NT SERVICE` to **Local System Account** to resolve permission constraints on Windows security event channels.

## 🔴 Attack Simulation & Telemetry Analysis

### 1. Brute-Force Authentication Test (`Crowbar`)
* **Execution:** Used Kali Linux to launch a credential brute-force attack against the Windows target via RDP (`port 3389`) using `crowbar`.
* **Telemetry Captured:** Generated Windows Security Event Logs (`EventCode=4625` for failed logins and `EventCode=4624` for successful authentications).
* **Splunk Query & Triage:**
  ```spl
  index=endpoint EventCode=4625 OR EventCode=4624 
  | table _time, host, TargetUserName, Source_Network_Address, EventCode 
  | sort - _time
