# 🏆 Complete Internship Report: Phases 1–3
## Cybersecurity SIEM Internship with Srida IT Consulting and Services Pvt Ltd.
Intern: Aleena Joy  
Mentor: Rajendra Bodda

## 📌 Program Objective

This three-phase internship was designed to build strong cybersecurity fundamentals (Phase 1), develop intermediate red‑team skills (Phase 2), and culminate in advanced adversary simulation and threat‑hunting (Phase 3) — replicating APT behaviors and detection strategies using enterprise-grade telemetry.

---

## 🧭 Phase 1: Foundations in Cybersecurity & Red‑Teaming

- **Skills Developed**: Reconnaissance, vulnerability scanning, exploit execution, basic PowerShell scripting, web attacks.
- **Tools Used**: Nmap, Metasploit, Burp Suite, Nikto, Hydra, PowerShell.
- **Key Activities**:
  - Port & service enumeration on target VMs.
  - Exploitation of known vulnerabilities (e.g. EternalBlue).
  - Gaining meterpreter access and conducting post‑exploitation tasks (hash dumps, persistence).
- **Evidence Collected**: Screenshots, terminal logs, PowerShell scripts.
- **Outcome**: Established a solid red‑teaming foundation with hands-on attack workflows.

---

## 🔍 Phase 2: Intermediate Red‑Team & Defensive Counterparts

- **Skills Expanded**: Lateral movement, shell pivoting, Kerberos attacks, Windows defense bypass.
- **Tools Used**: Hydra, Metasploit, Impacket (wmiexec, smbexec), Rubeus.
- **Scenario Highlights**:
  - Simulated RDP brute‑force attacks with account lockout controls.
  - Executed pass‑the‑hash and Kerberoasting attacks.
  - Simulated C2 pivoting between Windows hosts.
  - Documented detections via Windows Security Logs and basic SIEM alerts.
- **Evidence Collected**: Attack flow scripts, Windows logs, SIEM alert screenshots.
- **Outcome**: Understood the dynamics of lateral movement and defense/log correlation in small networks.

---

## 🛡️ Phase 3: Advanced Threat Hunting & APT Simulation

**Objective**: Simulate real-world APT tactics—fileless malware, RDP brute‑force, registry persistence, DNS exfil, credential dumping/exfiltration—and hunt them using Sysmon, Wazuh, and network monitoring.

### 🧠 Scenario 1: Fileless Malware via PowerShell
- Obfuscated PowerShell payload execution.
- Captured with **Sysmon Event IDs 1, 3**, PowerShell script‑block logging (ID 4104).

### 🧠 Scenario 2: RDP Brute‑Force / Lateral Movement
- Used Hydra to simulate brute‑force RDP attacks.
- Generated account lockouts and captured **Event ID 4625** in Security logs.

### 🧠 Scenario 3: Registry‑Based Persistence
- Persisted a dropped script via Run key in `HKCU`.
- Verified with **Sysmon Event ID 13** and Autoruns.

### 🧠 Scenario 4: DNS Tunneling (Data Exfiltration)
- Base64‑encoded DNS query simulation using `dnscat2`, `nslookup`, `ping`.
- Captured DNS traffic in Wireshark.
- Demonstrated detection limitations & telemetry gaps in Windows logs (Event ID 22).

### 🧠 Scenario 5: Credential Dumping & HTTPS Exfiltration
- Dumped credentials using `mimikatz`.
- Exfiltrated via HTTPS POST to ngrok public tunnel.
- Monitored via Sysmon, PowerShell logs, ngrok logs, and Wireshark.

---

## 🧾 Key Learnings & Outcomes

- **Detection Essentials**:
  - Monitoring Sysmon Event IDs 1/3/10/13/22/4104/4625 is critical.
  - Wazuh SIEM proves effective for alerting and correlation—though gaps exist (e.g. DNS behavior).
- **Advanced Threat Tactics**:
  - Fileless malware, brute‑force account lockouts, registry persistence, DNS tunnels, encrypted HTTPS exfiltration—mirrors real-world APT activity.
  - Threats evade standard logs; deep telemetry + network capture required.
- **Threat‑Hunting Strategy**:
  - Use Sigma rules for SIEM alerting.
  - Employ network tools like Wireshark and DNS parsing tools (Zeek/Suricata).
  - Maintain visibility on process creation, network connections, registry changes, DNS queries.
- **Portfolio‑Ready Skills**:
  - Complete documentation of attack simulations.
  - Evidence-backed analysis and detection exfiltration write‑ups.
  - Practice responding to interview questions about APT tradecraft and detection.

---

## Evidence & Repository

All scripts, logs, screenshots, and markdown documentation for each phase are stored in my GitHub repository:  
[Phase-1](https://github.com/alj-v/cyber-intern-phase-1/)  
[Phase-2](https://github.com/alj-v/cyber-intern-phase-2/)  
[Phase-3](https://github.com/alj-v/cyber-intern-phase-3/)

---

## ✅ Completion Status

> **All three phases completed successfully**  
> I hereby confirm completion of Phase 1, Phase 2, and Phase 3 and request issuance of the internship certificate reflecting full participation.
