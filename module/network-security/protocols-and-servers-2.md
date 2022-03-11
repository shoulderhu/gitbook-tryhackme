---
description: https://tryhackme.com/room/protocolsandservers2
---

# Protocols and Servers 2

## Task 2 Sniffing Attack

#### What do you need to add to the command `sudo tcpdump` to capture only Telnet traffic?

{% hint style="success" %}
port 23
{% endhint %}

#### What is the simplest display filter you can use with Wireshark to show only IMAP traffic?

{% hint style="success" %}
`imap`
{% endhint %}

## Task 3 Man-in-The-Middle (MiTM)

#### How many different interfaces does Ettercap offer?

![https://www.ettercap-project.org/about.html](<../../.gitbook/assets/Screenshot from 2022-02-21 10-29-37.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### In how many ways can you invoke Bettercap?

![https://www.bettercap.org/usage](<../../.gitbook/assets/Screenshot from 2022-02-21 10-33-42.png>)

{% hint style="success" %}
`3`
{% endhint %}

## Task 4 Transport Layer Security (TLS)

#### DNS can also be secured using TLS. What is the three-letter acronym of the DNS protocol that uses TLS?

{% hint style="success" %}
`DoT`
{% endhint %}

## Task 5 Secure Shell (SSH)

#### Use SSH to connect to 10.10.197.132 as `mark` with the password `XBtc49AB`. Using `uname -r`, find the Kernel release?

```bash
ssh mark@10.10.197.132
```

![ssh mark@10.10.197.132](<../../.gitbook/assets/Screenshot from 2022-02-21 10-08-41.png>)

{% hint style="success" %}
`5.4.0-84-generic`
{% endhint %}

#### Use SSH to download the file `book.txt` from the remote system. How many KBs did `scp` display as download size?

```bash
$ ls
$ exit
scp mark@10.10.197.132:/home/mark/book.txt .
```

![scp mark@10.10.197.132:/home/mark/book.txt .](<../../.gitbook/assets/Screenshot from 2022-02-21 10-10-27.png>)

{% hint style="success" %}
`415`
{% endhint %}

## Task 6 Password Attack

#### We learned that one of the email accounts is `lazie`. What is the password used to access the IMAP service on 10.10.124.168?

```bash
hydra -l lazie -P /usr/share/wordlists/rockyou.txt imap://10.10.124.168
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 21-14-22.png>)

{% hint style="success" %}
`butterfly`
{% endhint %}

