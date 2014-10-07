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

The Windows commands below will help you gather information about the victim system's network connections, devices and capabilities and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

## ipconfig
### Retrieve Local DNS Cache Info
 * **Command with arguments**: `ipconfig /displaydns`
 * **Description**: Displays the system's local DNS cache.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>ipconfig /displaydns<br>Windows IP Configuration<br>
    1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa
    ----------------------------------------<br>    Record Name . . . . . : 1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa.
    Record Type . . . . . : 12
    Time To Live  . . . . : 86400
    Data Length . . . . . : 4
    Section . . . . . . . : Answer
    PTR Record  . . . . . : localhost<br><br>
    1.0.0.127.in-addr.arpa
    ----------------------------------------<br>    Record Name . . . . . : 1.0.0.127.in-addr.arpa.
    Record Type . . . . . : 12
    Time To Live  . . . . : 86400
    Data Length . . . . . : 4
    Section . . . . . . . : Answer
    PTR Record  . . . . . : localhost<br><br>
    _ldap._tcp.default-first-site-name._sites.win-0p19ull2nb6.lab.sky.net
    ----------------------------------------<br>    Name does not exist.<br><br>
    _ldap._tcp.win-0p19ull2nb6.lab.sky.net
    ----------------------------------------<br>    Name does not exist.<br><br>
    localhost
    ----------------------------------------<br>    Record Name . . . . . : localhost
    Record Type . . . . . : 1
    Time To Live  . . . . : 86400
    Data Length . . . . . : 4
    Section . . . . . . . : Answer
    A (Host) Record . . . : 127.0.0.1<br><br>
    localhost
    ----------------------------------------<br>    Record Name . . . . . : localhost
    Record Type . . . . . : 28
    Time To Live  . . . . : 86400
    Data Length . . . . . : 16
    Section . . . . . . . : Answer
    AAAA Record . . . . . : ::1</code>       
</div>
    
### Retrieve NIC Info
 * **Command with arguments**: `ipconfig /all`
 * **Description**: Displays the full information about the system's network interface cards (NICs).
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\jondoe>ipconfig /all<br>
Windows IP Configuration<br>
   Host Name . . . . . . . . . . . . : WIN-0P19ULL2NB6
   Primary Dns Suffix  . . . . . . . : lab.sky.net
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : lab.sky.net
                                       sky.net<br>
Ethernet adapter Local Area Connection:<br>
   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Intel(R) PRO/1000 MT Network Connection
   Physical Address. . . . . . . . . : 00-0C-29-9A-E2-26
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::11bc:e019:25e5:916d%10(Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.10.34(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.10.1
   DHCPv6 IAID . . . . . . . . . . . : 234884137
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-19-E6-78-04-00-0C-29-9A-E2-26
   DNS Servers . . . . . . . . . . . : ::1
                                       127.0.0.1
   NetBIOS over Tcpip. . . . . . . . : Enabled<br>
Tunnel adapter Local Area Connection* 8:<br>
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : isatap.{DDE3DF3D-3417-4EBF-BF66-73BD3A64FF26}
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes</code></div>
----

## Misc
### arp
 * **Command with arguments**: `arp -a`
 * **Description**: Lists all the systems currently in the machine's ARP table.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>arp -a<br>
Interface: 192.168.10.34 --- 0xa
  Internet Address      Physical Address      Type
  192.168.10.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.252           01-00-5e-00-00-fc     static</code></div> 

### wmic
 * **Command with arguments**: `wmic ntdomain list`
 * **Description**: Retrieve information about Domain and Domain Controller.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>wmic ntdomain list
DomainGuid
{CD5C2FE3-5AFE-459D-804E-A81B49066CAD}</code></div>    
----

## net
For more information: http://technet.microsoft.com/en-us/library/bb490949.aspx

### Accounts
 * **Command with arguments**: `net accounts [/domain | /domain:OTHERDOMAINNAME]`
 * **Description**: Prints the password policy for the local system. Pass it the `/domain` option to query the domain for the domain password policy.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>net accounts
Force user logoff how long after time expires?:       Never
Minimum password age (days):                          1
Maximum password age (days):                          42
Minimum password length:                              7
Length of password history maintained:                24
Lockout threshold:                                    Never
Lockout duration (minutes):                           30
Lockout observation window (minutes):                 30
Computer role:                                        PRIMARY
The command completed successfully.</code></div>    

### Group
 * **Command with arguments**: `net group "GROUPNAME" /domain`
 * **Description**: Prints the members of the Administrators local group. The /domain switch can show you the list of current domain admins.
 
Note: This command can only be used on a Windows Domain Controller.
 
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>net group "domain admins"
Group name     Domain Admins
Comment        Designated administrators of the domain<br>
Members<br>
-------------------------------------------------------------------------------<br>
Administrator
The command completed successfully.</code></div>    

### Local Group
 * **Command with arguments**: `net localgroup "GROUPNAME" [/domain]`
 * **Description**: Prints the members of the local group "GROUPNAME". The `/domain` switch can show you members of domain groups.
 
Note: This command can only be used on a Windows Domain Controller.
 
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>net localgroup administrators
Alias name     administrators
Comment        Administrators have complete and unrestricted access to the computer/domain<br>
Members<br>
-------------------------------------------------------------------------------<br>
Administrator
Domain Admins
Enterprise Admins
johndoe
The command completed successfully.</code></div>  

### Queries SMB Hosts/Domain
 * **Command with arguments**: `net view [/domain | /domain:OTHERDOMAINNAME]`
 * **Description**: Queries NBNS/SMB (SAMBA) and tries to find all hosts in the system's current workgroup. Add the `/domain` option if the current system is joined to a domain. To query a different domain, use the `/domain:OTHERDOMAINNAME` option.
 * **Output**:
   * (Coming soon!)
   
### Session
 * **Command with arguments**: `net session`
 * **Description**: Displays information about all connections to the computer. 
 
Note: Needs to be launched within an administrative command shell.
 
 * **Output**:
   * (Coming soon!)
   
### Local Shares
 * **Command with arguments**: `net share`
 * **Description**: Displays the system's currently shared SMB entries, and what path(s) they point to.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>net share<br>
Share name   Resource                        Remark<br>
-------------------------------------------------------------------------------<br>C$           C:\                             Default share
IPC$                                         Remote IPC
ADMIN$       C:\Windows                      Remote Admin
NETLOGON     C:\Windows\SYSVOL\sysvol\lab.sky.net\SCRIPTS Logon server share
SYSVOL       C:\Windows\SYSVOL\sysvol        Logon server share
The command completed successfully.</code></div>

### Remote Shares
 * **Command with arguments**: `net view *share*`
 * **Description**: Displays the system's currently shared SMB entries, and what path(s) they point to.
 * **Example**: `net view \\w2k3-srv/`
 * **Output**:
   
### Users (List local/domain)
 * **Command with arguments**: `net user [/domain]`
 * **Description**: Lists the local users or, if the `/domain` option is passed, users on the computer's domain. 
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>net user<br>
User accounts for \\WIN-0P19ULL2NB6<br>
-------------------------------------------------------------------------------<br>Administrator            Guest                    johndoe<br>krbtgt<br>The command completed successfully. </code></div> 
   
### Users (Detailed User Information)
 * **Command with arguments**: `net user %USERNAME% [/domain]`
 * **Description**: Lists detailed information about the current local user or, if the `/domain` option is passed, the account on the computer's domain. If it is a local user then drop the `/domain`. Important things to note are login times, last time changed password, logon scripts, and group membership. You may wish to run this twice, once with and once without the `/domain` switch to find both local and domain accounts.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>net user johndoe
User name                    johndoe
Full Name                    John Doe
Comment
User's comment
Country code                 000 (System Default)
Account active               Yes
Account expires              Never<br>
Password last set            10/10/2013 8:57:02 PM
Password expires             11/21/2013 8:57:02 PM
Password changeable          10/11/2013 8:57:02 PM
Password required            Yes
User may change password     Yes<br>
Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   10/15/2013 6:53:42 PM<br>
Logon hours allowed          All<br>
Local Group Memberships      \*Administrators       \*Users
Global Group memberships     \*Domain Users
The command completed successfully.</code></div>

----

## netsh
For more information: http://technet.microsoft.com/en-us/library/bb490939.aspx

### Network Services
 * **Command with arguments**: `netsh diag show all`
 * **Description**: Shows information on network services and adapters.

Note: Windows XP only.

 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows XP SP3:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>netsh diag show all<br/>
Default Outlook Express Mail (Not Configured)<br/>
Default Outlook Express News (Not Configured)<br/>
Internet Explorer Web Proxy (Not Configured)<br/>
Loopback (127.0.0.1)<br/>
Computer System (OJ-75E3B8CC9475)<br/>
Operating System (Microsoft Windows XP Professional)<br/>
Version (5.1.2600)<br/>
Modems<br/>
Network Adapters
     1. [00000001] VMware Accelerated AMD PCNet Adapter
     2. [00000010] VMware Accelerated AMD PCNet Adapter<br/>
Network Clients
     1. VMware Shared Folders
     2. Microsoft Terminal Services
     3. Microsoft Windows Network
     4. Web Client Network
</code></div>

### Firewall Status
 * **Command with arguments**: `netsh firewall show conf`
 * **Description**: Show the configuration of the Windows Firewall

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
   
### Wireless Profile Viewing
 * **Command with arguments**: `netsh wlan show profiles`
 * **Description**: Shows all saved wireless profiles. You may then export the info for those profiles with the other netsh commands listed here.
   
### Wireless Profile Exporting
 * **Command with arguments**: `netsh wlan export profile folder=. key=clear`
 * **Description**: Exports a user wifi profile with the password in plaintext to an XML file in the current working directory.
   
----
## netstat
For more information: http://technet.microsoft.com/en-us/library/bb490947.aspx

### Find Information about a specific Service
 * **Command with arguments**: `netstat -nabo | findstr /I (SERVICE|PROCESS|PORT)`
 * **Description**: If you are interested in finding out more information about a specific service, process or port this will provide greater depth of information. The `netstat -b` flag makes the command take longer but will output the process name using each of the connections. 

Note: Needs to be launched within an administrative command shell due to the `-b`.

 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Windows\system32>netstat -nabo |findstr /I 445<br>
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    [::]:445               [::]:0                 LISTENING       4
  UDP    0.0.0.0:62445          *:*                                    1756
  UDP    0.0.0.0:63445          *:*                                    1756
  UDP    [::]:49445             *:*                                    1756
  UDP    [::]:64445             *:*                                    1756
  UDP    [::]:64450             *:*                                    1756
  UDP    [::]:64451             *:*                                    1756</code></div>
  
### Find Listeners
 * **Command with arguments**: `netstat -na | findstr :80`
 * **Description**: Find all listening ports and connections on port 80 (replace 80 with your target such as `445` or `3389`).
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>netstat -na | findstr :445
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING
  TCP    [::]:445               [::]:0                 LISTENING</code></div>

### Find Listeners and Process IDs
 * **Command with arguments**: `netstat -nao | findstr /I listening`
 * **Description**: Find all listening ports and their associated PIDs (Process IDs). The `findstr /I` switch makes the search case insensitive. This could be important if you are looking for a buMPy service (example: `svchost` vs. `SVChost`) or don't know the case of it.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>netstat -nao | findstr /I listening
  TCP    0.0.0.0:88             0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       908
  TCP    0.0.0.0:389            0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:464            0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:593            0.0.0.0:0              LISTENING       908
  TCP    0.0.0.0:636            0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:3268           0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:3269           0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:3389           0.0.0.0:0              LISTENING       1208
  TCP    0.0.0.0:49152          0.0.0.0:0              LISTENING       500
  TCP    0.0.0.0:49153          0.0.0.0:0              LISTENING       984
  TCP    0.0.0.0:49154          0.0.0.0:0              LISTENING       1056
  TCP    0.0.0.0:49156          0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:49157          0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:49158          0.0.0.0:0              LISTENING       592
  TCP    0.0.0.0:49161          0.0.0.0:0              LISTENING       1804
  TCP    0.0.0.0:49169          0.0.0.0:0              LISTENING       1756
  TCP    0.0.0.0:49170          0.0.0.0:0              LISTENING       580
  TCP    127.0.0.1:53           0.0.0.0:0              LISTENING       1756
  TCP    192.168.10.34:53       0.0.0.0:0              LISTENING       1756
  TCP    192.168.10.34:139      0.0.0.0:0              LISTENING       4
  TCP    [::]:88                [::]:0                 LISTENING       592
  TCP    [::]:135               [::]:0                 LISTENING       908
  TCP    [::]:389               [::]:0                 LISTENING       592
  TCP    [::]:445               [::]:0                 LISTENING       4
  TCP    [::]:464               [::]:0                 LISTENING       592
  TCP    [::]:593               [::]:0                 LISTENING       908
  TCP    [::]:636               [::]:0                 LISTENING       592</code></div>

### List Ports and Connections
 * **Command with arguments**: `netstat -nabo`
 * **Description**: Lists ports on and connections with the system with corresponding process (`-b`), without performing DNS lookup (`-n`), all connections (`-a`) and what is the owning process ID (`-o`). The `-b` switch is the switch in this command that requires elevated or admin privileges to execute. Omit it and you do not need to have an admin cmd shell.
 
 Note: Needs to be launched within an administrative command shell.
 
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Windows\system32>netstat -nabo<br>
Active Connections<br>
  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:88             0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       908
  RpcSs
 [svchost.exe]
  TCP    0.0.0.0:389            0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4<br>
 Can not obtain ownership information<br>
x: Windows Sockets initialization failed: 5
  TCP    0.0.0.0:464            0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    0.0.0.0:593            0.0.0.0:0              LISTENING       908
  RpcSs
 [svchost.exe]
  TCP    0.0.0.0:636            0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    0.0.0.0:3268           0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    0.0.0.0:3269           0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    0.0.0.0:3389           0.0.0.0:0              LISTENING       1208
  Dnscache</code></div> 

### Routing Table
 * **Command with arguments**: `netstat -r`
 * **Description**: Displays the system's routing table.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code>C:\Users\johndoe>netstat -r<br>===========================================================================<br>Interface List<br> 10 ...00 0c 29 9a e2 26 ...... Intel(R) PRO/1000 MT Network Connection<br>  1 ........................... Software Loopback Interface 1<br> 12 ...00 00 00 00 00 00 00 e0  isatap.{DDE3DF3D-3417-4EBF-BF66-73BD3A64FF26}<br> 11 ...02 00 54 55 4e 01 ...... Teredo Tunneling Pseudo-Interface<br>===========================================================================<br><br>IPv4 Route Table<br>===========================================================================<br>Active Routes:<br>Network Destination        Netmask          Gateway       Interface  Metric<br>          0.0.0.0          0.0.0.0     192.168.10.1    192.168.10.34    266<br>        127.0.0.0        255.0.0.0         On-link         127.0.0.1    306<br>        127.0.0.1  255.255.255.255         On-link         127.0.0.1    306<br>  127.255.255.255  255.255.255.255         On-link         127.0.0.1    306<br>     192.168.10.0    255.255.255.0         On-link     192.168.10.34    266<br>    192.168.10.34  255.255.255.255         On-link     192.168.10.34    266<br>   192.168.10.255  255.255.255.255         On-link     192.168.10.34    266<br>        224.0.0.0        240.0.0.0         On-link         127.0.0.1    306<br>        224.0.0.0        240.0.0.0         On-link     192.168.10.34    266<br>  255.255.255.255  255.255.255.255         On-link         127.0.0.1    306<br>  255.255.255.255  255.255.255.255         On-link     192.168.10.34    266<br>===========================================================================<br>Persistent Routes:<br>  Network Address          Netmask  Gateway Address  Metric<br>          0.0.0.0          0.0.0.0     192.168.10.1  Default<br>===========================================================================<br><br>IPv6 Route Table<br>===========================================================================<br>Active Routes:<br> If Metric Network Destination      Gateway<br>  1    306 ::1/128                  On-link<br> 10    266 fe80::/64                On-link<br> 10    266 fe80::11bc:e019:25e5:916d/128<br>                                    On-link<br>  1    306 ff00::/8                 On-link<br> 10    266 ff00::/8                 On-link<br>===========================================================================<br>Persistent Routes:<br>  None</code></div>
---

## nbtstat

### List Listening Services on A Remote Machine
 * **Command with arguments**: `nbtstat -A *target ip*`
 * **Description**: Displays the target PC's listening services
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code></code></div>

---
## telnet

### Basic Info Grab
 * **Command with arguments**: `telnet *ip address* *port*`
 * **Description**: Establishes a connection to the target IP and port, pressing enter a few times might display information about the software running on that port.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide ![](images/output.jpg)</div><div class="view"><code> Trying 173.194.118.9... <br />Connected to google.com.<br />Escape character is '^]'.<br />GET / HTTP/1.1<br /><br />HTTP/1.1 302 Found<br />Cache-Control: private<br />Content-Type: text/html; charset=UTF-8<br />Location: http://www.google.nl/?gfe_rd=cr&ei=r0T_U566H8iU8QerrYG4Ag <br /> Content-Length: 258<br />Date: Thu, 28 Aug 2014 15:03:11 GMT<br />Server: GFE/2.0<br />Alternate-Protocol: 80:quic<br />....</br></code></div>
---

## reg

### Enumerate keys
 * **Command with arguments**: `reg query *key*`
 * **Description**: Queries a key on the system and retrieves its contents.
 * **Example**: `reg query HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

---
