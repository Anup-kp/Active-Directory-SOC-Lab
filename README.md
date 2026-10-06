# Active Directory & Splunk SOC Lab (MyDFIR)

## 📌 Project Objective
To build an on-premise, enterprise-style Windows Active Directory environment (`MyDFIR`) using VirtualBox, integrate it with a centralized Splunk SIEM via Splunk Universal Forwarders and Sysmon, and simulate real-world attacks (Brute Force & Atomic Red Team) to perform log ingestion, threat detection, and alert triaging.

---

## 🏗️ Lab Architecture & Network Topology
The lab is built on a virtualized NAT Network (`192.168.10.0/24`):
* **Splunk SIEM Server:** `192.168.10.10`
* **Windows Server 2022 (Domain Controller):** `192.168.10.7` (Domain: `MyDFIR`)
* **Windows 10 (Target Endpoint):** `192.168.10.100` (Joined to `MyDFIR`)
* **Kali Linux (Attacker Machine):** `192.168.10.250`

---

## 🔍 Threat Simulation & Triage Section

### 1. Brute-Force Authentication Attack (Event ID 4625)
* **Simulation:** Using Kali Linux (`192.168.10.250`), executed credential brute-force attacks against target domain user accounts on the Windows 10 workstation (`192.168.10.100`).
* **Splunk Detection Query (SPL):**
  ```spl
  index=windows EventCode=4625 
  | stats count by TargetUserName, IpAddress 
  | sort - count
  📝 Analyst Remediation Note

    Incident ID: INC-2026-0428

    Finding: Multiple failed authentication attempts detected against domain user accounts from external source IP 192.168.10.250.

    Action Taken: Isolated the affected endpoint via network controls, disabled the compromised user account pending verification, forced a credential reset, and escalated the event to tier-2 incident response.Ah, good catch! Let's clear up that numbering confusion.

When I wrote out the complete `README.md` text earlier, the section headers got a little jumbled in formatting. In a proper Markdown report, everything under the **Threat Simulation & Triage Section** should be numbered sequentially so it flows logically.

Here is the **clean, properly numbered version** of what your entire GitHub `README.md` file should look from top to bottom:

---

```markdown
# Active Directory & Splunk SOC Lab (MyDFIR)

## 📌 Project Objective
To build an on-premise, enterprise-style Windows Active Directory environment (`MyDFIR`) using VirtualBox, integrate it with a centralized Splunk SIEM via Splunk Universal Forwarders and Sysmon, and simulate real-world attacks (Brute Force & Atomic Red Team) to perform log ingestion, threat detection, and alert triaging.

---

## 🏗️ Lab Architecture & Network Topology
The lab is built on a virtualized NAT Network (`192.168.10.0/24`):
* **Splunk SIEM Server:** `192.168.10.10`
* **Windows Server 2022 (Domain Controller):** `192.168.10.7` (Domain: `MyDFIR`)
* **Windows 10 (Target Endpoint):** `192.168.10.100` (Joined to `MyDFIR`)
* **Kali Linux (Attacker Machine):** `192.168.10.250`

---

## 🔍 Threat Simulation & Triage Section

### 1. Brute-Force Authentication Attack (Event ID 4625)
* **Simulation:** Using Kali Linux (`192.168.10.250`), executed credential brute-force attacks against target domain user accounts on the Windows 10 workstation (`192.168.10.100`).
* **Splunk Detection Query (SPL):**
  ```spl
  index=windows EventCode=4625 
  | stats count by TargetUserName, IpAddress 
  | sort - count

```

* **Telemetry Findings:** Splunk successfully surfaced repeated failed logon attempts originating from the attacker IP, detailing exact timestamps and target usernames.

### 2. TTP Simulation via Atomic Red Team

* **Simulation:** Executed specific adversary emulation tests (e.g., account discovery and credential dumping techniques) using Atomic Red Team on the Windows 10 endpoint.
* **Splunk Detection:** Sysmon logs captured suspicious process creation events (`EventCode=1`) and command-line executions, allowing for rapid hunting of malicious process trees.

---

## 📝 Analyst Remediation Note

* **Incident ID:** `INC-2026-0428`
* **Finding:** Multiple failed authentication attempts detected against domain user accounts from external source IP `192.168.10.250`.
* **Action Taken:** Isolated the affected endpoint via network controls, disabled the compromised user account pending verification, forced a credential reset, and escalated the event to tier-2 incident response.
First, let's quickly lock in your **Windows Server 2022 (Active Directory)** network configuration based on your `/24` network scheme and your planned IP (`192.168.10.7`):

* **IP Address:** `192.168.10.7`
* **Subnet Mask:** `255.255.255.0`
* **Default Gateway:** `192.168.10.1`
* **Preferred DNS Server:** `127.0.0.1` (or `192.168.10.7`, since this server will host the DNS role for the `MyDFIR` domain).

---

Here is your complete, step-by-step package for **Steps 3, 4, and 5** to build your powerful GitHub "Proof of Work" repository, video script, and resume update.

## Step 3: Create Your GitHub `README.md`

Create a public repository named `Active-Directory-SOC-Lab` and paste this comprehensive project report directly into your `README.md` file:

```markdown
# Active Directory & Splunk SOC Lab (MyDFIR)

## 📌 Project Objective
To build an on-premise, enterprise-style Windows Active Directory environment (`MyDFIR`) using VirtualBox, integrate it with a centralized Splunk SIEM via Splunk Universal Forwarders and Sysmon, and simulate real-world attacks (Brute Force & Atomic Red Team) to perform log ingestion, threat detection, and alert triaging.

---

## 🏗️ Lab Architecture & Network Topology
The lab is built on a virtualized NAT Network (`192.168.10.0/24`):
* **Splunk SIEM Server:** `192.168.10.10`
* **Windows Server 2022 (Domain Controller):** `192.168.10.7` (Domain: `MyDFIR`)
* **Windows 10 (Target Endpoint):** `192.168.10.100` (Joined to `MyDFIR`)
* **Kali Linux (Attacker Machine):** `192.168.10.250`

---

## 🔍 Threat Simulation & Triage Section

### 1. Brute-Force Authentication Attack (Event ID 4625)
* **Simulation:** Using Kali Linux (`192.168.10.250`), executed credential brute-force attacks against target domain user accounts on the Windows 10 workstation (`192.168.10.100`).
* **Splunk Detection Query (SPL):**
  ```spl
  index=windows EventCode=4625 
  | stats count by TargetUserName, IpAddress 
  | sort - count

```

* **Telemetry Findings:** Splunk successfully surfaced repeated failed logon attempts originating from the attacker IP, detailing exact timestamps and target usernames.

### 2. TTP Simulation via Atomic Red Team

* **Simulation:** Executed specific adversary emulation tests (e.g., account discovery and credential dumping techniques) using Atomic Red Team on the Windows 10 endpoint.
* **Splunk Detection:** Sysmon logs captured suspicious process creation events (`EventCode=1`) and command-line executions, allowing for rapid hunting of malicious process trees.

### 💡 Analyst Remediation Note

> **Incident ID:** INC-2026-0428
> **Finding:** Multiple failed authentication attempts detected against domain user accounts from external source IP `192.168.10.250`.
> **Action Taken:** Isolated the affected endpoint via network controls, disabled the compromised user account pending verification, forced a credential reset, and escalated the event to tier-2 incident response.

```

---

## Step 4: Record a 3-Minute Walkthrough Video Script
Use **OBS Studio** or **Loom** to record your screen and voice. Follow this precise script:

* **0:00 - 0:30 (Introduction):**  
  > *"Hi, I'm Anup. As a career-switcher moving into cybersecurity, I built an end-to-end on-premise SOC lab in VirtualBox to master enterprise telemetry. My environment runs a custom Active Directory domain named `MyDFIR` (`192.168.10.0/24`), complete with a dedicated Domain Controller, a Windows 10 endpoint running Sysmon and a Splunk Forwarder, and a Kali Linux attack machine."*
* **0:30 - 2:00 (The Demonstration):**  
  > *"Here is my Windows Server 2022 Domain Controller and my joined Windows 10 target machine. Next, let's jump into Splunk. I initiated a simulated brute-force attack from my Kali Linux VM (`192.168.10.250`). By writing this custom SPL query targeting Windows Event Code 4625, you can instantly see the spike in failed logons, the source IP address, and the targeted usernames mapped clearly across my dashboard."*
* **2:00 - 3:00 (Adversary Emulation & Triage):**  
  > *"Beyond brute forcing, I also tested adversary workflows using Atomic Red Team to trigger process creation and discovery tactics captured by Sysmon. This lab mirrors the exact triage workflows an entry-level analyst handles daily—detecting anomalies, analyzing telemetry, and writing concise remediation notes."*

---

## Step 5: Update Your Resume & LinkedIn Profile
Add this precise block to the top of your resume's **Projects** section and pin it to your LinkedIn featured section:

> **Active Directory & Splunk Security Monitoring Lab (`MyDFIR`)** | [GitHub Link] | [Video Walkthrough Link]
> * Built an on-premise Windows Server Active Directory domain environment integrated with a centralized Splunk SIEM for real-time security monitoring.
> * Configured Sysmon and Splunk Universal Forwarders on Windows endpoints to ingest security event logs and track system activity.
> * Simulated credential brute-force attacks via Kali Linux and adversary emulation via Atomic Red Team; authored custom SPL queries to detect anomalies and perform threat triage.

---

Would you like to move on to crafting the direct outreach message to send to SOC managers on LinkedIn using this newly created lab project?

```
