```
ssh version
22/tcp    open  ssh         OpenSSH 2.9p2 (protocol 1.99)
```
![[Pasted image 20240211193447.png]]

#### SSH Command for fingerprinting
```
ssh (target) -OkexAlgorithms+=diffie-hellman-group1-sha1 -c aes128-cbc
```

![[Pasted image 20240211194110.png]]