
# Linux Blind Files

In some cases during exploitation you as an attacker gain the ability to read arbitrary files. As an attacker you need go-to files that cover as many different OS versions as possible in order to either confirm exploitation or gather intelligence on the exploited system. For this we use a "blind file".

The files below are things to pull when all you can do is to blindly read. Examples of vulnerabilities or situations where this would be helpful might be: local file includes (LFI), directory traversals or remote file share instances like SMB, FTP, NFS or otherwise.

| File     | Description / Importance |
| -------- | ------------------------ |
| `/etc/issue` | A message or system identification to be printed before the login prompt. |
| `/etc/motd` | Message of the day banner content. Can contain information about the system owners or use of the system. | 
| `/etc/passwd` | List of account names, groups, home directory, and shell (should be globally readable). |
| `/etc/resolv.conf` | Contains the current name servers (DNS) for the system. This is a globally readable file that is less likely to trigger IDS alerts than `/etc/passwd`. |
| `/etc/shadow` | List of all user's password hashes (requires root). |
| `/home/[USERNAME]/.bash_history`<br>`~/.bash_history`<br>`/root/.bash_history` | Shell history for [USERNAME], the current user or root respectively. This file can contain passwords and other sensitive commands and content. |