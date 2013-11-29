# Windows Important Files

Files that can yield passwords or other intel about the system, network or users.

| File     | Description / Importance |
| -------- | ------------------------ |
| `%SYSTEMDRIVE%\pagefile.sys` | This file is used by the operating system when there is not enough RAM (memory) in the system. It is a large file, but contains spill over from RAM, usually lots of good information can be pulled, but should be a last resort due to size. |
| `%SYSTEMROOT%\repair\SAM` <br> `%SYSTEMROOT%\System32\config\RegBack\SAM` | These files store the LM and NTLM hashes for local users.  Using [Volume Shadow Copy](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html) or [Ninja Copy](http://clymb3r.wordpress.com/2013/06/13/using-powershell-to-copy-ntds-dit-registry-hives-bypass-sacls-dacls-file-locks/) you can retrieve these files. |
| `%SystemDrive%\inetpub\logs\LogFiles` | IIS 7.x web server log file location. |
| `%USERPROFILE%\LocalS~1\Tempor~1\Content.IE5\index.dat` | Internet Explorer web browser history file (http://support.microsoft.com/kb/322916) |
| `%USERPROFILE%\ntuser.dat` | User-level Windows registry settings (http://technet.microsoft.com/en-us/library/cc758618(v=WS.10).aspx) |
| `%WINDIR%\System32\drivers\etc\hosts` | System hosts file for local translation of host names to IP addresses. |
| `%WINDIR%\debug\NetSetup.log` | Shows issues when computers are joined to a domain. http://technet.microsoft.com/en-us/library/cc961817.aspx |
| `%WINDIR%\iis[version].log` where [version] = 6, 7, or 8 | Internet Information Service (IIS web server) log files. |
| `%WINDIR%\repair\sam`<br>`%WINDIR%\repair\system`<br>`%WINDIR%\repair\software`<br>`%WINDIR%\repair\security` | System registry hives. https://en.wikipedia.org/wiki/Windows_Registry |
| `%WINDIR%\system32\CCM\logs\*.log` | Windows SCCM (System Center Configuration Manager) log files (http://technet.microsoft.com/en-us/library/bb892800.aspx) |
| `%WINDIR%\system32\config\AppEvent.Evt`<br>`%WINDIR%\system32\config\SecEvent.Evt` | Windows Event Logs. |
| `%WINDIR%\system32\config\default.sav`<br>`%WINDIR%\system32\config\security.sav`<br>`%WINDIR%\system32\config\software.sav`<br>`%WINDIR%\system32\config\system.sav` | Backup Windows registry files (http://forensics.wikia.com/wiki/Windows_registry_entries) |
| `%WINDIR%\system32\logfiles\httperr\httperr1.log` | IIS 6.x web server error logs. |
| `%WINDIR%\system32\logfiles\w3svc1\exYYMMDD.log` where YYMMDD = year month day | Web server log files. |
| `unattend.txt, unattend.xml, sysprep.inf` | Used in the automated deployment of Windows images and can contain user accounts. |