# Protocols and Servers

{% embed url="https://tryhackme.com/room/protocolsandservers" %}
https://tryhackme.com/room/protocolsandservers
{% endembed %}

## Task 2 Telnet

#### To which port will the `telnet` command with the default parameters try to connect?

{% hint style="success" %}
`23`
{% endhint %}

## Task 3 Hypertext Transfer Protocol (HTTP)

#### Launch the attached VM. From the AttackBox terminal, connect using Telnet to `10.10.100.207 80` and retrieve the file `flag.thm`. What does it contain?

```bash
curl http://10.10.100.207/flag.thm
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 06-28-29.png>)

{% hint style="success" %}
`THM{e3eb0a1df437f3f97a64aca5952c8ea0}`
{% endhint %}

## Task 4 File Transfer Protocol (FTP)

A command like `STAT` can provide some added information. The `SYST` command shows the System Type of the target (UNIX in this case). `PASV` switches the mode to passive.

The command `TYPE A` switches the file transfer mode to ASCII, while `TYPE I` switches the file transfer mode to binary.

#### Using an FTP client, connect to the VM and try to recover the flag file. What is the flag?

* Username: frank
* Password: D2xc9CgD

```bash
lftp frank,D2xc9CgD 10.10.100.207
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 06-36-01.png>)

{% hint style="success" %}
`THM{364db6ad0e3ddfe7bf0b1870fb06fbdf}`
{% endhint %}

## Task 5 Simple Mail Transfer Protocol (SMTP)

#### Using the AttackBox terminal, connect to the SMTP port of the target VM. What is the flag that you can get?

```bash
nc 10.10.100.207 25
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 06-58-12.png>)

{% hint style="success" %}
`THM{5b31ddfc0c11d81eba776e983c35e9b5}`
{% endhint %}

## Task 6 Post Office Protocol 3 (POP3)

Using the command `STAT`, we get the reply `+OK 1 179`; based on [RFC 1939](https://datatracker.ietf.org/doc/html/rfc1939), a positive response to `STAT` has the format `+OK nn mm`, where _nn_ is the number of email messages in the inbox, and _mm_ is the size of the inbox in octets (byte). The command `LIST` provided a list of new messages on the server, and `RETR 1` retrieved the first message in the list.

#### Connect to the VM (`10.10.100.207`) at the POP3 port. Authenticate using the username `frank` and password `D2xc9CgD`. What is the response you get to `STAT`?

```bash
nc 10.10.100.207 110
> USER frank
> PASS D2xc9CgD
> STAT
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 07-05-37.png>)

{% hint style="success" %}
`+OK 0 0`
{% endhint %}

#### How many email messages are available to download via IMAP on `10.10.100.207`?

{% hint style="success" %}
`0`
{% endhint %}

## Task 7 Internet Message Access Protocol (IMAP)

IMAP makes it possible to keep your email **synchronized** across multiple devices (and mail clients). IMAP requires each command to be preceded by a random string to be able to track the reply. So we added `c1`, then `c2`, and so on.

```bash
nc 10.10.100.207 143
> c1 LOGIN frank D2xc9CgD
> c2 LIST "" "*"
> c3 EXAMINE INBOX
> c4 LOGOUT
```

#### What is the default port used by IMAP?

{% hint style="success" %}
`143`
{% endhint %}
