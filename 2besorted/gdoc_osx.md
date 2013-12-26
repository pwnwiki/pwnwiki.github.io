
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
