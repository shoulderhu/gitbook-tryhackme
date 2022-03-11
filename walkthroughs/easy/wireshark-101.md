---
description: https://tryhackme.com/room/wireshark
---

# Wireshark 101

## Task 7 ARP Traffic

#### What is the Opcode for Packet 6?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-11-34.png>)

{% hint style="success" %}
`request (1)`
{% endhint %}

#### What is the source MAC Address of Packet 19?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-13-24.png>)

{% hint style="success" %}
`80:fb:06:f0:45:d7`
{% endhint %}

#### What 4 packets are Reply packets?

```
arp.opcode == 2
```

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-14-38.png>)

{% hint style="success" %}
`76,400,459,520`
{% endhint %}

#### What IP Address is at 80:fb:06:f0:45:d7?

{% hint style="success" %}
`10.251.23.1`
{% endhint %}

## Task 8 ICMP Traffic

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-27-45.png>)

#### What is the type for packet 4?

{% hint style="success" %}
`8`
{% endhint %}

#### What is the type for packet 5?

{% hint style="success" %}
`0`
{% endhint %}

#### What is the timestamp for packet 12, only including month day and year?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-29-24.png>)

#### note: Wireshark bases it’s time off of your devices time zone, if your answer is wrong try one day more or less.

{% hint style="success" %}
`May 30, 2013`
{% endhint %}

#### What is the full data string for packet 18?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-30-10.png>)

{% hint style="success" %}
`08090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f202122232425262728292a2b2c2d2e2f3031323334353637`
{% endhint %}

## Task 10 DNS Traffic

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-40-50.png>)

#### What is being queried in packet 1?

{% hint style="success" %}
`8.8.8.8.in-addr.arpa`
{% endhint %}

#### What site is being queried in packet 26?

{% hint style="success" %}
`www.wireshark.org`
{% endhint %}

#### What is the Transaction ID for packet 26?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-42-28.png>)

{% hint style="success" %}
`0x2c58`
{% endhint %}

## Task 11 HTTP Traffic

#### What percent of packets originate from Domain Name System?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-49-45.png>)

{% hint style="success" %}
`4.7`
{% endhint %}

#### What endpoint ends in .237?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-50-42.png>)

{% hint style="success" %}
`145.254.160.237`
{% endhint %}

#### What is the user-agent listed in packet 4?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-52-24.png>)

{% hint style="success" %}
`Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.6) Gecko/20040113`
{% endhint %}

#### Looking at the data stream what is the full request URI from packet 18?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-55-20.png>)

{% hint style="success" %}
`https://pagead2.googlesyndication.com [truncated]GET /pagead/ads?client=ca-pub-2309191948673629&random=1084443430285&lmt=1082467020&format=468x60_as&output=html&url=http%3A%2F%2Fwww.ethereal.com%2Fdownload.html&color_bg=FFFFFF&color_text=333333&color_link=000000&color_url=66`
{% endhint %}

#### What domain name was requested from packet 38?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 22-57-45.png>)

![tcp.stream == 0 && http](<../../.gitbook/assets/Screenshot from 2022-03-08 22-58-42.png>)

{% hint style="success" %}
`www.ethereal.com`
{% endhint %}

#### Looking at the data stream what is the full request URI from packet 38?

{% hint style="success" %}
`http://www.ethereal.com/download.html`
{% endhint %}

## Task 12 HTTPS Traffic

#### Looking at the data stream what is the full request URI for packet 31?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 23-10-13.png>)

{% hint style="success" %}
`https://localhost/icons/apache_pb.png`
{% endhint %}

#### Looking at the data stream what is the full request URI for packet 50?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 23-10-57.png>)

{% hint style="success" %}
`https://localhost/icons/back.gif`
{% endhint %}

#### What is the User-Agent listed in packet 50?

{% hint style="success" %}
`Mozilla/5.0 (X11; U; Linux i686; fr; rv:1.8.0.2) Gecko/20060308 Firefox/1.5.0.2`
{% endhint %}
