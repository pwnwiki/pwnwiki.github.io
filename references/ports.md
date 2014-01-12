# Networking Port Reference #
*TODO* - Switch the NAME: and the PORT # so the port numbers go first.

## TCP Discovery Ports: ##
 * easy copy - `7,21,22,23,25,80,88,110,111,139,143,389,443,445,514,515,631,1352,2049,3000,3389,4949,5060,5631,5632,5666,5900-5905,6000-6009,8000,8006,8080,8089,8443,8834,9080,9100,9443,17500`
 * 7 Finger
 * 21 FTP
 * 22 SSH
 * 23 Telnet
 * 25 SMTP
 * 80 HTTP
 * 88 Kerberos
 * 110 POP3
 * 111 SUNRPC (UnixRPC)
 * 139 NetBIOS
 * 143 IMAP
 * 389 LDAP
 * 443 HTTPS
 * 445 Microsoft DS
 * 514 RSH
 * 515 Printers
 * 631 CUPS
 * 1352 Lotus Notes
 * 2049 NFS
 * 3000 Webrick (Ruby Webserver)
 * 3389 RDP
 * 4949 Munin
 * 5060 SIP
 * 5631-5632 PCAnywhere
 * 5666 Nagios server/NRPE(*nix)/NSCLIENT++(win)
 * 5900-5906 VNC (Same as X11; display over VNC. SPICE is usually in this range as well)
 * 6000-6009 Xll (seexspy, xwd, xkeyforexploitation)
 * 8006 Proxmox
 * 8080 Alt-HTTP
 * 8089 Splunk (also on 8000)
 * 8000 Another HTTP (mezzanine in development mode for example)
 * 8834 Nessus HTTPS
 * 8443 AltHTTPS
 * 9080 Alt-HTTPtomcat
 * 9443 vSphere
 * 9100 Printers
 * 17500 Dropbox lansync

## UDP Discovery: ##
 * easy copy - `53,111,123,161,177,500,514,623,1194,1434,1900,17185`
 * 53 DNS
 * 111 SUNRPC (Unix RPC)
 * 123 Network Time Protocol (NTP)
 * 161 SNMP
 * 177 XDMCP (via NSE script --script broadcast-xdmcp-discover, discover *nix boxes hosting X)
 * 500 Isakmp (ike PSK Attack)
 * 514 syslog
 * 623 IPMI (easy crack or auth bypass)
 * 1194 OpenVPN
 * 1434 MSSQL Ping
 * 1900 UPNP
 * 17185 vxworks debug

## Authentication Ports: ##
 * easy copy - `80,902,1494,5985,5986,6129,8200,9084`
 * 80,5985,5986 WinRM (5985 (HTTP), 5986 (HTTPS))
 * 902,8200,9084 VMware Server
 * 1494 Citrix
 * 6129 DameWare

## Easy-win Ports: ##
 * easy copy - `1098-1099,3299,3632,4848,6002,7002,8500,9060,10000,11211`
 * 1098-1099 Java RMI
 * 3299 SAP Router
 * 3632 DistCC
 * 4848 GlassFish
 * 6002,7002 (Sentinel license monitor (reverse dir traversal, sometimes as SYSTEM))
 * 8500 Coldfusion default stand alone
 * 9060 IBM Web Sphere
 * 10000 Webmin or BackupExec
 * 11211 memcached

## Database Ports: ##
 * easy copy - `1433,1521-1527,1583,3351,2100,3050,3306,5000,5432,5433,8471,9471`
 * 1433 MSSQL
 * 1521-1527 Oracle TNS Listener
 * 1583,3351 PervasiveSQL
 * 2100 Oracle XDB
 * 3050 Firebird/Interbase
 * 3306 MySQL
 * 5000 Sybase
 * 5432 PostgreSQL
 * 5433 PostgreSQL 9.2
 * 8471,9471 DB2/AS400

## SCADA / ICS:##
(source: http://www.digitalbond.com/tools/the-rack/control-system-port-list/ )
 * BACnet/IP: UDP/47808
 * DNP3: TCP/20000, UDP/20000
 * EtherCAT: UDP/34980
 * Ethernet/IP: TCP/44818, UDP/2222, UDP/44818
 * FL-net: UDP/55000-55003
 * Foundation Fieldbus HSETCP/1089-1091, UDP/1089-1091
 * ICCP: TCP/102
 * Modbus TCP: TCP/502
 * OPC UA Binary: Vendor Application Specific
 * OPC UA Discovery Server: TCP/4840
 * OPC UA XML: TCP/80, TCP/443
 * PROFINET: TCP/34962-34964, UDP/34962-34964
 * ROC PLus: TCP/UDP 4000

## Interesting Port Ranges: ##
 * 8000-9000 HTTP(S) Ports

## Web easy-win URLs: ##
(moved to: https://etherpad.mozilla.org/weburl-easywins )
`awk '$2~/tcp$/' nmap-services | sort -r -k3 | head -n 1000` # same for udp