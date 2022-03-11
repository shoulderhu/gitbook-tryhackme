# Subdomain Enumeration

## Task 1 Brief

#### What is a subdomain enumeration method beginning with B?

{% hint style="success" %}
`Brute Force`
{% endhint %}

#### What is a subdomain enumeration method beginning with O?

{% hint style="success" %}
`OSINT`
{% endhint %}

#### What is a subdomain enumeration method beginning with V?

{% hint style="success" %}
`Virtual Host`
{% endhint %}

## Task 2 ONIST - SSL/TLS Certificates

#### What domain was logged on crt.sh at 2020-12-26?

![](<.gitbook/assets/Screenshot from 2021-09-10 11-30-35.png>)

{% hint style="success" %}
`store.tryhackme.com`
{% endhint %}

## Task 3 OSINT - Search Engines

#### What is the TryHackMe subdomain beginning with B discovered using the above Google search?

![](<.gitbook/assets/Screenshot from 2021-09-10 11-34-17.png>)

{% hint style="success" %}
`blog.tryhackme.com`
{% endhint %}

## Task 4 DNS Bruteforce

#### What is the first subdomain found with the dnsrecon tool?

![](<.gitbook/assets/Screenshot from 2021-09-10 11-40-54.png>)

{% hint style="success" %}
`api.acmeitsupport.thm`
{% endhint %}

## Task 5 Sublist3r

#### What is the first subdomain discovered by sublist3r?

![](<.gitbook/assets/Screenshot from 2021-09-10 11-40-44.png>)

{% hint style="success" %}
`web55.acmeitsupport.thm`
{% endhint %}

## Task 6 Virtual Hosts

```bash
ffuf -c -w /usr/share/seclists/Discovery/DNS/namelist.txt \
     -H 'Host: FUZZ.acmeitsupport.thm' -u http://10.10.66.20 -fs 2395
```

#### What is the first subdomain discovered?

{% hint style="success" %}
`delta`
{% endhint %}

#### What is the second subdomain discovered?

{% hint style="success" %}
`yellow`
{% endhint %}
