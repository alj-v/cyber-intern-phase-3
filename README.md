# Cybersecurity Internship – Phase 3: Advanced Threat Hunting & APT Simulation

## 📌Overview

This phase focuses on simulating Advanced Persistent Threat (APT) techniques and applying threat hunting methodologies to detect, analyze, and respond to sophisticated cyber attacks. It is the final phase of a 3-part internship and showcases advanced knowledge of adversarial emulation, endpoint logging, and incident detection.

---

## ⚔️ Scenarios Covered

|Status|No.|Task|Description|
|------|---|----|-----------|
|✅|1.|**Fileless Malware via PowerShell**|Simulates a spear-phishing attack using in-memory PowerShell payloads.|
||2.|**Lateral Movement via RDP Brute Force**|Emulates attackers using stolen credentials to move across the network.|
||3.|**Persistence via Registry Run Keys**|Establishes stealthy persistence using Windows registry.|
||4.|**DNS Tunneling for Data Exfiltration**|Simulates data exfiltration over DNS requests.|
||5.|**Credential Dumping with Mimikatz**|Demonstrates how attackers extract sensitive credentials from memory.|

---

## Key Learning Areas

- Advanced use of **Sysmon**, **PowerShell Logging**, **Event Correlation**
- Building detection logic with **Wazuh** SIEM
- Threat hunting with **Windows Event IDs** and **Sigma Rule strategies**
- Hands-on simulation of APT techniques
- Documenting forensic evidence for each scenario

---

## Tools & Technologies Used

- **Sysmon + Wazuh** for endpoint detection
- **Kali Linux + PowerShell** for attacker simulation
- **Event Viewer**, **Wireshark**, **Impacket**, **Mimikatz**
- Markdown-based documentation for every scenario
- Preconfigured virtual lab (Kali, Windows 10, Wazuh OVA)

---

## Folder Structure

- `/hints/` – Walkthroughs for each attack simulation
- `/logs/` – Captured logs from Event Viewer or Wazuh
- `/screenshots/` – Visual proof of tasks completed
- `/reports/` – Analysis and final notes
