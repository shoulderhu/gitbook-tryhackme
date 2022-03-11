---
description: A tutorial room exploring CVE-2019-18634 in the Unix Sudo Program
---

# Sudo Buffer Overflow

## :ocean: Buffer Overflow

* `pwfeedback` option enabled

### #1 **Use the pre-compiled exploit in the VM to get a root shell.**

```bash
sshpass -p tryhackme ssh -p 4444 tryhackme@10.10.220.164
./exploit
```

### #2 **What's the flag in /root/root.txt?**

```bash
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 10-02-13.png>)

## :link: Support Material

{% embed url="https://github.com/saleemrashid/sudo-cve-2019-18634" %}

