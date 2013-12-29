
# Windows Blind Files

In some cases during exploitation you as an attacker gain the ability to read arbitrary files. As an attacker you need go-to files that cover as many different OS versions as possible in order to either confirm exploitation or gather intelligence on the exploited system. For this we use a "blind file".

The files below are things to pull when all you can do is to blindly read. Examples of vulnerabilities or situations where this would be helpful might be: local file includes (LFI), directory traversals or remote file share instances like SMB, FTP, NFS or otherwise. Files that will have the same name across networks, Windows domains, and systems are noted below. 

| File     | Description / Importance |
| -------- | ------------------------ |
| `%SYSTEMDRIVE%\boot.ini` | A file that can be counted on to be on virtually every windows host. Helps with confirmation that a read is happening. **WARNING - in more recent versions of Windows this file in no longer there.** |
| `%WINDIR%\win.ini` | This is another file that can be counted on to be readable by all users of a system. |
| `%SYSTEMROOT%\repair\SAM`<br>`%SYSTEMROOT%\System32\config\RegBack\SAM` | Stores user passwords in either an [LM hash](https://en.wikipedia.org/wiki/LM_hash) and/or an [NTLM hash](https://en.wikipedia.org/wiki/NTLM) format. The SAM file in \repair is locked, but can be retrieved using forensic or [Volume Shadow copy methods](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html). |
| `%SYSTEMROOT%\repair\system`<br>`%SYSTEMROOT%\System32\config\RegBack\system` | This is the SYSTEM registry hive. This file is needed to extract the user account password hashes from a Windows system. The SYSTEM file in \repair is locked, but can be retrieved using forensic or [Volume Shadow copy methods](http://www.room362.com/blog/2013/6/10/volume-shadow-copy-ntdsdit-domain-hashes-remotely-part1.html). |
| `%SYSTEMDRIVE%\autoexec.bat` | autoexec.bat is a startup script that executes at startup. As [Webopedia states](http://www.webopedia.com/TERM/A/autoexec_bat.html), “Stands for automatically executed batch file, the file that DOS automatically executes when a computer boots up. This is a convenient place to put commands you always want to execute at the beginning of a computing session. For example, you can set system parameters such as the date and time, and install memory-resident programs.” |
