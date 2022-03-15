---
description: https://tryhackme.com/room/rustscan
---

# RustScan

## Task 2 Installing RustScan

```bash
wget https://github.com/RustScan/RustScan/releases/download/2.0.1/rustscan_2.0.1_amd64.deb
sudo dpkg -i rustscan_2.0.1_amd64.deb
rustscan
```

## Task 5 Extensible

#### What is the scripting file config called?

{% hint style="success" %}
`rustscan_scripts.toml`
{% endhint %}

#### Can you run other binaries with RustScan?

{% hint style="success" %}
`T`
{% endhint %}

#### Does RutScan support scripts in Javascript?

{% hint style="success" %}
`R`
{% endhint %}

## Task 7 Scanning Time!

#### Try running the scan for all ports.

#### After scanning this, how many ports do we find open under 1000?

```bash
restscan -a 10.10.65.247
```

![](<../../.gitbook/assets/Screenshot from 2022-03-15 19-49-00.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-15 19-49-18.png>)

{% hint style="success" %}
`2`
{% endhint %}

#### Perform a service version detection scan, what is the version of the software running on port 22?

```bash
rustscan -a 10.10.65.247 -p22,80 -- -sV
```

![](<../../.gitbook/assets/Screenshot from 2022-03-15 19-51-31.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-15 19-51-45.png>)

{% hint style="success" %}
`6.6.1p1`
{% endhint %}

#### Perform an aggressive scan, what flag isn't set under the results for port 80?

```bash
rustscan -a 10.10.65.247 -p22,80 -- -A
```

![](<../../.gitbook/assets/Screenshot from 2022-03-15 19-56-16.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-15 19-55-55.png>)

{% hint style="success" %}
`httponly`
{% endhint %}

## Task 8 RustScan Quiz

#### First, how do you access the help menu?

{% hint style="success" %}
`-h`
{% endhint %}

#### Often referred to as "quiet" mode, What switch can do this?

{% hint style="success" %}
`-q`
{% endhint %}

#### Which switch can help us to scan for a particular Range?

{% hint style="success" %}
`-r`
{% endhint %}

#### What switch would you use to find out RustScan's version?

{% hint style="success" %}
`-V`
{% endhint %}

#### Which switch will help us to select batch size?

{% hint style="success" %}
`-b`
{% endhint %}

#### Which switch can set timeout?

{% hint style="success" %}
`-t`
{% endhint %}
