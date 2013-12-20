# Windows Commands for Post Exploitation

One liners
-----------
**Tunnel traffic natively with windows**
```bash
netsh int portproxy v4tov4 listenport=80 connecthost=10.0.0.1 connectport=80

**Launch cmd.exe as local system w/ psexec**
psexec -s cmd.exe

**Enable rdp with CLI**
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f

**Launch ARP scan**
for /L %i in (1,1,255) do @start /b ping -n 1 -w 1 192.168.1.%i
