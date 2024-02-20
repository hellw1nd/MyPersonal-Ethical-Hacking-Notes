[[Scanning with Nmap]], [[Enumerating SMB]]
### Scanning & Enumeration

1. Discovering network via netdiscover
**First we need to scan to our target ip address using netdiscover**

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# netdiscover -r 192.168.189.0/24

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-02-16 07:31 EST
Nmap scan report for 192.168.189.132
Host is up (0.00042s latency).
Not shown: 65527 closed tcp ports (conn-refused)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Ultimate 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: WIN-845Q99OO4PP; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows 7 Ultimate 7601 Service Pack 1 (Windows 7 Ultimate 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1
|   Computer name: WIN-845Q99OO4PP
|   NetBIOS computer name: WIN-845Q99OO4PP\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2024-02-16T07:32:58-05:00
|_clock-skew: mean: 1h40m00s, deviation: 2h53m12s, median: 0s
|_nbstat: NetBIOS name: WIN-845Q99OO4PP, NetBIOS user: <unknown>, NetBIOS MAC: 00:0c:29:45:2f:6d (VMware)
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2024-02-16T12:32:58
|_  start_date: 2024-02-16T09:41:20

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 104.96 seconds

```

![[Pasted image 20240216195210.png]]
**After scanning it we can test every possible ip address via Nmap scan**

2. Scanning the netdiscover ip address via nmap stealth scan 

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# nmap -T4 -p- -A 192.168.189.132
```

![[Pasted image 20240216201023.png]]

**We identify the port services running on this machine. then we will use the nmap vuln engine using this command.**

```
┌──(root㉿kali)-[/home/kali/Desktop]
└─# nmap --script=smb-vuln* 192.168.189.132
```

### Exploitation


