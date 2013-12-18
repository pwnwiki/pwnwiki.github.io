# Ncat Usage

`ncat` similar to the venerable `netcat`, is a command-line or shell application that can be used for a wide variety of exploitation matters including transferring files, establishing remote shells and more! The official ncat site is http://nmap.org/ncat/.

The examples below are mostly copied from the http://nmap.org/book/ncat-man-examples.html page or http://www.irongeek.com/i.php?page=videos/ncat-nmap-netcat and are not a complete listing of all the examples.

## Commands
| Command  | Description / Importance |
| -------- | ------------------------ |
| `ncat example.org 8080` | Connect to example.org on TCP port 8080. |
| `ncat -l 8080` | Listen for connections on TCP port 8080. |
| `ncat --sh-exec "ncat example.org 80" -l 8080 --keep-open` | Redirect TCP port 8080 on the local machine to host on port 80. |
| `ncat --exec "/bin/bash" -l 8081 --keep-open` | Bind to TCP port 8081 and attach /bin/bash for the world to access freely. |
| `ncat --exec "/bin/bash" --max-conns 3 --allow \`<br>`192.168.0.0/24 -l 8081 --keep-open` | Bind a shell to TCP port 8081, limit access to hosts on a local network, and limit the maximum number of simultaneous connections to 3. |
| `ncat -l --proxy-type http localhost 8888` | Create an HTTP proxy server on localhost port 8888. |
| `HOST1: ncat -l 9899 > outputfile`<br>`HOST2: ncat HOST1 9899 < inputfile` | Send a file over TCP port 9899 from host2 (client) to host1 (server). |
| `HOST1: ncat -l 9899 < inputfile`<br>`HOST2: ncat HOST1 9899 > outputfile` | Transfer in the other direction, turning Ncat into a "one file" server. |
| `echo -e "GET / HTTP/1.0\n\n"`&#124;`ncat google.com 80` | Retrieve the HTML source code of the web server at google.com on TCP port 80. |
| `ncat -t example.org 23` | Connect to example.org's telnet server on TCP port 23. |
| `Server: ncat -l 74 --udp`<br>`Client: ncat --udp localhost 74 < inputfile` | Transfer file from client to server over UDP. |
| `Server: ncat -l 74 --chat`<br>`Client1: ncat localhost 74`<br>`Client2: ncat localhost 74`| Simple chat. |
| `Server: ncat -l --ssl 74 --send-only < inputfile`<br>`Client: ncat localhost 74 --ssl > outputfile` | Transfer file from server to client using SSL encryption. | 
| `ncat -l localhost 80 --sh-exec "ncat google.com 80 -o text.txt -x hex.txt"` | Ncat relay |