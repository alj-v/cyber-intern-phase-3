# 📌 Internship Report: Phase 3 - Advanced Threat Hunting & APT Simulation

**Intern:** Aleena Joy  
**Mentor:** Rajendra Bodda

## 🧠 Overview

This phase focused on simulating real-world advanced persistent threat (APT) techniques, detecting them through host and network telemetry, and documenting findings through SIEM and log analysis. The simulations mimicked actual adversary behavior in controlled environments.

---

## 🔐 Platform & Setup

- **SIEM**: Wazuh (agent-based log ingestion)
- **Target OS**: Windows 10
- **Attacker OS**: Kali Linux (tools: Metasploit, Wireshark, Mimikatz, Impacket, etc.)
- **Communication Setup**: RDP, HTTP/HTTPS tunneling via ngrok, DNS tunneling (dnscat2, iodine)

---

## Tools Used:
- Powershell
- Autoruns
- ngrok
- wazuh

---

## Scenario-Based Simulations

### 1️⃣ **Fileless Malware with PowerShell**
- Simulated obfuscated PowerShell payload executed via remote delivery.
- Script block logging enabled to capture **Event ID 4104**.
- Detected Sysmon logs (**Event ID 1 - Process Creation**, **ID 3 - Network Connection**).
- Base64-encoded commands mimicked spear-phishing payload behavior.
- [Simulated](https://github.com/alj-v/cyber-intern-phase-3/blob/main/hints/hint01_fileless_malware_via_powershell.md)✅

### 2️⃣ **Lateral Movement via RDP Brute Force**
- Hydra used to simulate brute-force login attempts on RDP.
- Account lockouts triggered after multiple failed attempts.
- Detected **Event ID 4625 (Logon Failures)** with lockout reasons.
- Discussed lateral movement techniques attackers use post-compromise.
- [Simulated](https://github.com/alj-v/cyber-intern-phase-3/blob/main/hints/hint02_lateral_movement.md)✅

### 3️⃣ **Persistence via Registry Run Keys**
- Malicious process path written to `HKCU:\Software\Microsoft\Windows\CurrentVersion\Run`.
- Persistence verified after login.
- Obfuscated PowerShell + dropped EXE file simulated APT-style persistence methods.
- Detected using **autoruns** and Sysmon logs.
- [Simulated](https://github.com/alj-v/cyber-intern-phase-3/blob/main/hints/hint03_persistence.md)✅

### 4️⃣ **DNS Tunneling - Data Exfiltration**
- Simulated DNS exfiltration using base64-encoded queries.
- Tools used: `dnscat2`, `iodine`, manual `nslookup`, `ping`.
- Wireshark used to capture DNS traffic patterns.
- Observed **Sysmon Event ID 22** for DNS queries (when logged).
- Discussion on how attackers evade detection using DNS.
- [Simulated](https://github.com/alj-v/cyber-intern-phase-3/blob/main/hints/hint04_dns_tunneling.md)✅

### 5️⃣ **Credential Dumping and Exfiltration**
- Used `mimikatz` to dump LSASS credentials.
- Simulated secure exfiltration using HTTPS tunnel via `ngrok`.
- Powershell `Invoke-WebRequest` used to POST creds file.
- Detected exfiltration activity in ngrok logs and Sysmon (where applicable).
- [Simulated](https://github.com/alj-v/cyber-intern-phase-3/blob/main/hints/hint05_credential_dumping_and%20https_exfiltration.md)✅

---

## 📊 Key Observations

- DNS-based exfiltration is hard to detect due to lack of frequent logging (Event ID 22 gaps).
- HTTPS exfiltration blends easily with legitimate traffic; catching it requires deep inspection.
- Attack simulations revealed the importance of **Sysmon**, **PowerShell logging**, and **centralized SIEM visibility**.

---

## 🏁 Status

> ✅ **Phase 3 Successfully Completed**

This phase helped simulate realistic cyberattacks, strengthen detection skills, and apply core incident response techniques in a hands-on environment.

#### Report by: Aleena Joy
