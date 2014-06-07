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

