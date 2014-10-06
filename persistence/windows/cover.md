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

# Windows Covering Tracks Commands

Commands to run to clean up a system after you have exploited it and to reduce a target's ability to discover what you did while on their system and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

## del
### Delete Logs
 * **Command with arguments**: `del %WINDIR%\*.log /a /s /q /f`
 * **Description**: **MUST be run as an administrator**. Deletes all *.log files from the %WINDIR% directory.
 * **Output**:
   * NA

----

## wevtutil
### List Logs
 * **Command with arguments**: `wevutil el`
 * **Description**: Lists the different log files the system is keeping. More information can be found http://technet.microsoft.com/en-us/library/cc732848(WS.10).aspx
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>wevtutil el
Application
DFS Replication
Directory Service
DNS Server
File Replication Service
HardwareEvents
Internet Explorer
Key Management Service
Security
System
ThinPrint Diagnostics
EndpointMapper
ForwardedEvents
Microsoft-Windows-ADSI/Debug
Microsoft-Windows-Bits-Client/Analytic
Microsoft-Windows-Bits-Client/Operational
Microsoft-Windows-CAPI2/Operational
Microsoft-Windows-CertificateServicesClient-CredentialRoaming/Operational
Microsoft-Windows-CodeIntegrity/Operational
Microsoft-Windows-CodeIntegrity/Verbose
Microsoft-Windows-COM/Analytic
Microsoft-Windows-CorruptedFileRecovery-Client/Operational
Microsoft-Windows-CorruptedFileRecovery-Server/Operational
Microsoft-Windows-CredUI/Diagnostic
Microsoft-Windows-DateTimeControlPanel/Analytic
Microsoft-Windows-DateTimeControlPanel/Debug
Microsoft-Windows-DateTimeControlPanel/Operational
Microsoft-Windows-DCLocator/Debug
Microsoft-Windows-Diagnosis-DPS/Analytic
Microsoft-Windows-Diagnosis-DPS/Debug
Microsoft-Windows-Diagnosis-DPS/Operational
Microsoft-Windows-Diagnosis-MSDT/Debug
Microsoft-Windows-Diagnosis-MSDT/Operational
Microsoft-Windows-Diagnosis-PLA/Debug
Microsoft-Windows-Diagnosis-PLA/Operational
Microsoft-Windows-Diagnosis-WDI/Debug
Microsoft-Windows-Diagnostics-Networking/Debug
[...snip...]</code></div> 

### Clear Logs
 * **Command with arguments**: `wevtutil cl [LOGNAME]`
 * **Description**: **MUST be run as an administrator**.  Clears the contents of a specific log.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>c:\temp>wevtutil cl Microsoft-Windows-EventLog/Debug</code></div>
 * **Remove all logs**: `for /f %a in ('wevtutil el') do @wevtutil cl "%a"`
