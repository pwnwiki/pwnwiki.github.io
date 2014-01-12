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

# Windows CMD Network Commands

The Windows commands below will help you alter systems and move data between Windows systems and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

## netsh
For more information: http://technet.microsoft.com/en-us/library/bb490939.aspx

### Firewall Control
 * **Command with arguments**: `netsh firewall set opmode [disable|enable]`
 * **Description**: Enable or disable the Windows Firewall (requires admin privileges).
 * **Minimum required version**: Windows Vista.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows Vista:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>netsh firewall set opmode enable
Ok.<br/>
C:\Users\johndoe>netsh firewall set opmode disable
Ok.</code></div>
   * <div class="slide" style="cursor: pointer;"> **Windows 7:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>netsh firewall set opmode enable<br/>
IMPORTANT: Command executed successfully.
However, "netsh firewall" is deprecated;
use "netsh advfirewall firewall" instead.
For more information on using "netsh advfirewall firewall" commands
instead of "netsh firewall", see KB article 947709
at http://go.microsoft.com/fwlink/?linkid=121488 .<br/>
Ok.<br/>
C:\Users\johndoe>netsh firewall set opmode disable<br/>
IMPORTANT: Command executed successfully.
However, "netsh firewall" is deprecated;
use "netsh advfirewall firewall" instead.
For more information on using "netsh advfirewall firewall" commands
instead of "netsh firewall", see KB article 947709
at http://go.microsoft.com/fwlink/?linkid=121488 .<br/>
Ok.</code></div>

### Wireless Backdoor Creation
 * **Command with arguments**: 
   1. `netsh wlan set hostednetwork mode=[allow\|disallow]`
   1. `netsh wlan set hostednetwork ssid=<ssid> key=<passphrase> keyUsage=persistent\|temporary`
   1. `netsh wlan [start|stop] hostednetwork`
 * **Description**:
   1. Enables or disables hostednetwork service.
   1. Complete hosted network setup for creating a wireless backdoor.
   1. Starts or stops a wireless backdoor. See below to set it up.
 
Note: Windows 7 only.