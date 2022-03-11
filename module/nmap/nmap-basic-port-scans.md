---
description: https://tryhackme.com/room/nmap02
---

# Nmap Basic Port Scans

## Task 2 TCP and UDP Ports

#### Which service uses UDP port 53 by default?

{% hint style="success" %}
`DNS`
{% endhint %}

#### Which service uses TCP port 22 by default?

{% hint style="success" %}
`SSH`
{% endhint %}

#### How many port states does Nmap consider?

{% hint style="success" %}
`6`
{% endhint %}

#### Which port state is the most interesting to discover as a pentester?

{% hint style="success" %}
Open
{% endhint %}

## Task 3 TCP Flags

#### What 3 letters represent the Reset flag?

{% hint style="success" %}
`RST`
{% endhint %}

#### Which flag needs to be set when you initiate a TCP connection?

{% hint style="success" %}
`SYN`
{% endhint %}

## Task 4 TCP Connect Scan

#### Launch the VM. Open the AttackBox and execute `nmap -sT MACHINE_IP` via the terminal. A new service has been installed on this VM since our last scan. Which port number was closed in the scan above but is now open on this target VM?

```bash
nmap -n -sT 10.10.142.23
```

![nmap -n -sT 10.10.142.23](<../../.gitbook/assets/Screenshot from 2022-02-19 17-38-57.png>)

{% hint style="success" %}
`110`
{% endhint %}

#### What is Nmap’s guess about the newly installed service?

{% hint style="success" %}
`pop3`
{% endhint %}

## Task 5 TCP SYN Scan

#### Launch the VM. Some new server software has been installed since the last time we scanned it. On the AttackBox, use the terminal to execute `nmap -sS MACHINE_IP`. What is the new open port?

```bash
sudo nmap -n -sS 10.10.183.142
```

![sudo nmap -n -sS 10.10.183.142](<../../.gitbook/assets/Screenshot from 2022-02-19 17-46-33.png>)

{% hint style="success" %}
`6667`
{% endhint %}

#### What is Nmap’s guess of the service name?

{% hint style="success" %}
`irc`
{% endhint %}

## Task 6 UDP Scan

#### Launch the VM. On the AttackBox, use the terminal to execute `nmap -sU -F -v 10.10.172.205`. A new service has been installed since the last scan. What is the UDP port that is now open?

```bash
sudo nmap -n -sU -F 10.10.172.205 
```

![sudo nmap -n -sU -F 10.10.172.205](<../../.gitbook/assets/Screenshot from 2022-02-19 17-59-09.png>)

{% hint style="success" %}
`53`
{% endhint %}

#### What is the service name according to Nmap?

{% hint style="success" %}
`domain`
{% endhint %}

## Task 7 Fine-Tuning Scope and Performance

#### What is the option to scan all the TCP ports between 5000 and 5500?

{% hint style="success" %}
`-p5000-5500`
{% endhint %}

#### How can you ensure that Nmap will run at least 64 probes in parallel?

{% hint style="success" %}
`--min-parallelism 64`
{% endhint %}

#### What option would you add to make Nmap very slow and paranoid?

{% hint style="success" %}
`-T0`
{% endhint %}
