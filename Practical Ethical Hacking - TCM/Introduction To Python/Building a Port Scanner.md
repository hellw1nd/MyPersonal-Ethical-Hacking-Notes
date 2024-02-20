[[Sockets]], [[Importing]], [[Reading and Writing Files]], [[Classes and Objects]]

[Read More About Sys Module](https://docs.python.org/3/library/sys.html) and [Socket](https://docs.python.org/3/library/socket.html)
### Python Code 
```python
#!/bin/python3

import sys
import socket
from datetime import datetime

#DEFINE THE TARGET

if len(sys.argv) == 2:
	target = socket.gethostbyname(sys.argv[1]) #this will translate the hostname into ipv4
else:
	print("Invalid amount of arguments. ")
	print("Syntax: python3 scanner.py <ip>")

#Add a pretty banner
print("-" * 50)
print("Scanning target "+target)
print("Time Started: "+str(datetime.now()))
print("-" * 50)


try: 
	for port in range(50,85):
		s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
		socket.setdefaulttimeout(1)
		result = s.connect_ex((target,port))
		if result == 0:
			print(f"Port {port} is open")
		s.close()
except KeyboardInterrupt:
	print("\nExiting Program.")
	sys.exit()

except socket.gaierror:
	print("Hostname could not be resolved.")
	sys.exit()
	
except socket.error:
	print("Could not connect to the server. ")
	sys.exit()
	

```
![[Pasted image 20240203191734.png]]

