### Tools we need.
- metasploit
- smbclient
[[Gaining Root with Metasploit]] - COMMAND TO RUN METASPLOIT
```
┌──(kali㉿kali)-[~/Desktop]
└─$ msfconsole

```
#MSFCONSOLENOTE : acronym find in the metasploit.
- EXPLOITATION -  exploit attack
- Auxiliary - Scanning/Enumeration - Port scanning and information gathering.
- Post Module - Post exploitation after we compromise the machine we can do Post attack.
- Payloads - Payload attack.
- Encoders - 
- Nops -
- Evasion - 
### Command to search for specific port (search (smb))
```
msf6 > search smb 
```
### After the command there will be a lot of number that will pop-up
```
msf6 > use auxiliary/scanner/smb/smb_version
```
### We can also check about the info of previous command by checking the version.
```
msf6 auxiliary(scanner/smb/smb_version) >  info                                                                             
                                                                                                                                     
       Name: SMB Version Detection                                                                                                             
     Module: auxiliary/scanner/smb/smb_version                                                                                                 
    License: Metasploit Framework License (BSD)                                                                                                
       Rank: Normal                                                                                                                                        
                                                                                                                                                           
Provided by:                                                                                                                                               
  hdm <x@hdm.io>                                                                                                                                           
  Spencer McIntyre                                                                                                                                         
  Christophe De La Fuente                                                                                                                                                                 
                                                                                                                                                                                          
Check supported:                                                                                                                                                                          
  No

Basic options:
  Name     Current Setting  Required  Description
  ----     ---------------  --------  -----------
  RHOSTS                    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
  THREADS  1                yes       The number of concurrent threads (max one per host)

Description:
  Fingerprint and display version information about SMB servers. Protocol
  information and host operating system (if available) will be reported.
  Host operating system detection requires the remote server to support
  version 1 of the SMB protocol. Compression and encryption capability
  negotiation is only present in version 3.1.1.

```

### The similar command without displaying the version of the smb version detection.

```
Module options (auxiliary/scanner/smb/smb_version):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOSTS                    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   THREADS  1                yes       The number of concurrent threads (max one per host)


View the full module info with the info, or info -d command.
```

### This is the most important part of the attacking.
**First we set the RHOST into our taget address.**
```
msf6 auxiliary(scanner/smb/smb_version) > set RHOST 192.168.189.130
RHOST => 192.168.189.130
```
![[Pasted image 20240211191136.png]]
**After that we can run the metasploit**

```
msf6 auxiliary(scanner/smb/smb_version) > run
```
![[Pasted image 20240211191229.png]]
#INFORMATIONDISCLOSURE - (Samba 2.2.1a)

#SMBClient
**Command for smbclient, the -L command stands for list and the four dash is a scape sequence.**
```
smbclient -L \\\\192.168.189.130\\

```
![[Pasted image 20240211192910.png]]
**After getting into the IPC$ server we use the help function to and then we did ls command to check the file but it seems we're denied so therefore this is the "DEAD END"**
![[Pasted image 20240211193126.png]]