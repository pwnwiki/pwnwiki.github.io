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

# Windows CMD Config Commands

Commands that display information about the configuration of the victim and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

## Misc
### c:\windows\system32\gathernetworkinfo.vbs
 * **Command**: `c:\windows\system32\gathernetworkinfo.vbs`
 * **Command with arguments**: NA
 * **Description**: **Windows 7 Only** Script included gathers data about the system and stores output in files in the `c:\windows\system32\config` directory. External link [here.](http://www.verboon.info/index.php/2011/06/the-gathernetworkinfo-vbs-script/)
 * **Output**:
   * NA   
   
### echo
 * **Command**: `echo`
 * **Command with arguments**: `echo %COMSPEC%%`
 * **Description**: Determine the location of the command line interpreter such as cmd.exe.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>echo %COMSPEC%<br>C:\Windows\system32\cmd.exe</code></div>
    
### fsutil
 * **Command**: `set`
 * **Command with arguments**: `fsutil fsinfo drives`
 * **Description**: **Must be ADMIN to run this.** Lists the current drives on the system.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Windows\system32>fsutil fsinfo drives<br><br>Drives: A:\ C:\ D:\</code></div>   
    
### gpresult
 * **Command**: `gpresult`
 * **Command with arguments**: `gpresult /z`
 * **Description**: Extremely verbose output of GPO (Group policy) settings as applied to the current system and user.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>gpresult /z<br><br>Microsoft (R) Windows (R) Operating System Group Policy Result tool v2.0<br>Copyright (C) Microsoft Corp. 1981-2001<br><br>Created On 10/15/2013 at 7:02:05 PM<br><br><br>RSOP data for LAB\johndoe on WIN-0P19ULL2NB6 : Logging Mode<br>------------------------------------------------------------<br><br>OS Configuration:            Primary Domain Controller<br>OS Version:                  6.0.6002<br>Site Name:                   N/A<br>Roaming Profile:             N/A<br>Local Profile:               C:\Users\johndoe<br>Connected over a slow link?: No<br><br><br>USER SETTINGS<br>--------------<br>    CN=johndoe,CN=Users,DC=lab,DC=sky,DC=net<br>    Last time Group Policy was applied: 10/12/2013 at 6:20:23 PM<br>    Group Policy was applied from:      WIN-0P19ULL2NB6.lab.sky.net<br>    Group Policy slow link threshold:   500 kbps<br>    Domain Name:                        LAB<br>    Domain Type:                        Windows 2000<br><br>    Applied Group Policy Objects<br>    -----------------------------<br>        N/A<br><br>    The following GPOs were not applied because they were filtered out<br>    -------------------------------------------------------------------<br>        Local Group Policy<br>            Filtering:  Not Applied (Empty)<br><br>        Default Domain Policy<br>            Filtering:  Not Applied (Empty)<br><br>    The user is a part of the following security groups<br>    ---------------------------------------------------<br>        Domain Users<br>        Everyone<br>        BUILTIN\Users<br>        BUILTIN\Administrators<br>        BUILTIN\Pre-Windows 2000 Compatible Access<br>        NT AUTHORITY\INTERACTIVE<br>        NT AUTHORITY\Authenticated Users<br>        This Organization<br>        LOCAL<br>        High Mandatory Level<br><br>    The user has the following security privileges<br>    ----------------------------------------------<br><br><br>    Resultant Set Of Policies for User<br>    -----------------------------------</code></div>
   
### set
 * **Command**: `set`
 * **Command with arguments**: NA
 * **Description**: Shows all current environmental variables. Specific ones to look for are USERDOMAIN, USERNAME, USERPROFILE, HOMEPATH, LOGONSERVER, COMPUTERNAME, APPDATA, and ALLUSERPROFILE.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>set<br>ALLUSERSPROFILE=C:\ProgramData<br>APPDATA=C:\Users\johndoe\AppData\Roaming<br>CommonProgramFiles=C:\Program Files\Common Files<br>COMPUTERNAME=WIN-0P19ULL2NB6<br>ComSpec=C:\Windows\system32\cmd.exe<br>DFSTRACINGON=FALSE<br>FP_NO_HOST_CHECK=NO<br>HOMEDRIVE=C:<br>HOMEPATH=\Users\johndoe<br>LOCALAPPDATA=C:\Users\johndoe\AppData\Local<br>LOGONSERVER=\\WIN-0P19ULL2NB6<br>OS=Windows_NT<br>Path=C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem<br>PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC<br>PROCESSOR_ARCHITECTURE=x86<br>PROCESSOR_IDENTIFIER=x86 Family 6 Model 42 Stepping 7, GenuineIntel<br>PROCESSOR_LEVEL=6<br>PROCESSOR_REVISION=2a07<br>ProgramData=C:\ProgramData<br>ProgramFiles=C:\Program Files<br>PROMPT=$P$G<br>PUBLIC=C:\Users\Public<br>SESSIONNAME=Console<br>SystemDrive=C:<br>SystemRoot=C:\Windows<br>TEMP=C:\Users\johndoe\AppData\Local\Temp\1<br>TMP=C:\Users\johndoe\AppData\Local\Temp\1<br>TRACE_FORMAT_SEARCH_PATH=\\winseqfe\release\Windows6.0\lh_sp2rtm\6002.18005.090410-1830\x86fre\symbols.pri\TraceFormat<br>USERDNSDOMAIN=LAB.SKY.NET<br>USERDOMAIN=LAB<br>USERNAME=johndoe<br>USERPROFILE=C:\Users\johndoe<br>windir=C:\Windows</code></div>
 
### whoami
 * **Command**: `whoami`
 * **Command with arguments**: `whoami /all`
 * **Description**: Lists information about the user you are currently logged in as. Helpful for showing what groups, sid and privileges of this user. Not available in all versions of Windows but is in Windows Vista and more recent. According to [Wikipedia](http://en.wikipedia.org/wiki/Whoami), this command can be added to Windows 2000 using the resource kit and is installed in Windows XP SP2 Support Tools.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>whoami<br>lab\johndoe<br><br>C:\Users\johndoe>whoami/all<br><br>USER INFORMATION<br>----------------<br><br>User Name   SID<br>=========== ===========================================<br>lab\johndoe S-1-5-21-60789211-843652525-1994898995-1001<br><br><br>GROUP INFORMATION<br>-----------------<br><br>Group Name                                 Type             SID          Attributes<br>========================================== ================ ============ ==================================================<br>Everyone                                   Well-known group S-1-1-0      Mandatory group, Enabled by default, Enabled group<br>BUILTIN\Users                              Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group<br>BUILTIN\Administrators                     Alias            S-1-5-32-544 Group used for deny only<br>BUILTIN\Pre-Windows 2000 Compatible Access Alias            S-1-5-32-554 Group used for deny only<br>NT AUTHORITY\INTERACTIVE                   Well-known group S-1-5-4      Mandatory group, Enabled by default, Enabled group<br>NT AUTHORITY\Authenticated Users           Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group<br>NT AUTHORITY\This Organization             Well-known group S-1-5-15     Mandatory group, Enabled by default, Enabled group<br>LOCAL                                      Well-known group S-1-2-0      Mandatory group, Enabled by default, Enabled group<br>Mandatory Label\Medium Mandatory Level     Unknown SID type S-1-16-8192  Mandatory group, Enabled by default, Enabled group<br><br><br>PRIVILEGES INFORMATION<br>----------------------<br><br>Privilege Name                Description                          State<br>============================= ==================================== ========<br>SeShutdownPrivilege           Shut down the system                 Disabled<br>SeChangeNotifyPrivilege       Bypass traverse checking             Enabled<br>SeUndockPrivilege             Remove computer from docking station Disabled<br>SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled<br>SeTimeZonePrivilege           Change the time zone                 Disabled</code></div>
     
### systeminfo
 * **Command**: `systeminfo`
 * **Command with arguments**: NA
 * **Description**:In computing, systeminfo.exe, a command-line utility shipped with Microsoft Windows versions from Windows XP onwards, produces summary output of Windows hardware/software operating-environment parameters.
 * **Output**:
   *<div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Windows\system32>systeminfo<br><br>Host Name:                 ADMIN-PC<br>OS Name:                   Microsoft Windows 2008<br>OS Version:                6.1.7601 Service Pack 1 Build 7601<br>OS Manufacturer:           Microsoft Corporation<br>OS Configuration:          Standalone Workstation<br>OS Build Type:             Multiprocessor Free<br>Registered Owner:          johndoe<br>Registered Organization: <br>Product ID:                00426-OEM-8992662-00400<br>System Type:               x64-based PC<br>Processor(s):              1 Processor(s) Installed.<br>...</code></div>

### type
 * **Command**: `type`
 * **Command with arguments**: `type %WINDIR%\System32\drivers\etc\hosts`
 * **Description**: Show the contents of a file. In this case, you can get the system's host file which does the local translation of IP address to hostname. This file may contain important servers.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>type %WINDIR%\System32\drivers\etc\hosts<br># Copyright (c) 1993-2006 Microsoft Corp.<br>#<br># This is a sample HOSTS file used by Microsoft TCP/IP for Windows.<br>#<br># This file contains the mappings of IP addresses to host names. Each<br># entry should be kept on an individual line. The IP address should<br># be placed in the first column followed by the corresponding host name.<br># The IP address and the host name should be separated by at least one<br># space.<br>#<br># Additionally, comments (such as these) may be inserted on individual<br># lines or following the machine name denoted by a '#' symbol.<br>#<br># For example:<br>#<br>#      102.54.94.97     rhino.acme.com          # source server<br>#       38.25.63.10     x.acme.com              # x client host<br><br>127.0.0.1       localhost<br>::1             localhost</code></div>  
---- 

## Registry (reg)
For more information: http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/reg.mspx?mfr=true or http://www.petri.co.il/reg_command_in_windows_xp.htm
 
### Add
 * **Command with arguments**: `reg add [\\TargetIPaddr\] [RegDomain\Key]`
 * **Description**: Adds a key to target machine's registry. Replace [\\TargetIPaddr] with your target system, [RegDomain\Key] with the registry domain and key you'd like to insert.
 * **Output**:
   * NA  

### Export
 * **Command with arguments**: `reg export [RegDomain\Key] [OUTFILE]`
 * **Description**: Exports a key to a file. Replace [RegDomain\Key] with the registry domain and key you'd like to insert and [OUTFILE] with the name of the file you would like to save the registry key in.
 * **Output**:
   * NA     
 
### Import
 * **Command with arguments**: `reg import [INFILE]`
 * **Description**: Imports content to target machine's registry. Replace [INFILE] with the file that has the content you wish to insert.
 * **Output**:
   * NA    
   
### Query (Local)
 * **Command with arguments**: `reg query HKLM /s /d /f "C:\* *.exe" | find /I "C:\" | find /V """"`
 * **Description**: Securely registered executables within the system registry.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>reg query HKLM /s /d /f "C:\* *.exe" &#124; find /I "C:\" &#124; find /V """"<br>    (Default)    REG_SZ    C:\Program Files\VMware\VMware Tools\TPVCGateway.exe<br>    (Default)    REG_SZ    C:\Program Files\VMware\VMware Tools\VMwareCplLauncher.exe<br>    (Default)    REG_SZ    C:\Program Files\Internet Explorer\iexplore.exe<br>    LocalizedString    REG_SZ    @C:\Program Files\VMware\VMware Tools\VMwareHostOpen.exe,-1008<br>    (Default)    REG_SZ    C:\Program Files\VMware\VMware Tools\VMwareHostOpen.exe,-101<br>    (Default)    REG_SZ    C:\Program Files\Internet Explorer\IEXPLORE.EXE<br>    (Default)    REG_SZ    C:\Program Files\VMware\VMware Tools\VMwareTray.exe<br>    627BF46A150AF194A92056AAE2EFA363    REG_SZ    C:\Program Files\VMware\VMware Tools\rpctool.exe<br>    627BF46A150AF194A92056AAE2EFA363    REG_SZ    C:\Program Files\VMware\VMware Tools\VMwareCplLauncher.exe<br>    627BF46A150AF194A92056AAE2EFA363    REG_SZ    C:\Program Files\VMware\VMware Tools\VMwareToolboxCmd.exe<br>    627BF46A150AF194A92056AAE2EFA363    REG_SZ    C:\Program Files\VMware\VMware Tools\unzip.exe<br>    627BF46A150AF194A92056AAE2EFA363    REG_SZ    C:\Program Files\VMware\VMware Tools\vmtoolsd.exe<br>    627BF46A150AF194A92056AAE2EFA363    REG_SZ    C:\Program Files\Common Files\VMware\Drivers\vss\comreg.exe</code></div>  
   
### Query (Remote)
 * **Command with arguments**: `reg query [\\TargetIPaddr\] [RegDomain\Key] /v [ValueName]`
 * **Description**: Retrieves a key and value from target machine's registry. Replace [\\TargetIPaddr] with your target system, [RegDomain\Key] with the registry domain and key you'd like to query.
 * **Output**:
   * NA  
   
### Save
 * **Command with arguments**: `reg save [HIVE] [OUTFILE]`
 * **Description**: **Must be run as an administrator.** Saves part of the registry to a file. Replace [HIVE] with HKLM\Security, HKLM\System, or HKLM\SAM and [OUTFILE] with the name of the file you would like to save the registry in.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>c:\temp>reg save HKLM\Security security.hive && dir<br>The operation completed successfully.<br> Volume in drive C has no label.<br> Volume Serial Number is 1A09-5F16<br> Directory of c:\temp<br>10/26/2013  11:17 PM    <DIR>          .<br>10/26/2013  11:17 PM    <DIR>          ..<br>10/26/2013  11:17 PM            32,768 security.hive<br>               1 File(s)         32,768 bytes<br>               2 Dir(s)  33,312,219,136 bytes free</code></div>
----

## sc
sc.exe retrieves and sets control information about services. You can use sc.exe for testing and debugging service programs. For more information: http://technet.microsoft.com/en-us/library/bb490995.aspx. 
<div class="slide" style="cursor: pointer;">Help details can be found if you expand this section here: Show/Hide</div><div class="view"><code>C:\Users\tester>sc
DESCRIPTION:
        SC is a command line program used for communicating with the
        Service Control Manager and services.
USAGE:
        sc <server> [command] [service name] <option1> <option2>...

        The option <server> has the form "\\ServerName"
        Further help on commands can be obtained by typing: "sc [command]"
        Commands:
          query-----------Queries the status for a service, or
                          enumerates the status for types of services.
          queryex---------Queries the extended status for a service, or
                          enumerates the status for types of services.
          start-----------Starts a service.
          pause-----------Sends a PAUSE control request to a service.
          interrogate-----Sends an INTERROGATE control request to a service.
          continue--------Sends a CONTINUE control request to a service.
          stop------------Sends a STOP request to a service.
          config----------Changes the configuration of a service (persistent).
          description-----Changes the description of a service.
          failure---------Changes the actions taken by a service upon failure.
          failureflag-----Changes the failure actions flag of a service.
          sidtype---------Changes the service SID type of a service.
          privs-----------Changes the required privileges of a service.
          qc--------------Queries the configuration information for a service.
          qdescription----Queries the description for a service.
          qfailure--------Queries the actions taken by a service upon failure.
          qfailureflag----Queries the failure actions flag of a service.
          qsidtype--------Queries the service SID type of a service.
          qprivs----------Queries the required privileges of a service.
          qtriggerinfo----Queries the trigger parameters of a service.
          qpreferrednode--Queries the preferred NUMA node of a service.
          delete----------Deletes a service (from the registry).
          create----------Creates a service. (adds it to the registry).
          control---------Sends a control to a service.
          sdshow----------Displays a service's security descriptor.
          sdset-----------Sets a service's security descriptor.
          showsid---------Displays the service SID string corresponding to an arbitrary name.
          triggerinfo-----Configures the trigger parameters of a service.
          preferrednode---Sets the preferred NUMA node of a service.
          GetDisplayName--Gets the DisplayName for a service.
          GetKeyName------Gets the ServiceKeyName for a service.
          EnumDepend------Enumerates Service Dependencies.

        The following commands don't require a service name:
        sc <server> <command> <option>
          boot------------(ok | bad) Indicates whether the last boot should
                          be saved as the last-known-good boot configuration
          Lock------------Locks the Service Database
          QueryLock-------Queries the LockStatus for the SCManager Database
EXAMPLE:
        sc start MyService</code></div>

### Query Configuration
 * **Command with arguments**: `sc qc [servicename]`
 * **Description**: Queries the configuration information for a service. Things to look at here are the path to the executable, the start type (does it start at boot or on demand?), and service names.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code> c:\Users\johndoe>sc qc browser
[SC] QueryServiceConfig SUCCESS<br>SERVICE_NAME: browser<br>        TYPE               : 20  WIN32_SHARE_PROCESS<br>        START_TYPE         : 4   DISABLED<br>        ERROR_CONTROL      : 1   NORMAL<br>        BINARY_PATH_NAME   : C:\Windows\System32\svchost.exe -k netsvcs<br>        LOAD_ORDER_GROUP   : NetworkProvider<br>        TAG                : 0<br>        DISPLAY_NAME       : Computer Browser<br>        DEPENDENCIES       : LanmanWorkstation<br>                           : LanmanServer<br>
        SERVICE_START_NAME : LocalSystem</code></div>
   
### Query Status
 * **Command with arguments**: `sc query [servicename]`
 * **Description**: Queries the status for a service, or enumerates the status for types of services.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>sc query browser<br><br>SERVICE_NAME: browser<br>        TYPE               : 20  WIN32_SHARE_PROCESS<br>        STATE              : 1  STOPPED<br>        WIN32_EXIT_CODE    : 1077  (0x435)<br>        SERVICE_EXIT_CODE  : 0  (0x0)<br>        CHECKPOINT         : 0x0<br>        WAIT_HINT          : 0x0</code></div>		
   
### Query Status Extended
 * **Command with arguments**: `sc queryex [servicename]`
 * **Description**: Queries the status for a service, or enumerates the status for types of services.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>sc queryex browser<br>
SERVICE_NAME: browser<br>        TYPE               : 20  WIN32_SHARE_PROCESS<br>        STATE              : 1  STOPPED<br>        WIN32_EXIT_CODE    : 1077  (0x435)<br>        SERVICE_EXIT_CODE  : 0  (0x0)<br>        CHECKPOINT         : 0x0<br>        WAIT_HINT          : 0x0<br>        PID                : 0<br>        FLAGS              :</code></div>
----		

## wmi
According to Microsoft (http://msdn.microsoft.com/en-us/library/aa394531(v=vs.85).aspx), "the WMI command-line (WMIC) utility provides a command-line interface for WMI. WMIC is compatible with existing shells and utility commands." Additional information can also be found here https://isc.sans.edu/diary/Windows+Command-Line+Kung+Fu+with+WMIC/1229.

For some of these `wmic` commands that pull information (versus perform an action) you can add `list full` to the end and retrieve the data in a non-table format. Sometimes this view is easier to read. Using `list brief` shows less data. The examples below show several output formats.
 
### BIOS Information
 * **Command with arguments**: `wmic bios [list full]`
 * **Description**: Retrieves BIOS information including system serial number.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic bios list full<br><br><br>BiosCharacteristics={4,7,8,9,10,11,12,14,15,16,19,26,27,28,29,30,32,39,40,41,42,50,57,58}<br>BuildNumber=<br>CodeSet=<br>CurrentLanguage=<br>Description=PhoenixBIOS 4.0 Release 6.0<br>IdentificationCode=<br>InstallableLanguages=<br>InstallDate=<br>LanguageEdition=<br>ListOfLanguages=<br>Manufacturer=Phoenix Technologies LTD<br>Name=PhoenixBIOS 4.0 Release 6.0<br>OtherTargetOS=<br>PrimaryBIOS=TRUE<br>ReleaseDate=20120920000000.000000+000<br>SerialNumber=VMware-56 4d 8b 9d 3b a9 3a b4-a7 09 2d ff 09 9a e2 26<br>SMBIOSBIOSVersion=6.00<br>SMBIOSMajorVersion=2<br>SMBIOSMinorVersion=4<br>SMBIOSPresent=TRUE<br>SoftwareElementID=PhoenixBIOS 4.0 Release 6.0<br>SoftwareElementState=3<br>Status=OK<br>TargetOperatingSystem=0<br>Version=INTEL  - 6040000</code></div>
  
### Disk Information
 * **Command with arguments**: `wmic logicaldisk where drivetype=3 get name, freespace, systemname, filesystem, size, volumeserialnumber`
 * **Description**: Retrieve information about the harddrive.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic logicaldisk where drivetype=3 get name, freespace, systemname, filesystem, size, volumeserialnumber<br>FileSystem  FreeSpace    Name  Size         SystemName       VolumeSerialNumber<br>NTFS        33311481856  C:    42947571712  WIN-0P19ULL2NB6  1A095F16</code></div>
   
### Patch IDs
 * **Command with arguments**: `wmic qfe get hotfixid`
 * **Description**: Retrieves BIOS information including system serial number.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic qfe get hotfixid<br>HotFixID<br>KB955430</code></div>	
   
### Process Create
 * **Command with arguments**: `wmic process call create [EXECUTABLE]`
 * **Description**: Launches an executable. Replace [EXECUTABLE] with the name of the executable you'd like to launch (for example: calc.exe). Do not include quotes around the value (for example: *DO* use calc.exe; do *NOT* use "calc.exe"). Another option for this command comes from [Rob Fuller's talk](http://www.slideshare.net/mubix/windows-attacks-at-is-the-new-black-26665607): `wmic /node:DC1 /user:DOMAIN\domainadminsvc /password:domainadminsvc123 process call create "cmd /c vssadmin list shadows 2>&1 > c:\temp\output.txt"`
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic process call create calc.exe<br>Executing (Win32_Process)->Create()<br>Method execution successful.<br>Out Parameters:<br>instance of __PARAMETERS<br>{<br>        ProcessId = 1936;<br>        ReturnValue = 0;<br>};</code></div>	
   
### Process Information
 * **Command with arguments**: `wmic process get caption,executablepath,commandline`
 * **Description**: Retrieves process names, captions, executable paths and command line flags.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic process get caption,executablepath,commandline<br>Caption               CommandLine                                                   ExecutablePath<br>System Idle Process<br>System<br>smss.exe<br>csrss.exe<br>[...SNIP...]<br>dllhost.exe<br>dwm.exe               "C:\Windows\system32\Dwm.exe"                                 C:\Windows\system32\Dwm.exe<br>taskeng.exe           taskeng.exe {72464C44-C181-4387-A20A-569E0267D2AF}            C:\Windows\system32\taskeng.exe<br>TPAutoConnect.exe     TPAutoConnect.exe -q -i vmware -a COM1 -F 30                  C:\Program Files\VMware\VMware Tools\TPAutoConnect.exe<br>explorer.exe          C:\Windows\Explorer.EXE                                       C:\Windows\Explorer.EXE<br>VMwareTray.exe        "C:\Program Files\VMware\VMware Tools\VMwareTray.exe"         C:\Program Files\VMware\VMware Tools\VMwareTray.exe<br>vmtoolsd.exe          "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe" -n vmusr  C:\Program Files\VMware\VMware Tools\vmtoolsd.exe<br>cmd.exe               "C:\Windows\System32\cmd.exe"                                 C:\Windows\System32\cmd.exe<br>cmd.exe<br>TrustedInstaller.exe<br>WMIC.exe              wmic  process get caption,executablepath,commandline          C:\Windows\System32\Wbem\WMIC.exe<br>WmiPrvSE.exe</code></div>
     
### Process Terminate
 * **Command with arguments**: `wmic process where name="[PROCESS]" call terminate`
 * **Description**: Terminates a process. Replace [PROCESS] with the name of the process you'd like to terminate and you *DO* need the quotes around it (for example: calc.exe).
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic process where name="calc.exe" call terminate<br>Executing (\\WIN-0P19ULL2NB6\ROOT\CIMV2:Win32_Process.Handle="1936")->terminate()<br>Method execution successful.<br>Out Parameters:<br>instance of __PARAMETERS<br>{<br>        ReturnValue = 0;<br>};</code></div>
   
### Service Information
 * **Command with arguments**: `wmic service [list full]`
 * **Description**: Retrieves ton of information about all the services installed on the system.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic service list full<br><br><br>AcceptPause=FALSE<br>AcceptStop=TRUE<br>Caption=Application Experience<br>CheckPoint=0<br>CreationClassName=Win32_Service<br>Description=Processes application compatibility cache requests for applications as they are launched<br>DesktopInteract=FALSE<br>DisplayName=Application Experience<br>ErrorControl=Normal<br>ExitCode=0<br>InstallDate=<br>Name=AeLookupSvc<br>PathName=C:\Windows\system32\svchost.exe -k netsvcs<br>ProcessId=1056<br>ServiceSpecificExitCode=0<br>ServiceType=Share Process<br>Started=TRUE<br>StartMode=Auto<br>StartName=localSystem<br>State=Running<br>Status=OK<br>SystemCreationClassName=Win32_ComputerSystem<br>SystemName=WIN-0P19ULL2NB6<br>TagId=0<br>WaitHint=0<br><br><br>AcceptPause=FALSE<br>AcceptStop=FALSE<br>Caption=Application Layer Gateway Service<br>CheckPoint=0<br>CreationClassName=Win32_Service<br>Description=Provides support for 3rd party protocol plug-ins for Internet Connection Sharing<br>DesktopInteract=FALSE<br>DisplayName=Application Layer Gateway Service<br>ErrorControl=Normal<br>ExitCode=1077<br>InstallDate=<br>Name=ALG<br>PathName=C:\Windows\System32\alg.exe<br>ProcessId=0<br>ServiceSpecificExitCode=0<br>ServiceType=Own Process<br>Started=FALSE<br>StartMode=Manual<br>StartName=NT AUTHORITY\LocalService<br>State=Stopped<br>Status=OK<br>SystemCreationClassName=Win32_ComputerSystem<br>SystemName=WIN-0P19ULL2NB6<br>TagId=0<br>WaitHint=0<br>[...Truncated for brevity...]</code></div>

### Share Information
 * **Command with arguments**: `wmic share [list brief]`
 * **Description**: Retrieve information about local shares.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic share list brief
Description         Name      Path
Remote Admin        ADMIN$    C:\Windows
Default share       C$        C:\
Remote IPC          IPC$
Logon server share  NETLOGON  C:\Windows\SYSVOL\sysvol\lab.sky.net\SCRIPTS
Logon server share  SYSVOL    C:\Windows\SYSVOL\sysvol</code></div>
   
### Startup Items
 * **Command with arguments**: `wmic startup [list brief]`
 * **Description**: Shows startup items, which user runs them and full paths to the executables.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic startup list brief<br>Caption              Command                                                       User<br>VMware Tools         "C:\Program Files\VMware\VMware Tools\VMwareTray.exe"         Public<br>VMware User Process  "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe" -n vmusr  Public</code></div>
 
### User Information
 * **Command with arguments**: `wmic useraccount [list full]`
 * **Description**:  Retrieve information about the user accounts on the system.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wmic useraccount list full<br><br><br>AccountType=512<br>Description=Built-in account for administering the computer/domain<br>Disabled=FALSE<br>Domain=LAB<br>FullName=<br>InstallDate=<br>LocalAccount=FALSE<br>Lockout=FALSE<br>Name=Administrator<br>PasswordChangeable=TRUE<br>PasswordExpires=TRUE<br>PasswordRequired=TRUE<br>SID=S-1-5-21-60789211-843652525-1994898995-500<br>SIDType=1<br>Status=OK<br><br><br>AccountType=512<br>Description=Key Distribution Center Service Account<br>Disabled=TRUE<br>Domain=LAB<br>FullName=<br>InstallDate=<br>LocalAccount=FALSE<br>Lockout=FALSE<br>Name=krbtgt<br>PasswordChangeable=TRUE<br>PasswordExpires=TRUE<br>PasswordRequired=TRUE<br>SID=S-1-5-21-60789211-843652525-1994898995-502<br>SIDType=1<br>Status=Degraded<br><br><br>AccountType=512<br>Description=<br>Disabled=FALSE<br>Domain=LAB<br>FullName=John Doe<br>InstallDate=<br>LocalAccount=FALSE<br>Lockout=FALSE<br>Name=johndoe<br>PasswordChangeable=TRUE<br>PasswordExpires=TRUE<br>PasswordRequired=TRUE<br>SID=S-1-5-21-60789211-843652525-1994898995-1001<br>SIDType=1<br>Status=OK<br></code></div>
