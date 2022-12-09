---
layout: default
title: Flow
parent: Kioptrix
nav_order: 2
---

# Flow
- [Flow](#flow)
  - [1 Scanning \& Enummeration](#1-scanning--enummeration)
    - [1.1 NetDiscover](#11-netdiscover)
    - [1.2 NMap](#12-nmap)
    - [1.3 Nikto](#13-nikto)
    - [1.4 DirBuster](#14-dirbuster)
    - [1.5 Metaspliot](#15-metaspliot)
    - [1.6 smbclient](#16-smbclient)
    - [1.7 ssh](#17-ssh)
  - [2. Research](#2-research)
    - [2.1 google](#21-google)
    - [2.2 searchspliot](#22-searchspliot)

## 1 Scanning & Enummeration

### 1.1 NetDiscover
```console 
sudo netdiscover -r 10.0.2.0/24
```
[NetDiscover results](assets/NetDiscover.txt)

### 1.2 NMap
``` console
sudo nmap -T4 -p- -A 10.0.2.4
```
[nmap tcp scan](assets/nmap%20tcp.txt)  

```console
sudo nmap -T4 -sU 10.0.2.4 
```
[nmap upd scan](assets/nmap%20udp.txt)

### 1.3 Nikto
```console
nikto -h http://10.0.2.4
```
[nikto results](assets/nikto.txt)

### 1.4 DirBuster 
- Use GET requests only
- Go Faster
- wordlist: "/usr/share/wordlists/dirbuster/directory-list-2.3-small.txt"
  
![alt](assets/dirBuster.png)

### 1.5 Metaspliot
- search for "smb/smb_version"

``` console
msfconsole          // start metasploit
search smb_V        // search for a module to find smb versions
use 0               // use the found module
info                // get infos on how to use the module
set RHOST 10.0.2.4  // set the host (target)
run                 // run the module
```
![](assets/msf_01.png)
![](assets/msf_02.png)

### 1.6 smbclient

```console
smbclient -L \\\\10.0.2.4\\
```
-L : List services

![](assets/smb_1.png)

> 2 hares found!

```console
smbclient -L \\\\10.0.2.4\\ADMIN$
```

![](assets/smb_2.png)
```console
smbclient -L \\\\10.0.2.4\\IPC$
```
> Sucess!!!

```console
ls
```
![](assets/smb_3.png)
> Network access denied... damn

### 1.7 ssh

```console
ssh 10.0.2.4
```
```console
Unable to negotiate with 10.0.2.4 port 22: no matching key exchange method found. Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1

```
```console
ssh 10.0.2.4 -oKexAlgorithms=+diffie-hellman-group1-sha1
```
```console
Unable to negotiate with 10.0.2.4 port 22: no matching host key type found. Their offer: ssh-rsa,ssh-dss

```
![alt](assets/rJBwk0u.png)

> After fix

```console
The authenticity of host '10.0.2.4 (10.0.2.4)' can't be established.
RSA key fingerprint is SHA256:VDo/h/SG4A6H+WPH3LsQqw1jwjyseGYq9nLeRWPCY/A.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.2.4' (RSA) to the list of known hosts.
kali@10.0.2.4's password: 
```
> No banner with further infos sadly


## 2. Research

### 2.1 google
- `Samba 2.2.1a exploit`
- `mod_ssl/2.8.4 exploit`

### 2.2 searchspliot
```console
searchsploit Samba 2.2.1a 
```

```console
searchsploit mod_ssl 2.8.4
```
---
