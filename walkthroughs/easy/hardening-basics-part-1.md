---
description: https://tryhackme.com/room/hardeningbasicspart1
---

# Hardening Basics Part 1

## Task 11 \~\~\~\~\~ Chapter 1 Quiz \~\~\~\~\~

```bash
ssh spooky@10.10.205.236
```

#### What group are users automatically added to in Ubuntu?

{% hint style="success" %}
`sudo`
{% endhint %}

#### What would be the command to add an existing user, nick, to the sudo group? You're running as root

{% hint style="success" %}
`usermod -aG sudo nick`
{% endhint %}

#### What command as a user can we enter to see what we are allowed to execute with sudo?

{% hint style="success" %}
sudo -l
{% endhint %}

#### Where is the sudo policy file stored?

{% hint style="success" %}
`/etc/sudoers`
{% endhint %}

#### When in visudo and you see %\_\_\_\_, what does the % sign indicate that you are dealing with?

{% hint style="success" %}
`group`
{% endhint %}

#### This Alias lets the user assign a name, like "ADMINS" to a group of peopleThis Alias lets the user assign a name, like "ADMINS" to a group of people

{% hint style="success" %}
`User`
{% endhint %}

#### Which Alias allows you to create a set of commands that you can then assign to a User Alias?

{% hint style="success" %}
`Command`
{% endhint %}

#### emacs has a shell escape

{% hint style="success" %}
`Yey`
{% endhint %}

#### What is the minimum recommended password length set by NIST?

![](<../../.gitbook/assets/Screenshot from 2022-03-13 16-30-32.png>)

{% hint style="success" %}
`8`
{% endhint %}

#### When using the pwhistory module, which file will contain the previous passwords for the user?

![](<../../.gitbook/assets/Screenshot from 2022-03-13 16-32-28.png>)

{% hint style="success" %}
`opasswd`
{% endhint %}

#### What principle states that every user only has enough access to do their daily duties and tasks

{% hint style="success" %}
`Principle of Least Privilege`
{% endhint %}

## Task 15 Basic Uncomplicated Firewall for Ubuntu & Chapter 2 Quiz

#### This type of Firewall typically has two NIC cards

{% hint style="success" %}
`Network-Based`
{% endhint %}

#### This type of Firewall is typically installed on a host computer and rules apply to that specific host only

{% hint style="success" %}
Host-Based
{% endhint %}

#### Web Application Firewalls help add an extra layer of security to your web servers. Where should these be installed?

{% hint style="success" %}
`Demilitarized Zone`
{% endhint %}

#### iptables is _not_ the name of the Linux Firewall.  What is the framework that iptables allows us to interact with?

{% hint style="success" %}
`netfilter`
{% endhint %}

#### This 3 letter acronym is a set of rules that defines what the Firewall should allow and what it should deny

{% hint style="success" %}
`ACL`
{% endhint %}

#### Which iptables option allows us to keep track of the connection state?

{% hint style="success" %}
`--ctstate`
{% endhint %}

#### Which iptable Chain is responsible for packets on the local network that are being carried onwards?

{% hint style="success" %}
`FORWARD`
{% endhint %}

#### Which table mashes up the packets as they go through the Firewall?

{% hint style="success" %}
`MANGLE`
{% endhint %}

#### What is the last rule that should be added to an access control list?

{% hint style="success" %}
`Implicit Deny`
{% endhint %}
