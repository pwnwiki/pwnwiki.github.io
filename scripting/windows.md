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

**Capture all IPv4 traffic, TCP only, which matches the IP address on a 64 bit Windows 7/Windows 2008 
or newer box, continue the capture even if the computer restarts, save capture to a nondefault location. 
Captures can then be analysed with Microsoft's Message Analyser
http://www.microsoft.com/en-us/download/details.aspx?id=44226**
```bash
netsh trace start capture=yes Ethernet.Type=IPv4  IPv4.Address=157.59.136.1 Protocol=TCP persistent=yes traceFile=C:\Users\Public\trace.etl
```
**Stop the capture**
```bash
netsh trace stop
```