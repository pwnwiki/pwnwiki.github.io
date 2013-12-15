
# OS X Blind Files

In some cases during exploitation you as an attacker gain the ability to read arbitrary files. As an attacker you need go-to files that cover as many different OS versions as possible in order to either confirm exploitation or gather intelligence on the exploited system. For this we use a "blind file".

The files below are things to pull when all you can do is to blindly read. Examples of vulnerabilities or situations where this would be helpful might be: local file includes (LFI), directory traversals or remote file share instances like SMB, FTP, NFS or otherwise. Files that will have the same name across networks, Windows domains, and systems are noted below. 

| File     | Description / Importance |
| -------- | ------------------------ |
| /etc/fstab | Displays the file systems and mounted permissions of file systems attached to the host. |
| /etc/group | User group assignments. Displays user and group names and which user is a member of which group. |
| /etc/hosts | Manually-entered IP to hostname translation. |
| /etc/master.passwd | **Must be root to read.** Contains users, their UID, primary group, and default shell. |
| /etc/passwd | Contains users, their UID, primary group, and default shell. |
| /etc/resolv.conf | Configuration file for DNS server entries. |
| /etc/sudoers | Configuration file for the `sudo` command. May tell you if some users can elevate privileges with or without a password using the `sudo` command. |
| /etc/sysctl.conf | Contains a list of sysctl variable assignments that is read at system startup by rc early on in the boot sequence. [^1](http://www.openbsd.org/cgi-bin/man.cgi?query=sysctl.conf&sektion=5) |