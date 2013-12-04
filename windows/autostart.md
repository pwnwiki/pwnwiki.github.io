## Windows Autostart Locations
### Folders
| Location | Operating System |
| -------- | ---------------- |
| `%SystemDrive%\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\` | Windows NT 6.0, 6.1 |
| `%SystemDrive%\Documents And Settings\All Users\Start Menu\Programs\StartUp\` | Windows 5.0, 5.1, 5.2 |
| `%SystemDrive%\wmiOWS\Start Menu\Programs\StartUp\` | Windows 9x |
| `%SystemDrive%\WINNT\Profiles\All Users\Start Menu\Programs\StartUp\` | Windows NT 3.50, 3.51, 4.0 |
| `User\Startup\` | |
| `%windir%\Start Menu\Programs\Startup\` | |
| `%windir%\Tasks\` | |
| `%windir%\system\iosubsys\` | |
| `%windir%\system\vmm32\` | |

### Files
| Location | Operating System |
| -------- | ---------------- |
| `%windir%\dosstart.bat` | |
| `%windir%\system.ini` - [boot] "scrnsave.exe" | |
| `%windir%\system.ini` - [boot] "shell" | |
| `%windir%\system\autoexec.nt` | |
| `%windir%\system\config.nt` | |
| `%windir%\win.ini` - [windows] "load" | |
| `%windir%\win.ini` - [windows] "run" | |
| `%windir%\wininit.ini` | |
| `%windir%\winstart.bat` | |
| `c:\autoexec.bat` | |
| `c:\config.sys` | |
| `c:\explorer.exe` | |

### Registry
| Location | Function |
| -------- | -------- |
| `%windir%\dosstart.bat` | |
| `HKEY_CLASSES_ROOT\batfile\shell\open\command\` | Executed whenever a .BAT file (Batch Command) is run. |
| `HKEY_CLASSES_ROOT\comfile\shell\open\command\` | Executed whenever a .COM file (Command) is run. |
| `HKEY_CLASSES_ROOT\exefile\shell\open\command\` | Executed whenever a .EXE file (Executable) is run. |
| `HKEY_CLASSES_ROOT\jsefile\shell\open\command\` | Executed whenever a .JSE file (Encoded Javascript) is run. |
| `HKEY_CLASSES_ROOT\jsfile\shell\open\command\` | Executed whenever a .JS file (Javascript) is run. |
| `HKEY_CLASSES_ROOT\piffile\shell\open\command\` | Executed whenever a .PIF file (Portable Interchange Format) is run. |
| `HKEY_CLASSES_ROOT\scrfile\shell\open\command\` | Executed whenever a .SCR file (Screen Saver) is run. |
| `HKEY_CLASSES_ROOT\vbefile\shell\open\command\` | Executed whenever a .VBE file (Encoded Visual Basic Script) is run. |
| `HKEY_CLASSES_ROOT\vbsfile\shell\open\command\` | Executed whenever a .VBS file (Visual Basic Script) is run. |
| `HKEY_CLASSES_ROOT\wsffile\shell\open\command\` | Executed whenever a .WSF file (Windows Scripting File) is run. |
| `HKEY_CLASSES_ROOT\wshfile\shell\open\command\` | Executed whenever a .WSH file (Windows Scripting Host) is run. |
| `HKEY_CURRENT_USER\Control Panel\Desktop` | The "SCRNSAVE.EXE" value is monitored. This value is launched when your screen saver activates. |
| `HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\load` | Executed when the user logs in. |
| `HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\run` | Executed when the user logs in. |
| `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\run\` | Subvalues are executed when Explorer initialises. |
| `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\Setup\` | Used only by Setup. Displays a progress dialog box as the keys are run one at a time. |
| `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\` | All values in this key are executed, and then their autostart reference is deleted. |
| `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run\` | All values in this key are executed. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Active Setup\Installed Components\` | All subkeys are monitored, with special attention paid to the "StubPath" value in each subkey. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit` | Executed when a user logs in. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon` | The "Shell" value is monitored. This value is executed after you log in. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run\` | All values in this key are executed. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\run\` | Subvalues are executed when Explorer initialises. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce\` | All values in this key are executed, and then their autostart reference is deleted. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce\` | All values in this key are executed as services, and then their autostart reference is deleted. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices\` | All values in this key are executed as services. |
| `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\ShellServiceObjectDelayLoad\` | Executed by explorer.exe as soon as it has loaded. |
| `HKEY_LOCAL_MACHINE\System\Control\WOW\cmdline` | Executed when a 16-bit Windows executable is executed. |
| `HKEY_LOCAL_MACHINE\System\Control\WOW\wowcmdline` | Executed when a 16-bit DOS application is executed. |
| `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager` | The "BootExecute" value is monitored. Files listed here are Native Applications that are executed before Windows starts. |
| `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\` | All subkeys are monitored, with special attention paid to the "StaticVXD" value in each subkey. |
| `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Winsock2\Parameters\Protocol_Catalog\Catalog_En tries\` | Layered Service Providers, executed before user login. |
| `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\` | Services marked to startup automatically are executed before user login. |
| `HKEY_USERS\.Default\Software\Microsoft\Windows\CurrentVersion\RunOnce\` | Similar to the RunOnce key from HKEY_CURRENT_USER. |
| `HKEY_USERS\.Default\Software\Microsoft\Windows\CurrentVersion\Run\` | Similar to the Run key from HKEY_CURRENT_USER. |


## Windows Operating System Versions
From http://msdn.microsoft.com/en-us/library/windows/desktop/ms724832(v=vs.85).aspx:

The following table summarizes the most recent operating system version numbers.

| Operating system | Version number |
| ---------------- | -------------- |
| Windows 8.1 | 6.3 |
| Windows Server 2012 R2 | 6.3 |
| Windows 8 | 6.2 |
| Windows Server 2012 | 6.2 |
| Windows 7 | 6.1 |
| Windows Server 2008 R2 | 6.1 |
| Windows Server 2008 | 6.0 |
| Windows Vista | 6.0 |
| Windows Server 2003 R2 | 5.2 |
| Windows Server 2003 | 5.2 |
| Windows XP 64-Bit Edition | 5.2 |
| Windows XP | 5.1 |
| Windows 2000 | 5.0 |

## References
A large portion of this content came from https://web.archive.org/web/20110203184210/http://www.easy-data.no/Autostart.html
