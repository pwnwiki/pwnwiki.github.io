# OS X Finding File Commands

Commands that find files on the filesystem and are usually executed from the context of the shell (`/bin/bash` or `/bin/sh`) prompt.

| Command  | Description / Importance |
| -------- | ------------------------ |
| `find /sbin /usr/sbin /opt /lib` &#96;`echo $PATH` &#124;`'sed s/:/ /g'`&#96;` -perm -4000` | Find SUID files. |
| `for user in $(cut -f1 -d: /etc/passwd); do echo $user; crontab -u $user -l; done` | Lists all the user crontab or scheduled tasks files. |
| `find /var/log -type f -exec ls -la {} \;` | Find all the log files in `/var/log/` |
| `ls -alhtr /Volumes` | Display the volumes mounted at `/Volumes` |
| `ls /Users/*/.ssh/*` | Discover SSH files (keys and such) located in each user's home drive. May require root permissions to view these files in other user's directories. |
| `locate tar` &#124; `grep [.]tar$` | Finds all files that have a `.tar` extension. Substitute other archive extensions (e.g., `.zip`, `.7z`, `.rar`) or other extensions such as `.sql` or `.conf`. |
| `locate settings` $#124; `grep [.]php$` | Find all files with the word settings in it and with a `.php` extension. |
| `locate .properties` $#124; `grep [.]properties` | Finds Java configuration files. | 

