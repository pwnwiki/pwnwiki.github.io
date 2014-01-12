# Networking Port Reference #
*TODO* - Switch the NAME: and the PORT # so the port numbers go first.

## TCP Discovery Ports: ##
 * easy copy - `7,21,22,23,25,80,88,110,111,139,143,389,443,445,514,515,631,1352,2049,3000,3389,4949,5060,5631,5632,5666,5900-5905,6000-6009,8000,8006,8080,8089,8443,8834,9080,9100,9443,17500`
 * FTP: 21
 * SSH: 22
 * Telnet: 23
 * SMTP: 25
 * Finger: 7
 * HTTP: 80
 * Kerberos: 88
 * POP3: 110
 * SUNRPC (Unix RPC): 111 (think: rpcinfo)
 * NetBIOS: 139
 * IMAP 143
 * LDAP: 389
 * HTTPS: 443
 * LotusNotes: 1352
 * Microsoft DS: 445
 * RSH: 514
 * CUPS: 631
 * NFS: 2049
 * Webrick(Ruby Webserver): 3000
 * RDP: 3389
 * Munin: 4949 
 * SIP: 5060
 * PCAnywhere: 5631 (5632)
 * NRPE (*nix) /NSCLIENT++ (win): 5666 (evidence of Nagios server on network)
 * Alt-HTTP: 8080
 * Alt-HTTP tomcat: 9080
 * Another HTTP: 8000 (mezzanine in development mode for example)
 * Nessus HTTPS: 8834
 * Proxmox: 8006
 * Splunk: 8089 (also on 8000)
 * Alt HTTPS: 8443
 * vSphere: 9443
 * X11: 6000-6009 (+1 to portnum for additional displays) (see xspy, xwd, xkey for exploitation)
 * VNC: 5900, 5901+ (Same as X11; +1 to portnum for each user/dipslay over VNC. SPICE is usually in this range as well)
Printers: 9100, 515
 * Dropbox lansync: 17500

## UDP Discovery: ##
 * easy copy - `53,123,161,1434`
 * DNS: 53
 * XDMCP: 177 (via NSE script --script broadcast-xdmcp-discover, discover nix boxes hosting X)
 * OpenVPN: 1194
 * MSSQL Ping: 1434
 * SUNRPC (Unix RPC): 111 (yeah, it's UDP, too)
 * SNMP 161
 * Network Time Protocol (NTP): 123 
 * syslog : 514
 * UPNP: 1900
 * Isakmp - 500 (ike PSK Attack)
 * vxworks debug: 17185 (udp)

## Authentication Ports (other than ones already listed): ##
 * easy copy - `1494`
 * Citrix: 1494
 * WinRM: 80,5985 (HTTP), 5986 (HTTPS)
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