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
 * 111 SUNRPC(UnixRPC)
 * 139 NetBIOS
 * 143 IMAP
 * 389 LDAP
 * 443 HTTPS
 * 445 MicrosoftDS
 * 514 RSH
 * 515 Printers
 * 631 CUPS
 * 1352 LotusNotes
 * 2049 NFS
 * 3000 Webrick (Ruby Webserver)
 * 3389 RDP
 * 4949 Munin
 * 5060 SIP
 * 5631-5632 PCAnywhere
 * 5666(evidence of Nagios server on network) NRPE(*nix)/NSCLIENT++(win)
 * 5900-5906 (Same as X11; display over VNC. SPICE is usually in this range as well) VNC
 * 6000-6009 (seexspy, xwd, xkeyforexploitation) X11
 * 8006 Proxmox
 * 8080 Alt-HTTP
 * 8089(also on 8000) Splunk
 * 8000(mezzanine in development mode for example) AnotherHTTP
 * 8834 Nessus HTTPS
 * 8443 AltHTTPS
 * 9080 Alt-HTTPtomcat
 * 9443 vSphere
 * 9100 Printers
 * 17500 Dropbox lansync

## UDP Discovery: ##
 * easy copy - `53,111,123,161,177,500,514,1194,1434,1900,17185`
 * 53 DNS
 * 111 SUNRPC (Unix RPC)
 * 123 Network Time Protocol (NTP)
 * 161 SNMP
 * 177 XDMCP (via NSE script --script broadcast-xdmcp-discover, discover *nix boxes hosting X)
 * 500 Isakmp (ike PSK Attack)
 * 514 syslog
 * 1194 OpenVPN
 * 1434 MSSQL Ping
 * 1900 UPNP
 * 17185 vxworks debug

## Authentication Ports: ##
 * easy copy - `80,902,1494,5985,5986,6129,8200,9084`
 * Citrix: 1494
 * WinRM: 80, 5985 (HTTP), 5986 (HTTPS)
 * VMware Server: 8200, 902, 9084
 * DameWare: 6129

## Easy-win Ports: ##
 * Java RMI - 1099, 1098
 * coldfusion default stand alone - 8500
 * IPMI UDP(623) (easy crack or auth bypass)
 * 6002, 7002 (sentinel license monitor (reverse dir traversal, sometimes as SYSTEM))
 * GlassFish: 4848
 * easy copy - `9060`
 * IBM Web Sphere: 9060
 * Webmin or BackupExec: 10000
 * memcached: 11211
 * DistCC: 3632
 * SAP Router: 3299

## Database Ports: ##
 * easy copy - `3306,1521-1527,5432,5433,1433,3050,3351,1583,8471,9471`
 * MySQL: 3306
 * PostgreSQL: 5432
 * PostgreSQL 9.2: 5433
 * Oracle TNS Listener: 1521-1527
 * Oracle XDB: 2100
 * MSSQL: 1433
 * Firebird / Interbase: 3050
 * PervasiveSQL: 3351, 1583
 * DB2/AS400 8471, 9471
 * Sybase 5000

## SCADA / ICS:##
(source: http://www.digitalbond.com/tools/the-rack/control-system-port-list/ )
 * BACnet/IP: UDP/47808
 * DNP3: TCP/20000, UDP/20000
 * EtherCAT: UDP/34980
 * Ethernet/IP: TCP/44818, UDP/2222, UDP/44818
 * FL-net: UDP/55000 to 55003
 * Foundation Fieldbus HSETCP/1089 to 1091, UDP/1089 to 1091
 * ICCP: TCP/102
 * Modbus TCP: TCP/502
 * OPC UA Binary: Vendor Application Specific
 * OPC UA Discovery Server: TCP/4840
 * OPC UA XML: TCP/80, TCP/443
 * PROFINET: TCP/34962 to 34964, UDP/34962 to 34964
 * ROC PLus: TCP/UDP 4000

## Interesting Port Ranges: ##
 * HTTP(S) Ports: 8000-9000

## Web easy-win URLs: ##
(moved to: https://etherpad.mozilla.org/weburl-easywins )
`awk '$2~/tcp$/' nmap-services | sort -r -k3 | head -n 1000` # same for udp