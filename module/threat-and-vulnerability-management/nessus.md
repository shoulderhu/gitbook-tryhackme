---
description: https://tryhackme.com/room/rpnessusredux
---

# Nessus

## Task 3 Navigation and Scans

#### What is the name of the button which is used to launch a scan?

{% hint style="success" %}
`New Scan`
{% endhint %}

#### What side menu option allows us to create custom templates?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-13-56.png>)

{% hint style="success" %}
`Policies`
{% endhint %}

#### What menu allows us to change plugin properties such as hiding them or changing their severity?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-14-11.png>)

{% hint style="success" %}
`Plugin Rules`
{% endhint %}

#### In the '**Scan Templates**' section after clicking on '**New Scan**', what scan allows us to see simply what hosts are alive?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-16-45.png>)

{% hint style="success" %}
`Host Discovery`
{% endhint %}

#### One of the most useful scan types, which is considered to be 'suitable for any host'?

{% hint style="success" %}
`Basic Network Scan`
{% endhint %}

#### What scan allows you to 'Authenticate to hosts and enumerate missing updates'?

{% hint style="success" %}
`Credentialed Patch Audit`
{% endhint %}

#### What scan is specifically used for scanning **Web Applications**?&#x20;

{% hint style="success" %}
`Web Application Tests`
{% endhint %}

## Task 4 Scanning!

#### Create a new '**Basic Network Scan**' targeting the deployed VM. What option can we set under '**BASIC**' (on the left) to set a time for this scan to run? This can be very useful when network congestion is an issue.

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-19-45.png>)

{% hint style="success" %}
`Schedule`
{% endhint %}

#### Under 'DISCOVERY' (on the left) set the 'Scan Type' to cover ports 1-65535. What is this type called?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-21-00.png>)

{% hint style="success" %}
`Port scan (all ports)`
{% endhint %}

#### What 'Scan Type' can we change to under '**ADVANCED**' for lower bandwidth connection?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-23-49.png>)

{% hint style="success" %}
`Scan low bandwidth links`
{% endhint %}

#### With these options set, launch the scan.

#### After the scan completes, which '**Vulnerability**' in the '**Port scanners**' family can we view the details of to see the open ports on this host?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-36-55.png>)

{% hint style="success" %}
`Nessus SYN scanner`
{% endhint %}

#### What Apache HTTP Server Version is reported by Nessus?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-38-27.png>)

{% hint style="success" %}
`2.4.99`
{% endhint %}

## Task 5 Scanning a Web Application!

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-27-46.png>)

#### What is the plugin id of the plugin that determines the HTTP server type and version?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-48-44.png>)

{% hint style="success" %}
`10107`
{% endhint %}

#### What authentication page is discovered by the scanner that transmits credentials in cleartext?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-50-26.png>)

{% hint style="success" %}
`login.php`
{% endhint %}

#### What is the file extension of the config backup?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-51-46.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-52-06.png>)

{% hint style="success" %}
`.bak`
{% endhint %}

#### Which directory contains example documents?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-55-46.png>)

{% hint style="success" %}
`/external/phpids/0.6/docs/examples/`
{% endhint %}

#### What vulnerability is this application susceptible to that is associated with X-Frame-Options?

![](<../../.gitbook/assets/Screenshot from 2022-03-09 23-58-51.png>)

{% hint style="success" %}
`Clickjacking`
{% endhint %}
