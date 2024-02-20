[[Common Network Commands]], [[Navigating the File System]]
`we can use ifconfig to check our network ip address and we can use "ping" to check the data sent over network -c stands for counter and 1 stands for how many packet will be sent`
![[Common Network Commands]]
#### Storing ping address
Now with the help of >(output redirection) we can store our ip address with command line arguments ping in the text file 
- for example we can ping google.com -c 1 > test.txt
- we can look up anytime 

![[Pasted image 20240115193314.png]]
	[now we can scan this further with grep command for matching patterns](https://explainshell.com/explain?cmd=grep)
![[Pasted image 20240115194532.png]]
[scanning with cut](https://explainshell.com/explain?cmd=cut)
![[Pasted image 20240115195326.png]] Use for loop for scanning
#!/bin/bash

for ip in `seq 1 254`; do
ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
done

./ipsweep.sh 192.168.4

![[Pasted image 20240115202052.png]]