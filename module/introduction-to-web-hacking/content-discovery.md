---
description: https://tryhackme.com/room/contentdiscovery
---

# Content Discovery

## Task 1 What Is Content Discovery?

#### What is the Content Discovery method that begins with M?

{% hint style="success" %}
`Manually`
{% endhint %}

#### What is the Content Discovery method that begins with A?

{% hint style="success" %}
`Automated`
{% endhint %}

#### What is the Content Discovery method that begins with O?

{% hint style="success" %}
`OSINT`
{% endhint %}

## Task 2 Manual Discovery - Robots.txt

#### What is the directory in the robots.txt that isn't allowed to be viewed by web crawlers?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-11-13.png>)

{% hint style="success" %}
`/staff-portal`
{% endhint %}

## Task 3 Manual Discovery - Favicon

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-13-56.png>)

```bash
curl -s https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-15-45.png>)

![https://wiki.owasp.org/index.php/OWASP\_favicon\_database](<../../.gitbook/assets/Screenshot from 2022-03-06 17-16-36.png>)

{% hint style="success" %}
`cgiirc`
{% endhint %}

## Task 4 Manual Discovery - Sitemap.xml

#### What is the path of the secret area that can be found in the sitemap.xml file?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-24-05.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-25-40.png>)

{% hint style="success" %}
`/s3cr3t-area`
{% endhint %}

## Task 5 Manual Discovery - HTTP Headers

#### What is the flag value from the X-FLAG header?

```bash
curl -I 10.10.91.7
```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-30-34.png>)

{% hint style="success" %}
`THM{HEADER_FLAG}`
{% endhint %}

## Task 6 Manual Discovery - Framework Stack

#### What is the flag from the framework's administration portal?

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-34-53.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-35-24.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-35-39.png>)

{% hint style="success" %}
`THM{CHANGE_DEFAULT_CREDENTIALS}`
{% endhint %}

## Task 7 OSINT - Google Hacking / Dorking

#### What Google dork operator can be used to only show results from a particular site?

{% hint style="success" %}
`site:`
{% endhint %}

## Task 8 OSINT - Wappalyzer

#### What online tool can be used to identify what technologies a website is running?

{% hint style="success" %}
`Wappalyzer`
{% endhint %}

## Task 9 OSINT - Wayback Machine

#### What is the website address for the Wayback Machine?

{% hint style="success" %}
`https://archive.org/web/`
{% endhint %}

## Task 10 OSINT - GitHub

#### What is Git?

{% hint style="success" %}
`version control system`
{% endhint %}

## Task 11 OSINT - S3 Buckets

#### What URL format do Amazon S3 buckets end in?

{% hint style="success" %}
`.s3.amazonaws.com`
{% endhint %}

## Task 12

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt \
     -u http://10.10.91.7/FUZZ -c -t 128

```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-51-36.png>)

```bash
dirb http://10.10.91.7/ /usr/share/seclists/Discovery/Web-Content/common.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 18-14-04.png>)

```bash
gobuster dir -u http://10.10.91.7/ \
             -w /usr/share/seclists/Discovery/Web-Content/common.txt \
             -t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-06 17-53-47.png>)

#### What is the name of the directory beginning "/mo...." that was discovered?

{% hint style="success" %}
`/monthly`
{% endhint %}

#### What is the name of the log file that was discovered?

{% hint style="success" %}
`/development.log`
{% endhint %}

## Reference

{% embed url="https://wiki.owasp.org/index.php/OWASP_favicon_database" %}
