# Sudo
Don't forget to check sudo to see if you can execute any commands with any privilege besides your user level
**Show which commands sudo allows you to run**
`sudo -l`

# Find
The following commands are helpful when looking to exploit local applications for privilege escalation
**Finding world writeable directories**
`find / -perm 777`

**Find setuid files**
`find / -perm +4000 -type f`

**Find root setuid files**
`find / -perm +4000 -uid 0 -type f`
