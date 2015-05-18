
Introduction
----------------------
Privilege escalation is driven by information gathering. 

Straight-forward vectors include vulnerable kernels, vulnerable services running as root and setuid programs, but often escalation is achieved through the manipulation of file permissions, paths and other subtle mis-configurations. 


Methodology 
----------------------

1) Information Gathering
2) Process 
3) Exploit 
4) Repeat - (extensive trial and error is often required)


Information Gathering 
----------------------

## Operating System Enumeration

The distribution and kernel versions will be key pieces of information in attempting to locate a viable local privilege escalation attack. Often a particular kernel version or linux distribution will be vulnerable to a well known specific exploit or avenue for privilege escalation.

**Determine linux distribution and version** 
```bash 
cat /etc/issue
cat /etc/*-release
cat /etc/lsb-release
cat /etc/redhat-release
cat /etc/os-release
```

**Determine kernel version - 32 or 64-bit?** 
```bash
cat /proc/version
uname -a
uname -mrs
rpm -q kernel
dmesg | grep Linux
ls /boot | grep vmlinuz-
```

**List environment variables** 
```bash
cat /etc/profile
cat /etc/bashrc
cat ~/.bash_profile
cat ~/.bashrc
cat ~/.bash_logout
env
```

**Determine if there is a printer** 
```bash
lpstat -a
```

## Applications and Services Enumeration

**Determine which services are running**
```bash
ps aux
ps -ef
top
cat /etc/service 
```

**Determine which services are running as root**
```bash
ps aux | grep root
ps -ef | grep root
``` 

**Determine installed applications**
```bash 
ls -alh /usr/bin/
ls -alh /sbin/
dpkg -l
rpm -qa
ls -alh /var/cache/apt/archivesO
ls -alh /var/cache/yum/
yum list | grep installed
Solaris: pkginfo
Arch Linux: pacman -Q 
```


**Determine versions of important applications** 
```bash 
gcc -v
mysql --version
java -version
python --version
ruby -v
perl -v
```

**Review installed configurations**

Syslog Configuration
```bash
cat /etc/syslog.conf
``` 
Web Server Configurations
```bash 
cat /etc/chttp.conf
cat /etc/lighttpd.conf
cat /etc/apache2/apache2.conf
cat /etc/httpd/conf/httpd.conf
cat /opt/lampp/etc/httpd.conf
```
PHP Configuration
```bash 
/etc/php5/apache2/php.ini
```
Printer (cupsd) Configuration 
```bash 
cat /etc/cups/cupsd.conf 
``` 
MySQL Configuration
```bash
cat /etc/my.conf
```
Inetd Configuration
```bash 
cat /etc/inetd.conf 
```
List All 
```bash 
ls -aRl /etc/ | awk '$1 ~ /^.*r.*/'
```

**Determine scheduled jobs**
```bash
crontab -l
ls -alh /var/spool/cron
ls -al /etc/ | grep cron
ls -al /etc/cron*
cat /etc/cron*
cat /etc/at.allow
cat /etc/at.deny
cat /etc/cron.allow
cat /etc/cron.deny
cat /etc/crontab
cat /etc/anacrontab
cat /var/spool/cron/crontabs/root
``` 

**Locate any plaintext usernames and passwords**
```bash 
grep -i user [filename]
grep -i pass [filename]
grep -C 5 "password" [filename]
find . -name "*.php" -print0 | xargs -0 grep -i -n "var $password"   # Joomla 
```
## Communications and Networking Enumeration 

**Identify connected NICs and other networks**
```bash 
/sbin/ifconfig -a
cat /etc/network/interfaces
cat /etc/sysconfig/network
``` 

**Identify connected users and hosts** 
```bash 
lsof -nPi
lsof -i :80
grep 80 /etc/services
netstat -antup
netstat -antpx
netstat -tulpn
chkconfig --list
chkconfig --list | grep 3:on
last
w
```

**Identify cached IP or MAC addresses**
```bash
arp -a
route -n
/sbin/route -nee
ip ro show
```

**Identify network configuration Settings (DHCP, DNS, Gateway)** 
```bash
cat /etc/resolv.conf
cat /etc/hosts
cat /etc/sysconfig/network
cat /etc/networks
iptables -L
iptables -t nat -L
hostname
dnsdomainname
```

**Is packet sniffing possible** 
```bash
# tcpdump tcp dst [ip] [port] and tcp dst [ip] [port]
tcpdump tcp dst 192.168.1.7 80 and tcp dst 10.2.2.222 21
```

**Check for ports open for local only connections** 
```bash
netstat -tupan
```

**Is tunnelling possible** 
```bash 
ssh -D 127.0.0.1:9050 -N [username]@[ip] 
proxychains ifconfig
```

## User and Confidential Information Enumeration

**Identify the current user and users in the system**
```bash
id
who
w
last 
cat /etc/passwd | cut -d :  -f 1  # List users
grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}'   # List of super users
awk -F: '($3 == "0") {print}' /etc/passwd   # List of super users
``` 

**List Sudoers**
```bash 
cat /etc/sudoers
```

**Show which commands sudo allows you to run**
```bash 
sudo -l
```

**Attempt to display sensitive files** 
```bash
cat /etc/passwd
cat /etc/group
cat /etc/shadow
ls -alh /var/mail/
``` 

**Check for anything interesting in home directories** 
```bash
ls -ahlR /root/
ls -ahlR /home/
```

**Are there any hardcoded passwords in scripts, databases or configuration files**
```bash
cat /var/apache2/config.inc
cat /var/lib/mysql/mysql/user.MYD 
cat /root/anaconda-ks.cfg
```

**Dump all Local, LDAP, NIS, etc password hashes
```bash
getent passwd
```

**Check user history for credentials and activity**
```bash
cat ~/.bash_history
cat ~/.nano_history
cat ~/.atftp_history
cat ~/.mysql_history 
cat ~/.php_history
```

**Check user profile and mail**
```bash
cat ~/.bashrc
cat ~/.profile
cat /var/mail/root
cat /var/spool/mail/root
```

**Check for mail aliases or all aliases**
```bash
cat /etc/aliases
getent aliases
```

**Check for accessible private keys**
```bash 
cat ~/.ssh/authorized_keys
cat ~/.ssh/identity.pub
cat ~/.ssh/identity
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_rsa
cat ~/.ssh/id_dsa.pub
cat ~/.ssh/id_dsa
cat /etc/ssh/ssh_config
cat /etc/ssh/sshd_config
cat /etc/ssh/ssh_host_dsa_key.pub
cat /etc/ssh/ssh_host_dsa_key
cat /etc/ssh/ssh_host_rsa_key.pub
cat /etc/ssh/ssh_host_rsa_key
cat /etc/ssh/ssh_host_key.pub
cat /etc/ssh/ssh_host_key
```
 

## File System Enumeration
The following commands are helpful when looking to exploit local applications for privilege escalation

**Find writeable configuration files in /etc** 
```bash
ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null     # Anyone
ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null        # Owner
ls -aRl /etc/ | awk '$1 ~ /^.....w/' 2>/dev/null    # Group
ls -aRl /etc/ | awk '$1 ~ /w.$/' 2>/dev/null          # Other

find /etc/ -readable -type f 2>/dev/null                         # Anyone
find /etc/ -readable -type f -maxdepth 1 2>/dev/null   # Anyone 
```

**Examine /var structure (logs, configuration files** 
```bash 
ls -alh /var/log
ls -alh /var/mail
ls -alh /var/spool
ls -alh /var/spool/lpd 
ls -alh /var/lib/pgsql
ls -alh /var/lib/mysql
cat /var/lib/dhcp3/dhclient.leases
```

**Any hidden files / settings on a hosted website**
```bash 
ls -alhR /var/www/
ls -alhR /srv/www/htdocs/ 
ls -alhR /usr/local/www/apache22/data/
ls -alhR /opt/lampp/htdocs/ 
ls -alhR /var/www/html/
``` 

**Check Local Log Files** 
```bash
# http://www.thegeekstuff.com/2011/08/linux-var-log-files/
cat /etc/httpd/logs/access_log
cat /etc/httpd/logs/access.log
cat /etc/httpd/logs/error_log
cat /etc/httpd/logs/error.log
cat /var/log/apache2/access_log
cat /var/log/apache2/access.log
cat /var/log/apache2/error_log
cat /var/log/apache2/error.log
cat /var/log/apache/access_log
cat /var/log/apache/access.log
cat /var/log/auth.log
cat /var/log/chttp.log
cat /var/log/cups/error_log
cat /var/log/dpkg.log
cat /var/log/faillog
cat /var/log/httpd/access_log
cat /var/log/httpd/access.log
cat /var/log/httpd/error_log
cat /var/log/httpd/error.log
cat /var/log/lastlog
cat /var/log/lighttpd/access.log
cat /var/log/lighttpd/error.log
cat /var/log/lighttpd/lighttpd.access.log
cat /var/log/lighttpd/lighttpd.error.log
cat /var/log/messages
cat /var/log/secure
cat /var/log/syslog
cat /var/log/wtmp
cat /var/log/xferlog
cat /var/log/yum.log
cat /var/run/utmp
cat /var/webmin/miniserv.log
cat /var/www/logs/access_log
cat /var/www/logs/access.log
ls -alh /var/lib/dhcp3/
ls -alh /var/log/postgresql/
ls -alh /var/log/proftpd/
ls -alh /var/log/samba/
# auth.log, boot, btmp, daemon.log, debug, dmesg, kern.log, mail.info, mail.log, mail.warn, messages, syslog, udev, wtmp
``` 

**Is it possible to break out of "jail" shell** 
```bash	
python -c 'import pty;pty.spawn("/bin/bash")'
echo os.system('/bin/bash')
/bin/sh -i
vi -> :sh or :!UNIX_command
``` 

**Check which filesystems are mounted** 
```bash 
mount 
df -h
``` 

**Check if there are unmounted filesystems** 
```bash 
cat /etc/fstab 
``` 

**Finding world writeable directories**
```bash
find / -perm 777
```

**Find setuid files**
```bash
find / -perm +4000 -type f
```

**Find root setuid files**
```bash 
find / -perm +4000 -uid 0 -type f
``` 

**Additional File System Checks? Sticky bits, SUID & GUID**
```bash 
find / -perm -1000 -type d 2>/dev/null    # Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here
find / -perm -g=s -type f 2>/dev/null    # SGID (chmod 2000) - run as the  group, not the user who started it.
find / -perm -u=s -type f 2>/dev/null    # SUID (chmod 4000) - run as the  owner, not the user who started it.

find / -perm -g=s -o -perm -u=s -type f 2>/dev/null    # SGID or SUID
for i in `locate -r "bin$"`; do find $i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done    # Looks in 'common' places: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin and any other *bin, for SGID or SUID (Quicker search)

# find starting at root (/), SGID or SUID, not Symbolic links, only 3 folders deep, list with more detail and hide any errors (e.g. permission denied)
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null 
``` 

**Check common directories for write and execute permissions** 
```bash 
find / -writable -type d 2>/dev/null        # world-writeable folders
find / -perm -222 -type d 2>/dev/null      # world-writeable folders
find / -perm -o+w -type d 2>/dev/null    # world-writeable folders
find / -perm -o+x -type d 2>/dev/null    # world-executable folders
find / \( -perm -o+w -perm -o+x \) -type d 2>/dev/null   # world-writeable & executable folders
```

**Check for problem files (World Writeable / "Nobody" files)** 
```bash 
find / -xdev -type d \( -perm -0002 -a ! -perm -1000 \) -print   # world-writeable files
find /dir -xdev \( -nouser -o -nogroup \) -print   # Noowner files
```

Exploitation 
----------------------

##Attacking Vulnerable Kernel and SUID Applications

**Finding Exploit Code**
```bash
/pentest/exploits/exploitdb/searchsploit "kernel"  |grep -i "root"
cat /pentest/exploits/exploitdb/files.csv |grep -i privile
grep -i X.X /pentest/exploits/exploitdb/files.csv |grep -i local 
grep -i application /pentest/exploits/exploitdb/files.csv |grep -i local
``` 

**Check Development Environment on Target Hosts** 
```bash
find / -name perl*
find / -name python*
find / -name gcc* 
find / -name cc
``` 

**How can files be uploaded?**

```bash 
find / -name wget
find / -name nc*
find / -name netcat*
find / -name tftp* 
find / -name ftp 
``` 
One method to overcome library dependency problems is to compile the exploit statically locally and upload. The trade-off is that the file will be quite large. 


**Automated Checks**

unix-privesc-check
http://pentestmonkey.net/tools/audit/unix-privesc-check


Sources 
----------------------
All credits for the examples and explanation comes from the below sources.

Primary (vast majority of content on this page)
http://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation.html

Secondary
https://sites.google.com/site/mateustymbu/Pentest_Checklist.pdf?attredirects=0
http://insidetrust.blogspot.com/2011/04/quick-guide-to-linux-privilege.html
http://www.0daysecurity.com/penetration-testing/enumeration.html
http://www.microloft.co.uk/hacking/hacking3.htm



