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

# Windows Remote Access Commands

Commands that move data and files between systems on a network and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

## Miscellaneous
### dir
 * **Command with arguments**: `dir \\[computername|ip]\share`
 * **Description**: **Must have token to the remote system.** See `net use` below to establish such a connection. Displays the contents of the remote computer's share.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>dir \\192.168.10.34\c$
 Volume in drive \\192.168.10.34\c$ has no label.
 Volume Serial Number is 1A09-5F16<br>
 Directory of \\192.168.10.34\c$<br>
09/18/2006  05:43 PM                24 autoexec.bat
09/18/2006  05:43 PM                10 config.sys
01/19/2008  05:40 AM    <DIR>          PerfLogs
10/08/2013  07:36 PM    <DIR>          Program Files
10/23/2013  08:20 PM    <DIR>          temp
10/10/2013  08:59 PM    <DIR>          Users
10/23/2013  08:38 PM    <DIR>          Windows
               2 File(s)             34 bytes
               5 Dir(s)  33,316,192,256 bytes free</code></div> 
      
### qprocess
 * **Command with arguments**: `qprocess * [/SERVER:computername]`
 * **Description**: Shows information about processes locally or remotely if you provide the computername or IP.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>qprocess * /SERVER:192.168.1.2
 USERNAME              SESSIONNAME         ID    PID  IMAGE
 (unknown)             services             0      0
 (unknown)             services             0      4  system
 (unknown)             services             0    268  smss.exe
 (unknown)             services             0    356  csrss.exe
 (unknown)             services             0    408  wininit.exe
>(unknown)             console              1    420  csrss.exe
>(unknown)             console              1    460  winlogon.exe
 (unknown)             services             0    516  services.exe
>johndoe               console              1   1584  dwm.exe
>johndoe               console              1   1600  explorer.exe
 (unknown)             services             0   1708  vmtoolsd.exe
>johndoe               console              1   1936  vmwaretray.exe
>johndoe               console              1   1944  vmtoolsd.exe
 (unknown)             services             0    316  tpautoconnsv...
>johndoe               console              1   1716  tpautoconnec...
>johndoe               console              1   1680  conhost.exe
 (unknown)             services             0   1984  searchindexe...
 (unknown)             services             0   2076  msdtc.exe
 (unknown)             services             0   2844  svchost.exe
 (unknown)             services             0   2920  sppsvc.exe
 (unknown)             services             0   2976  svchost.exe
>johndoe               console              1   3576  cmd.exe
>johndoe               console              1   3540  conhost.exe
>johndoe               console              1   2340  cmd.exe
>johndoe               console              1   1560  conhost.exe
>johndoe               console              1   3616  qprocess.exe</code></div> 
   
### qwinsta
 * **Command with arguments**: `qwinsta [/SERVER:computername]`
 * **Description**: Shows information about Remote Desktop Sessions locally or remotely if you provide the computername or IP.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>qwinsta<br> SESSIONNAME       USERNAME                 ID  STATE   TYPE        DEVICE<br> services                                    0  Disc<br>>console           johndoe                   1  Active<br> rdp-tcp                                 65536  Listen</code></div> 

### psexec
 * **Command with arguments**: `psexec \\[computername|IP] [cmd]`
 * **Description**: The [`psexec` tool](http://technet.microsoft.com/en-us/sysinternals/bb897553.aspx) executes processes on other systems over a network. Most systems now disable the "clipbook" which `psexec` required. According to Val Smith's and Colin Ames' [BlackHat 2008 presentation (page 50)](http://www.blackhat.com/presentations/bh-usa-08/Smith_Ames/BH_US_08_Smith_Ames_Meta-Post_Exploitation.pdf), you can re-enable the sub-systems needed to use `psexec` using the `sc` commands below.
<pre>
c:\> net use \\[computername|IP]\ipc$ username /user:password
c:\> sc \\[computername|IP] config netdde start= auto
c:\> sc \\[computername|IP] config netddedsdm start= auto
c:\> sc \\[computername|IP] config clipsrv start= auto
c:\> sc \\[computername|IP] start netdde
c:\> sc \\[computername|IP] start netddedsdm
c:\> sc \\[computername|IP] start clipsrv
</pre>
 * **Example Command**: `psexec \\1.1.1.1 ipconfig /all` would retrieve the IP settings for the 1.1.1.1 system.

### tasklist
 * **Command with arguments**: `tasklist /v /s [computername|IP]`
 * **Description**: Retrieve the current running processes from the remote system. [Microsoft manual](http://technet.microsoft.com/en-us/library/bb491010.aspx).
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Windows\system32>tasklist /V /S 192.168.10.34<br>Type the password for WIN-V32NJ7H3AQE\johndoe:************************<br><br><br>Image Name                     PID Session Name        Session#    Mem Usage User Name                                              CPU Time<br>========================= ======== ================ =========== ============ ================================================== ============<br>System Idle Process              0                            0         24 K N/A                                                     4:01:47<br>System                           4                            0      2,244 K N/A                                                     0:00:13<br>smss.exe                       388                            0        696 K NT AUTHORITY\SYSTEM                                     0:00:00<br>csrss.exe                      452                            0      4,992 K NT AUTHORITY\SYSTEM                                     0:00:01<br>csrss.exe                      492                            1     10,800 K NT AUTHORITY\SYSTEM                                     0:00:17<br>wininit.exe                    500                            0      3,740 K NT AUTHORITY\SYSTEM                                     0:00:00<br>winlogon.exe                   532                            1      4,244 K NT AUTHORITY\SYSTEM                                     0:00:00<br>services.exe                   580                            0      7,308 K NT AUTHORITY\SYSTEM                                     0:00:03<br>lsass.exe                      592                            0     36,968 K NT AUTHORITY\SYSTEM                                     0:00:06<br>lsm.exe                        600                            0      5,128 K NT AUTHORITY\SYSTEM                                     0:00:00<br>svchost.exe                    840                            0      6,576 K NT AUTHORITY\SYSTEM                                     0:00:02<br>svchost.exe                    908                            0      6,652 K NT AUTHORITY\NETWORK SERVICE                            0:00:00<br>svchost.exe                    984                            0      7,976 K NT AUTHORITY\LOCAL SERVICE                              0:00:02<br>svchost.exe                   1036                            0      7,992 K NT AUTHORITY\SYSTEM                                     0:00:00<br>svchost.exe                   1056                            0     26,740 K NT AUTHORITY\SYSTEM                                     0:00:08<br>SLsvc.exe                     1072                            0     11,280 K NT AUTHORITY\NETWORK SERVICE                            0:00:12<br>svchost.exe                   1124                            0      9,720 K NT AUTHORITY\LOCAL SERVICE                              0:00:01<br>svchost.exe                   1184                            0      8,888 K NT AUTHORITY\SYSTEM                                     0:00:01<br>svchost.exe                   1208                            0     15,332 K NT AUTHORITY\NETWORK SERVICE                            0:00:01<br>svchost.exe                   1368                            0     10,140 K NT AUTHORITY\LOCAL SERVICE                              0:00:00<br>taskeng.exe                   1572                            0      7,024 K NT AUTHORITY\SYSTEM                                     0:00:00<br>spoolsv.exe                   1680                            0      9,892 K NT AUTHORITY\SYSTEM                                     0:00:00<br>dfsrs.exe                     1732                            0      8,608 K NT AUTHORITY\SYSTEM                                     0:00:00<br>dns.exe                       1756                            0     39,456 K NT AUTHORITY\SYSTEM                                     0:00:00</code></div> 
----

## net
### net time
 * **Command with arguments**: `net time \\[computername|ip]`
 * **Description**: Display the time from the remote system.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>net time \\192.168.10.34
Current time at \\192.168.10.34 is 10/23/2013 9:03:04 PM<br>
The command completed successfully.</code></div> 

### net use
 * **Command with arguments**: `net use \\[computername|ip] [/user:DOMAIN\USERNAME] [password]	`
 * **Description**: Create a connection to the remote computer. This maps IPC$ which does not show up as a drive but allows you to access the remote system as the current user. If the user you launch the command as is not valid on the remote system you will need to specify a valid DOMAIN\USER and PASSWORD. This is useful when you have credentials from somewhere and wish to use them but do not have an active token on a machine you have a session on.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>net use \\192.168.10.34 /user:lab\johndoe
The password or user name is invalid for \\192.168.10.34.<br>
Enter the password for 'lab\johndoe' to connect to '192.168.10.34':
The command completed successfully.</code></div> 
