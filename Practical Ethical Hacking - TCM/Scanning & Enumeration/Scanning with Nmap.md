[[Common Network Commands]], [[Five Stage Of Ethical Hacking]] - The 2nd one.
![[Pasted image 20240209194726.png]]
So we're using an old vm machine name kioptrix, it's so old that we can't use ifconfig so what we did was use #Ping 8.8.8.8 - the number it's just a basic dns host but the real motive here was to check what's the ip address look at the (ping from (ip))

**TOOLS WE USE TO SCAN FOR NETWORK**
### ARP-SCAN 
always run in super user(su) to use this tool.
[Manual Page of ARP-SCAN](https://linux.die.net/man/1/arp-scan)
![[Pasted image 20240209195126.png]]
So there are 4 different IP reflected on arp-scan -l it means list we already saw what IP does kioptrix VM run on.

### netdiscover
**Help page of the netdiscover**
![[Pasted image 20240209200005.png]]
(Scanning using net-discover)
```
┌──(root㉿kali)-[/home/kali]
└─# netdiscover -r 192.168.189.0/24
```
The Result will be this. looks family right? bwhahaha there 
![[Pasted image 20240209200504.png]]

After trying different network scanning we can confirm that this ip address belongs to our target (which is necessary.)

### SYN ACK
This is one of the most important network lesson 
[Read more about SYN ACK](https://www.guru99.com/tcp-3-way-handshake.html)

### NMAP (Network Mapper)
[Manual Page of Nmap](https://linux.die.net/man/1/nmap)
![[Pasted image 20240209204933.png]]
#-Tn Represent for **paranoid** (**0**), **sneaky** (**1**), **polite** (**2**), **normal** (**3**), **aggressive** (**4**), and **insane** (**5**). we can choose what number we want to use for example -T1 for sneaky.

Personal Opinion: -T4 are the most common.

#-p- (**-p**) _port ranges_ (Only scan specified ports) .

This option specifies which ports you want to scan and overrides the default. Individual port numbers are OK, as are ranges separated by a hyphen (e.g. 1-1023). The beginning and/or end values of a range may be omitted, causing Nmap to use 1 and 65535, respectively. So you can specify **-p-** to scan ports from 1 through 65535. Scanning port zero. is allowed if you specify it explicitly. For IP protocol scanning (**-sO**), this option specifies the protocol numbers you wish to scan for (0-255).

When scanning both TCP and UDP ports, you can specify a particular protocol by preceding the port numbers by T: or U:. The qualifier lasts until you specify another qualifier. For example, the argument **-p U:53,111,137,T:21-25,80,139,8080** would scan UDP ports 53, 111,and 137, as well as the listed TCP ports. Note that to scan both UDP and TCP, you have to specify **-sU** and at least one TCP scan type (such as **-sS**, **-sF**, or **-sT**). If no protocol qualifier is given, the port numbers are added to all protocol lists. Ports can also be specified by name according to what the port is referred to in the nmap-services. You can even use the wildcards * and ? with the names. For example, to scan FTP and all ports whose names begin with "http", use **-p ftp,http***. Be careful about shell expansions and quote the argument to **-p** if unsure.

Ranges of ports can be surrounded by square brackets to indicate ports inside that range that appear in nmap-services. For example, the following will scan all ports in nmap-services equal to or below 1024: **-p [-1024]**. Be careful with shell expansions and quote the argument to **-p** if unsure.

#-A **-A** (Aggressive scan options) .

This option enables additional advanced and aggressive options. I haven't decided exactly which it stands for yet. Presently this enables OS detection (**-O**), version scanning (**-sV**), script scanning (**-sC**) and traceroute (**--traceroute**).. More features may be added in the future. The point is to enable a comprehensive set of scan options without people having to remember a large set of flags. However, because script scanning with the default set is considered intrusive, you should not use **-A** against target networks without permission. This option only enables features, and not timing options (such as **-T4**) or verbosity options (**-v**) that you might want as well.

```
┌──(root㉿kali)-[/home/kali]
└─# nmap -T4 -p- -A 192.168.189.130
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-02-10 05:21 EST
Nmap scan report for 192.168.189.130
Host is up (0.00090s latency).
Not shown: 65529 closed tcp ports (reset)
PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         OpenSSH 2.9p2 (protocol 1.99)
| ssh-hostkey: 
|   1024 b8:74:6c:db:fd:8b:e6:66:e9:2a:2b:df:5e:6f:64:86 (RSA1)
|   1024 8f:8e:5b:81:ed:21:ab:c1:80:e1:57:a3:3c:85:c4:71 (DSA)
|_  1024 ed:4e:a9:4a:06:14:ff:15:14:ce:da:3a:80:db:e2:81 (RSA)
|_sshv1: Server supports SSHv1
80/tcp    open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: Test Page for the Apache Web Server on Red Hat Linux
111/tcp   open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100024  1          32768/tcp   status
|_  100024  1          32768/udp   status
139/tcp   open  netbios-ssn Samba smbd (workgroup: MYGROUP)
443/tcp   open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_ssl-date: 2024-02-10T23:22:05+00:00; +13h00m05s from scanner time.
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2009-09-26T09:32:06
|_Not valid after:  2010-09-26T09:32:06
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_RC4_64_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|_    SSL2_DES_64_CBC_WITH_MD5
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: 400 Bad Request
32768/tcp open  status      1 (RPC #100024)
MAC Address: 00:0C:29:65:14:06 (VMware)
Device type: general purpose
Running: Linux 2.4.X
OS CPE: cpe:/o:linux:linux_kernel:2.4
OS details: Linux 2.4.9 - 2.4.18 (likely embedded)
Network Distance: 1 hop

Host script results:
|_smb2-time: Protocol negotiation failed (SMB2)
|_clock-skew: 13h00m04s
|_nbstat: NetBIOS name: KIOPTRIX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)

TRACEROUTE
HOP RTT     ADDRESS
1   0.90 ms 192.168.189.130

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.87 seconds
```

FINAL NOTES: 
Familiarize the nmap -T4 -p- -A (IP) commands
and also the -p- scan for all the open tcp of ip address you can also set the limit of the port like -p1-1000 it means scan the best 1000 open ports from 1 to 1000.