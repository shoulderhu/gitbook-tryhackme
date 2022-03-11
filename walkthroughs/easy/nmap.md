---
description: https://tryhackme.com/room/furthernmap
---

# Nmap

## Task 2 Introduction

#### What networking constructs are used to direct traffic to the right application on a server?

{% hint style="success" %}
`Ports`
{% endhint %}

#### How many of these are available on any network-enabled computer?

{% hint style="success" %}
`65535`
{% endhint %}

#### How many of these are considered "well-known"?

{% hint style="success" %}
`1024`
{% endhint %}

## Task 3 Nmap Switches

#### What is the first switch listed in the help menu for a "Syn Scan"?

{% hint style="success" %}
`-sS`
{% endhint %}

#### Which switch would you use for a "UDP scan"?

{% hint style="success" %}
`-sU`
{% endhint %}

#### If you wanted to detect which operating system the target is running on, which switch would you use?

{% hint style="success" %}
`-O`
{% endhint %}

#### Nmap provides a switch to detect the version of the services running on the target. What is this switch?

{% hint style="success" %}
`-sV`
{% endhint %}

#### The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?

{% hint style="success" %}
`-v`
{% endhint %}

#### Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?

{% hint style="success" %}
`-vv`
{% endhint %}

#### We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients.

#### What switch would you use to save the nmap results in three major formats?

{% hint style="success" %}
`-oA`
{% endhint %}

#### What switch would you use to save the nmap results in a "normal" format?

{% hint style="success" %}
`-oN`
{% endhint %}

#### A very useful output format: how would you save results in a "grepable" format?

{% hint style="success" %}
`-oG`
{% endhint %}

#### Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning.&#x20;

#### How would you activate this setting?

{% hint style="success" %}
`-A`
{% endhint %}

#### Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors!

#### How would you set the timing template to level 5?

{% hint style="success" %}
`-T5`
{% endhint %}

#### We can also choose which port(s) to scan.

#### How would you tell nmap to only scan port 80?

{% hint style="success" %}
`-p 80`
{% endhint %}

#### How would you tell nmap to scan ports 1000-1500?

{% hint style="success" %}
`-p 1000-1500`
{% endhint %}

#### A very useful option that should not be ignored:

#### How would you tell nmap to scan _all_ ports?

{% hint style="success" %}
`-p-`
{% endhint %}

#### How would you activate a script from the nmap scripting library?

{% hint style="success" %}
`--script`
{% endhint %}

#### How would you activate all of the scripts in the "vuln" category?

{% hint style="success" %}
\--script=vuln
{% endhint %}

## Task 5 TCP Connect Scans

#### Which RFC defines the appropriate behaviour for the TCP protocol?

{% hint style="success" %}
`RFC 793`
{% endhint %}

#### If a port is closed, which flag should the server send back to indicate this?

{% hint style="success" %}
`RST`
{% endhint %}

## Task 6 SYN Scans

#### There are two other names for a SYN scan, what are they?

{% hint style="success" %}
`Half-open, Stealth`
{% endhint %}

#### Can Nmap use a SYN scan without Sudo permissions?

{% hint style="success" %}
`N`
{% endhint %}

## Task 7 UDP Scans

#### If a UDP port doesn't respond to an Nmap scan, what will it be marked as?

{% hint style="success" %}
`open|filtered`
{% endhint %}

#### When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so?

{% hint style="success" %}
`ICMP`
{% endhint %}

## Task 8 NULL, FIN and Xmas

#### Which of the three shown scan types uses the URG flag?

{% hint style="success" %}
`Xmas`
{% endhint %}

#### Why are NULL, FIN and Xmas scans generally used?

{% hint style="success" %}
`firewall evasion`
{% endhint %}

#### Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port?

{% hint style="success" %}
`Microsoft Windows`
{% endhint %}

## Task 9 ICMP Network Scanning

#### How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap?

{% hint style="success" %}
`nmap -sn 172.16.0.0/16`
{% endhint %}

## Task 10 Overview

#### What language are NSE scripts written in?

{% hint style="success" %}
`Lua`
{% endhint %}

#### Which category of scripts would be a _very_ bad idea to run in a production environment?

{% hint style="success" %}
`intrusive`
{% endhint %}

## Task 11 Working with the NSE

#### What optional argument can the `ftp-anon.nse` script take?

![https://nmap.org/nsedoc/scripts/ftp-anon.html](<../../.gitbook/assets/Screenshot from 2022-02-19 15-32-46.png>)

{% hint style="success" %}
`maxlist`
{% endhint %}

## Task 12 Searching for Scripts

#### Search for "smb" scripts in the `/usr/share/nmap/scripts/` directory using either of the demonstrated methods. What is the filename of the script which determines the underlying OS of the SMB server?

```bash
cat /usr/share/nmap/scripts/script.db | grep smb | grep os
nmap --script-help=smb-os-discovery
```

![cat /usr/share/nmap/scripts/script.db | grep smb | grep os](<../../.gitbook/assets/Screenshot from 2022-02-19 15-52-10.png>)

![nmap --script-help=smb-os-discovery](<../../.gitbook/assets/Screenshot from 2022-02-19 15-55-05.png>)

{% hint style="success" %}
`smb-os-discovery.nse`
{% endhint %}

#### Read through this script. What does it depend on?

```bash
cat /usr/share/nmap/scripts/smb-os-discovery.nse | sed -n 81p
# dependencies = {"smb-brute"}
```

{% hint style="success" %}
`smb-brute`
{% endhint %}

## Task 13 Firewall Evasion

#### Which simple protocol is often blocked, requiring the use of the `-Pn` switch?

{% hint style="success" %}
`ICMP`
{% endhint %}

#### Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?

```bash
nmap -h | grep data
```

{% hint style="success" %}
`--data-length`
{% endhint %}

## Task 14 Practical

#### Does the target respond to ICMP (ping) requests?

```bash
ping -c4 10.10.82.137
```

![ping -c4 10.10.82.137](<../../.gitbook/assets/Screenshot from 2022-02-19 16-18-27.png>)

{% hint style="success" %}
`N`
{% endhint %}

#### Perform an Xmas scan on the first 999 ports of the target -- how many ports are shown to be open or filtered?

```bash
sudo nmap -n -Pn -sX -p -999 10.10.82.137
```

![sudo nmap -n -Pn -sX -p -999 10.10.82.137](<../../.gitbook/assets/Screenshot from 2022-02-19 16-29-06.png>)

{% hint style="success" %}
`999`
{% endhint %}

#### There is a reason given for this -- what is it?

{% hint style="success" %}
`no response`
{% endhint %}

#### Perform a TCP SYN scan on the first 5000 ports of the target -- how many ports are shown to be open?

```bash
sudo nmap -n -Pn -sS -p -5000 10.10.82.137
```

![sudo nmap -n -Pn -sS -p -5000 10.10.82.137](<../../.gitbook/assets/Screenshot from 2022-02-19 16-32-11.png>)

{% hint style="success" %}
`5`
{% endhint %}

#### Open Wireshark and perform a TCP Connect scan against port 80 on the target, monitoring the results.

```bash
nmap -n -Pn -sT -p80 10.10.82.137
```

![nmap -n -Pn -sT -p80 10.10.82.137](<../../.gitbook/assets/Screenshot from 2022-02-19 16-37-31.png>)

![Wireshark](<../../.gitbook/assets/Screenshot from 2022-02-19 16-37-25.png>)

#### Deploy the `ftp-anon` script against the box. Can Nmap login successfully to the FTP server on port 21?

```bash
nmap -n -Pn -p21 --script=ftp-anon 10.10.82.137
ftp anonymous@10.10.82.137
```

![nmap -n -Pn -p21 --script=ftp-anon 10.10.82.137](<../../.gitbook/assets/Screenshot from 2022-02-19 16-41-20.png>)

![ftp anonymous@10.10.82.137](<../../.gitbook/assets/Screenshot from 2022-02-19 16-42-41.png>)

{% hint style="success" %}
`Y`
{% endhint %}
