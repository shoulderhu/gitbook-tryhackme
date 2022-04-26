---
description: A tutorial room exploring CVE-2019-18634 in the Unix Sudo Program
---

# Sudo Buffer Overflow

It has been patched, but affects versions of sudo earlier than **1.8.26**.

* `pwfeedback` option enabled

![](<../../.gitbook/assets/image (5) (1) (1) (1).png>)

## Task 2 Buffer Overflow

#### **Use the pre-compiled exploit in the VM to get a root shell.**

```bash
sshpass -p tryhackme ssh -p 4444 tryhackme@10.10.220.164
./exploit
```

#### **What's the flag in /root/root.txt?**

```bash
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 10-02-13.png>)

## Support Material

{% embed url="https://github.com/saleemrashid/sudo-cve-2019-18634" %}
