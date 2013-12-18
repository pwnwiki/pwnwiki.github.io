# socat Usage

`socat` or SOcket CAT, similar to the venerable `netcat`, is a command-line or shell application that can be used for a wide variety of exploitation matters including transferring files, establishing remote shells, SSL transport, IPv6 networking and more! The official socat site is http://www.dest-unreach.org/socat/.

An important piece to understand about `socat` is that the format of the command is: `socat [options] <address> <address>` where `<address>` is in a special format. Check out the docs here http://www.dest-unreach.org/socat/doc/socat.html#ADDRESS_TYPES for more information. 

The examples below are mostly copied from the http://www.dest-unreach.org/socat/doc/socat.html#EXAMPLES page.

## Commands
| Command  | Description / Importance |
| -------- | ------------------------ |
| `socat - TCP4:www.domain.org:80` | transfers data between STDIO (-) and a TCP4 connection to port 80 of host www.domain.org. This example results in an interactive connection similar to telnet or netcat. The stdin terminal parameters are not changed, so you may close the relay with ^D or abort it with ^C. |
| `socat -d -d READLINE,history=$HOME/.http_history \`<br>`TCP4:www.domain.org:www,crnl` | this is similar to the previous example, but you can edit the current line in a bash like manner (READLINE) and use the history file .http_history; socat prints messages about progress (-d -d). The port is specified by service name (www), and correct network line termination characters (crnl) instead of NL are used. |
| `socat TCP4-LISTEN:www TCP4:www.domain.org:www` | installs a simple TCP port forwarder. With TCP4-LISTEN it listens on local port "www" until a connection comes in, accepts it, then connects to the remote host (TCP4) and starts data transfer. It will not accept a econd connection. |
| `socat -d -d -lmlocal2 TCP4-LISTEN:80,bind=myaddr1, \`<br>`su=nobody,fork,range=10.0.0.0/8,reuseaddr  \`<br>`TCP4:www.domain.org:80,bind=myaddr2` | TCP port forwarder, each side bound to another local IP address (bind). This example handles an almost arbitrary number of parallel or consecutive connections by fork'ing a new process after each accept() . It provides a little security by su'ing to user nobody after forking; it only permits connections from the private 10 network (range); due to reuseaddr, it allows immediate restart after master process's termination, even if some child sockets are not completely shut down. With -lmlocal2, socat logs to stderr until successfully reaching the accept loop. Further logging is directed to syslog with facility local2. |
