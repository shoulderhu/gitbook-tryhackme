---
description: https://tryhackme.com/room/redteamnetsec
---

# Network Security Solutions

## Task 1 Introduction

#### What does an IPS stand for?

{% hint style="success" %}
`Intrusion Prevention System`
{% endhint %}

#### What do you call a system that can detect malicious activity but not stop it?

{% hint style="success" %}
`Intrusion Detection System`
{% endhint %}

## Task 2 IDS Engine Types

#### What kind of IDS engine has a database of all known malicious packets’ contents?

{% hint style="success" %}
`Signature-based`
{% endhint %}

#### What kind of IDS engine needs to learn what normal traffic looks like instead of malicious traffic?

{% hint style="success" %}
`Anomaly-based`
{% endhint %}

#### What kind of IDS engine needs to be updated constantly as new malicious packets and activities are discovered?

{% hint style="success" %}
`Signature-based`
{% endhint %}

## Task 3 IDS/IPS Rule Triggering

#### In the attached file, the logs show that a specific IP address has been detected scanning our system of IP address `10.10.112.168`. What is the IP address running the port scan?

```bash
tar xzvf 1010112168.tar.gz
grep -r '10.10.112.168' 10.10.112.168
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 20-48-40.png>)

{% hint style="success" %}
`10.14.17.226`
{% endhint %}



## Task 4 Evasion via Protocol Manipulation

#### We use the following Nmap command, `nmap -sU -F 10.10.152.8`, to launch a UDP scan against our target. What is the option we need to add to set the source port to 161?

{% hint style="success" %}
`-g 161`
{% endhint %}

#### The target allows Telnet traffic. Using `ncat`, how do we set a listener on the Telnet port?

{% hint style="success" %}
`ncat -lvnp 23`
{% endhint %}

#### We are scanning our target using `nmap -sS -F 10.10.152.8`. We want to fragment the IP packets used in our Nmap scan so that the data size does not exceed 16 bytes. What is the option that we need to add?

{% hint style="success" %}
`-ff`
{% endhint %}

#### Consider the following three types of Nmap scans:

* `-sX` for Xmas Scan
* `-sF` for FIN Scan
* `-sN`for Null Scan

#### Which of the above three arguments would return meaningful results when scanning `10.10.152.8`?

```bash
sudo nmap -n -sF 10.10.152.8
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 21-23-22.png>)

{% hint style="success" %}
`-sF`
{% endhint %}

#### What is the option in `hping3` to set a custom TCP window size?

```bash
hping3 -h | grep win
```

![](<../../.gitbook/assets/Screenshot from 2022-03-16 21-21-18.png>)

{% hint style="success" %}
`-w`
{% endhint %}

## Task 5 Evasion via Payload Manipulation

#### Using `base64` encoding, what is the transformation of `cat /etc/passwd`?

```bash
echo 'cat /etc/passwd' | base64                          
```

![](<../../.gitbook/assets/Screenshot from 2022-03-17 06-48-07.png>)

{% hint style="success" %}
`Y2F0IC9ldGMvcGFzc3dkCg==`
{% endhint %}

#### The `base32` encoding of a particular string is `NZRWC5BAFVWCAOBQHAYAU===`. What is the original string?

```bash
echo 'NZRWC5BAFVWCAOBQHAYAU===' | base32 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-03-17 06-49-57.png>)

{% hint style="success" %}
`ncat -l 8080`
{% endhint %}

#### Using the provided `openssl` command above. You created a certificate, which we gave the extension `.crt`, and a private key, which we gave the extension `.key`. What is the first line in the certificate file?

```bash
openssl req -x509 -newkey rsa:4096 -days 365 \
            -subj '/CN=www.redteam.thm/O=Red Team THM/C=UK' -nodes \
            -keyout thm-reverse.key -out thm-reverse.crt
head -n1 thm-reverse.crt
tail -n1 thm-reverse.key
```

![](<../../.gitbook/assets/Screenshot from 2022-03-17 06-52-05.png>)

{% hint style="success" %}
`-----BEGIN CERTIFICATE-----`
{% endhint %}

#### What is the last line in the private key file?

{% hint style="success" %}
`-----END PRIVATE KEY-----`
{% endhint %}

#### On the attached machine from the previous task, browse to `http://10.10.106.14:8080`, where you can write your Linux commands. Note that no output will be returned. A command like `ncat -lvnp 1234 -e /bin/bash` will create a bind shell that you can connect to it from the AttackBox using `ncat 10.10.106.14 1234`; however, some IPS is filtering out the command we are submitting on the form. Using one of the techniques mentioned in this task, try to adapt the command typed in the form to run properly. Once you connect to the bind shell using `ncat 10.10.106.14 1234`, find the user’s name.

![](<../../.gitbook/assets/Screenshot from 2022-03-17 07-02-31.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-17 07-02-42.png>)

{% hint style="success" %}
`redteamnetsec`
{% endhint %}

## Task 6 Evasion via Route Manipulation

#### Protocols used in proxy servers can be HTTP, HTTPS, SOCKS4, and SOCKS5. Which protocols are currently supported by Nmap?

{% hint style="success" %}
`HTTP SOCKS4`
{% endhint %}







