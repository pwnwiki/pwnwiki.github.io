# Netcat Usage

`netcat` is a command-line or shell application that can be used for a wide variety of exploitation matters including transferring files, establishing remote shells and more! The official netcat site is http://netcat.sourceforge.net and, although Sourceforge has this repository, most Unix/Linux operating systems have a netcat application that is/can be installed via their packagers (apt-get, ports, etc.).

The [SANS Institute](http://www.sans.org/security-resources/sec560/netcat_cheat_sheet_v1.pdf) has a very good "Cheat Sheet" PDF for netcat commands and functions. Please **note** that "All syntax is designed for the original netcat versions, released by Hobbit and Weld Pond. The syntax here can be adapted for other netcats." So, you may need to modify the commands below. Please do check out their PDF.

## Commands
| Command  | Category | Description / Importance |
| -------- | -------- | ------------------------ |
| **Client:** `nc -l -p [LocalPort] -e relay.bat` <br> **Listener:** `echo nc [TargetIPaddr] [port] > relay.bat` | Relay - Windows | **Listener-to-Client Relay** - Create a relay that sends packets from the local port [LocalPort] to a netcat client connected to [TargetIPaddr] on port [port] |
| **Listener 1:** `echo nc -l -p [LocalPort_2] > relay.bat`<br>**Listener 2:** `nc -l -p [LocalPort_1] -e relay.bat` | Relay - Windows | **Listener-to-Listener Relay** - Create a relay that will send packets from any connection on {LocalPort_1] to any connection on [LocalPort_2] |
| **Client 1:** `echo nc [NextHopIPaddr] [port2] > relay.bat`<br>**Client 2:** `nc [PreviousHopIPaddr] [port] -e relay.bat` | Relay - Windows | **Client-to-Client Relay** - Create a relay that will send packets from the connection to [PreviousHopIPaddr] on port [port] to a Netcat Client connected to [NextHopIPaddr] on port [port2] |
| **Client:** `nc -l -p [LocalPort] > [outfile]`<br>**Listener:** `nc -w3 [TargetIPaddr] [port] < [infile]` | File Transfer - All OS | Push [infile] to [TargetIPaddr] on [port] |
| **Listener:** `nc -l -p [LocalPort] < [infile]`<br>**Client:** `nc -w3 [TargetIPaddr] [port] > [outfile]` | File Transfer - All OS | Connect to [TargetIPaddr] on [port] and retrieve [outfile] |
 
