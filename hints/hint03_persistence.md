# Scenario 3: Registry Persistence via Dropped Script

## ✅Simulated Activity:
Simulated an attacker-like persistence using a script file dropped into a public directory and triggered via Registry Run Key.

---

## Attack Simulation

### Step 1: Connect via RDP
```bash
xfreerdp /u:Administrator /p:'YourPassword' /v:<Win10-IP>
```

### Step 2: Create Script File
```powershell
echo Write-Output "Persistence Triggered Successfully" > C:\Users\Public\doorbell.ps1
```

### Step 3: Simulate the Drop
```powershell
Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name "StartUpBait" -Value "powershell.exe -ExecutionPolicy Bypass -WindowStyle Hidden -File C:\Users\Public\doorbell.ps1"
```
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint03_persistence_simulated_via_rdp.png)

### Step 4: Trigger Persistence
- Logged out / restarted machine
- Upon login, script executed

## Detection
### # Sysmon:
- Event ID 13: Registry value set (Persistence added)
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint03_persistence_sysmon_log_13.png)

### # Autoruns:
- Entry found: StartupBait in Logon tab
- Points to dropped .ps1 script
![](https://github.com/alj-v/cyber-intern-phase-3/blob/main/screenshots/hint03_persistence_autoruns_log.png)

### # Cleanup
To remove persistence:
```powershell
Remove-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name "StartUpBait"
Remove-Item C:\Users\Public\doorbell.ps1
```

### Interview Note  
Q: How do attackers use Registry Run Keys for persistence?  
A: They drop a payload (EXE/PS1) and register it in HKCU:\Software\Microsoft\Windows\CurrentVersion\Run or HKLM equivalent, causing it to run at every user login.  

⚠️Limitations  
- Script executed silently; user may not notice  
- Simulated in single host environment
