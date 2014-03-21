# Windows Commands for Post Exploitation

One liners
-----------
**Launch cmd.exe as local system w/ psexec**
```bash
psexec -s cmd.exe
```

**Enable rdp with CLI**
```bash
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

**Launch ARP scan**
```bash
for /L %i in (1,1,255) do @start /b ping -n 1 -w 1 192.168.1.%i
```