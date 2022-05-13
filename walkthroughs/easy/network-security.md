# Network Security

{% embed url="https://tryhackme.com/room/intronetworksecurity" %}
https://tryhackme.com/room/intronetworksecurity
{% endembed %}

## Task 1 Introduction

#### What type of firewall is Windows Defender Firewall?

{% hint style="success" %}
`Host Firewall`
{% endhint %}

## Task 2 Methodology

![](<../../.gitbook/assets/image (5) (1).png>)

#### During which step of the Cyber Kill Chain does the attacker gather information about the target?

{% hint style="success" %}
`Recon`
{% endhint %}

## Task 3 Practical Example of Network Security

```bash
nmap -n -sVC 10.10.2.213
```

![](<../../.gitbook/assets/Screenshot from 2022-04-27 06-25-11.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-27 06-25-20.png>)

#### What is the password in the `secret.txt` file?

```bash
lftp -u anonymous, 10.10.2.213
ftp > ls -lA
ftp > cat secret.txt 
```

![](<../../.gitbook/assets/Screenshot from 2022-04-27 06-28-45.png>)

{% hint style="success" %}
`ABC789xyz123`
{% endhint %}

#### What is the content of the `flag.txt` in the `/root` directory?

```bash
ssh root@10.10.2.213
```

{% hint style="success" %}
`THM{FTP_SERVER_OWNED}`
{% endhint %}

#### What is the content of the `flag.txt` in the `/home/librarian` directory?

```bash
cat /home/librarian/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-27 06-30-31.png>)

{% hint style="success" %}
`THM{LIBRARIAN_ACCOUNT_COMPROMISED}`
{% endhint %}
