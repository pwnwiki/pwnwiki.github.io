# Windows Blind Files

In some cases during exploitation you as an attacker gain the ability to read arbitrary files. As an attacker you need go-to files that cover as many different OS versions as possible in order to either confirm exploitation or gather intelligence on the exploited system. For this we use a "blind file".

The files below are things to pull when all you can do is to blindly read. Examples of vulnerabilities or situations where this would be helpful might be: local file includes (LFI), directory traversals or remote file share instances like SMB, FTP, NFS or otherwise. Files that will have the same name across networks, Windows domains, and systems are noted below. 

| File     | Description / Importance |
| -------- | ------------------------ |
| `%SYSTEMDRIVE%\boot.ini` | A file that can be counted on to be on virtually every windows host. Helps with confirmation that a read is happening. **WARNING - in more recent versions of Windows this file in no longer there.** |
| `%WINDIR%\win.ini` | This is another file that can be counted on to be readable by all users of a system. |
| `%SYSTEMROOT%\repair\SAM`<br>`%SYSTEMROOT%\System32\config\RegBack\SAM` | Stores user passwords in either an [LM hash](https://en.wikipedia.org/wiki/LM_hash) and/or an [NTLM hash](https://en.wikipedia.org/wiki/NTLM) format. The SAM file in \repair is locked, but can be retrieved using forensic or [Volume Shadow copy methods](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html). |
| `%SYSTEMROOT%\repair\system`<br>`%SYSTEMROOT%\System32\config\RegBack\system` | This is the SYSTEM registry hive. This file is needed to extract the user account password hashes from a Windows system. The SYSTEM file in \repair is locked, but can be retrieved using forensic or [Volume Shadow copy methods](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html). |
| `%SYSTEMROOT%\repair\SAM` <br> `%SYSTEMROOT%\System32\config\RegBack\SAM` | These files store the LM and NTLM hashes for local users.  Using [Volume Shadow Copy](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html) or [Ninja Copy](http://clymb3r.wordpress.com/2013/06/13/using-powershell-to-copy-ntds-dit-registry-hives-bypass-sacls-dacls-file-locks/) you can retrieve these files. |
| `%WINDIR%\repair\sam`<br>`%WINDIR%\repair\system`<br>`%WINDIR%\repair\software`<br>`%WINDIR%\repair\security` | System registry hives. https://en.wikipedia.org/wiki/Windows_Registry |
| `%SYSTEMROOT%\repair\SAM`<br>`%SYSTEMROOT%\System32\config\SAM`<br>`%SYSTEMROOT%\System32\config\RegBack\SAM` | Stores user passwords in either an [LM hash](https://en.wikipedia.org/wiki/LM_hash) and/or an [NTLM hash](https://en.wikipedia.org/wiki/NTLM) format. The SAM file in \repair is locked, but can be retrieved using forensic or [Volume Shadow copy methods](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html). |
| `%SYSTEMROOT%\repair\SYSTEM`<br>`%SYSTEMROOT%\System32\config\SYSTEM`<br>`%SYSTEMROOT%\System32\config\RegBack\SYSTEM` | This is the SYSTEM registry hive. This file is needed to extract the user account password hashes from a Windows system. The SYSTEM file in \repair is locked, but can be retrieved using forensic or [Volume Shadow copy methods](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html). |
| `%SYSTEMDRIVE%\autoexec.bat` | autoexec.bat is a startup script that executes at startup. As [Webopedia states](http://www.webopedia.com/TERM/A/autoexec_bat.html), “Stands for automatically executed batch file, the file that DOS automatically executes when a computer boots up. This is a convenient place to put commands you always want to execute at the beginning of a computing session. For example, you can set system parameters such as the date and time, and install memory-resident programs.” |
| `%SYSTEMDRIVE%\pagefile.sys` | This file is used by the operating system when there is not enough RAM (memory) in the system. It is a large file, but contains spill over from RAM, usually lots of good information can be pulled, but should be a last resort due to size. |
| `%SystemDrive%\inetpub\logs\LogFiles` | IIS 7.x web server log file location. |
| `%USERPROFILE%\LocalS~1\Tempor~1\Content.IE5\index.dat` | Internet Explorer web browser history file (http://support.microsoft.com/kb/322916) |
| `%USERPROFILE%\ntuser.dat` | User-level Windows registry settings (http://technet.microsoft.com/en-us/library/cc758618(v=WS.10).aspx) |
| `%WINDIR%\System32\drivers\etc\hosts` | System hosts file for local translation of host names to IP addresses. |
| `%WINDIR%\debug\NetSetup.log` | Shows issues when computers are joined to a domain. http://technet.microsoft.com/en-us/library/cc961817.aspx |
| `%WINDIR%\iis[version].log` where [version] = 6, 7, or 8 | Internet Information Service (IIS web server) log files. |
| `%WINDIR%\system32\CCM\logs\*.log` | Windows SCCM (System Center Configuration Manager) log files (http://technet.microsoft.com/en-us/library/bb892800.aspx) |
| `%WINDIR%\system32\config\AppEvent.Evt`<br>`%WINDIR%\system32\config\SecEvent.Evt` | Windows Event Logs. |
| `%WINDIR%\system32\config\default.sav`<br>`%WINDIR%\system32\config\security.sav`<br>`%WINDIR%\system32\config\software.sav`<br>`%WINDIR%\system32\config\system.sav` | Backup Windows registry files (http://forensics.wikia.com/wiki/Windows_registry_entries) |
| `%WINDIR%\system32\logfiles\httperr\httperr1.log` | IIS 6.x web server error logs. |
| `%WINDIR%\system32\logfiles\w3svc1\exYYMMDD.log` where YYMMDD = year month day | Web server log files. |
| `unattend.txt, unattend.xml, unattended.xml, sysprep.inf` | Used in the automated deployment of Windows images and can contain user accounts. Sometimes found in the `%WINDIR%\Panther\` directory. |
