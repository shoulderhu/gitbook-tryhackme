---
description: https://tryhackme.com/room/passiverecon
---

# Passive Reconnaissance

## Task 2 Passive Versus Active Recon

#### You visit the Facebook page of the target company, hoping to get some of their employee names. What kind of reconnaissance activity is this?

{% hint style="success" %}
`P`
{% endhint %}

#### You ping the IP address of the company webserver to check if ICMP traffic is blocked. What kind of reconnaissance activity is this?

{% hint style="success" %}
`A`
{% endhint %}

#### You happen to meet the IT administrator of the target company at a party. You try to use social engineering to get more information about their systems and network infrastructure. What kind of reconnaissance activity is this?

{% hint style="success" %}
`A`
{% endhint %}

## Task 3 Whois

#### When was TryHackMe.com registered?

```bash
whois tryhackme.com
```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-08-51.png>)

{% hint style="success" %}
20180705
{% endhint %}

#### What is the registrar of TryHackMe.com?

{% hint style="success" %}
`namecheap.com`
{% endhint %}

#### Which company is TryHackMe.com using for name servers?

{% hint style="success" %}
`CLOUDFLARE.COM`
{% endhint %}

## Task 4 nslookup and dig

```bash
nslookup -type=TXT thmlabs.com
dig thmlabs.com TXT
```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-19-50.png>)

{% hint style="success" %}
`THM{a5b83929888ed36acb0272971e438d78}`
{% endhint %}

## Task 5 DNSDumpster

#### Lookup tryhackme.com on DNSDumpster. What is one interesting subdomain that you would discover in addition to www and blog?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-26-48.png>)

{% hint style="success" %}
`remote`
{% endhint %}

## Task 6 Shodan.io

#### According to Shodan.io, what is the 2nd country in the world in terms of the number of publicly accessible Apache servers?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-35-36.png>)

{% hint style="success" %}
`Germany`
{% endhint %}

#### Based on Shodan.io, what is the 3rd most common port used for Apache?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-36-21.png>)

{% hint style="success" %}
`8080`
{% endhint %}

#### Based on Shodan.io, what is the 3rd most common port used for nginx?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-37-09.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-06 11-37-56.png>)

{% hint style="success" %}
`8888`
{% endhint %}
