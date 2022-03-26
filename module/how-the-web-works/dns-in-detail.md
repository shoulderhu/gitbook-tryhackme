---
description: Learn how DNS works and how it helps you access internet services.
---

# DNS in detail

{% embed url="https://tryhackme.com/room/dnsindetail" %}
https://tryhackme.com/room/dnsindetail
{% endembed %}

## Task 1 What is DNS?

#### What does DNS stand for?

{% hint style="success" %}
Domain Name System
{% endhint %}

## Task 2 Domain Hierarchy

#### What is the maximum length of a subdomain?

{% hint style="success" %}
`63`
{% endhint %}

#### Which of the following characters cannot be used in a subdomain ( 3 b \_ - )?

{% hint style="success" %}
`_`
{% endhint %}

#### What is the maximum length of a domain name?

{% hint style="success" %}
`253`
{% endhint %}

#### What type of TLD is .co.uk?

* Generic Top Level Domain (gTLD)
* Country Code Top Level Domain (ccTLD)

{% hint style="success" %}
`ccTLD`
{% endhint %}

## Task 3 Record Types

#### What type of record would be used to advise where to send email?

{% hint style="success" %}
`MX`
{% endhint %}

#### What type of record handles IPv6 addresses?

{% hint style="success" %}
`AAAA`
{% endhint %}

## Task 4 Making A Request

#### What field specifies how long a DNS record should be cached for?

{% hint style="success" %}
`TTL`
{% endhint %}

#### What type of DNS Server is usually provided by your ISP?

{% hint style="success" %}
`Recursive`
{% endhint %}

#### What type of server holds all the records for a domain?

{% hint style="success" %}
`Authoritative`
{% endhint %}

## Task 5 Practical

#### What is the CNAME of shop.website.thm?

![](<../../.gitbook/assets/Screenshot from 2022-03-26 08-26-23.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-26 08-26-57.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-26 08-27-40.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-26 08-28-05.png>)

{% hint style="success" %}
`shops.myshopify.com`
{% endhint %}

#### What is the value of the TXT record of website.thm?

{% hint style="success" %}
`THM{7012BBA60997F35A9516C2E16D2944FF}`
{% endhint %}

#### What is the numerical priority value for the MX record?

{% hint style="success" %}
`30`
{% endhint %}

#### What is the IP address for the A record of www.website.thm?

{% hint style="success" %}
`10.10.10.10`
{% endhint %}
