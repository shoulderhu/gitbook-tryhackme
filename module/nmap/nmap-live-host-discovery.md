---
description: https://tryhackme.com/room/nmap01
---

# Nmap Live Host Discovery

{% embed url="https://tryhackme.com/room/nmap01" %}
https://tryhackme.com/room/nmap01
{% endembed %}

## Task 2 Subnetworks

#### Send a packet with the following:

* From computer1
* To computer1 (to indicate it is broadcast)
* Packet Type: “ARP Request”
* Data: computer6 (because we are asking for computer6 MAC address using ARP Request)

#### How many devices can see the ARP Request?

{% hint style="success" %}
`4`
{% endhint %}

#### Did computer6 receive the ARP Request?

{% hint style="success" %}
`N`
{% endhint %}

#### Send a packet with the following:

* From computer4
* To computer4 (to indicate it is broadcast)
* Packet Type: “ARP Request”
* Data: computer6 (because we are asking for computer6 MAC address using ARP Request)

#### How many devices can see the ARP Request?

{% hint style="success" %}
`4`
{% endhint %}

#### Did computer6 reply to the ARP Request?

{% hint style="success" %}
`Y`
{% endhint %}

## Task 3 Enumerating Targets

If you want to check the list of hosts that Nmap will scan, you can use `nmap -sL TARGETS`. This option will give you a detailed list of the hosts that Nmap will scan without scanning them**.**

#### What is the first IP address Nmap would scan if you provided `10.10.12.13/29` as your target?

```bash
nmap -n -sL 10.10.12.13/29
```

![](<../../.gitbook/assets/Screenshot from 2022-04-12 04-42-32.png>)

{% hint style="success" %}
`10.10.12.8`
{% endhint %}

#### How many IP addresses will Nmap scan if you provide the following range `10.10.0-255.101-125`?&#x20;

```bash
nmap -n -sL 10.10.0-255.101-125
```

![](<../../.gitbook/assets/Screenshot from 2022-04-12 04-44-14.png>)

{% hint style="success" %}
`6400`
{% endhint %}

## Task 4 Discovering Live Hosts

#### Send a packet with the following:

* From computer1
* To computer3
* Packet Type: “Ping Request”

#### What is the type of packet that computer1 sent before the ping?

{% hint style="success" %}
`ARP Request`
{% endhint %}

#### What is the type of packet that computer1 received before being able to send the ping?

{% hint style="success" %}
`ARP Response`
{% endhint %}

#### How many computers responded to the ping request?

{% hint style="success" %}
`1`
{% endhint %}

#### Send a packet with the following:

* From computer2
* To computer5
* Packet Type: “Ping Request”

#### What is the name of the first device that responded to the first ARP Request?

{% hint style="success" %}
`router`
{% endhint %}

#### What is the name of the first device that responded to the second ARP Request?

{% hint style="success" %}
`computer5`
{% endhint %}

#### Send another Ping Request. Did it require new ARP Requests?

{% hint style="success" %}
`N`
{% endhint %}

## Task 5 Nmap Host Discovery Using ARP

1. When a _privileged_ user tries to scan targets on a local network (Ethernet), Nmap uses _ARP requests_.
2. When a _privileged_ user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
3. When an _unprivileged_ user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

#### We will be sending broadcast ARP Requests packets with the following options:

* From computer1
* To computer1 (to indicate it is broadcast)
* Packet Type: “ARP Request”
* Data: try all the possible eight devices (other than computer1) in the network: computer2, computer3, computer4, computer5, computer6, switch1, switch2, and router.

#### How many devices are you able to discover using ARP requests?

* computer2
* computer3
* router

{% hint style="success" %}
`3`
{% endhint %}

## Task 6 Nmap Host Discovery Using ICMP

#### What is the option required to tell Nmap to use ICMP Timestamp to discover live hosts?

{% hint style="success" %}
`-PP`
{% endhint %}

#### What is the option required to tell Nmap to use ICMP Address Mask to discover live hosts?

{% hint style="success" %}
`-PM`
{% endhint %}

#### What is the option required to tell Nmap to use ICMP Echo to discover life hosts?

{% hint style="success" %}
`-PE`
{% endhint %}

## Task 7 Nmap Host Discovery Using TCP and UDP

#### Which TCP ping scan does not require a privileged account?

{% hint style="success" %}
`TCP SYN Ping`
{% endhint %}

#### Which TCP ping scan requires a privileged account?

{% hint style="success" %}
`TCP ACK Ping`
{% endhint %}

#### What option do you need to add to Nmap to run a TCP SYN ping scan on the telnet port?

{% hint style="success" %}
`-PS23`
{% endhint %}

## Task 8 Using Reverse-DNS Lookup

By default, Nmap will look up online hosts; however, you can use the option `-R` to query the DNS server even for offline hosts. If you want to use a specific DNS server, you can add the `--dns-servers DNS_SERVER` option.

#### We want Nmap to issue a reverse DNS lookup for all the possibles hosts on a subnet, hoping to get some insights from the names. What option should we add?

{% hint style="success" %}
`-R`
{% endhint %}
