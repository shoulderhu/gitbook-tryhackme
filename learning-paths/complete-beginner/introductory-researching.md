# Introductory Researching

{% embed url="https://tryhackme.com/room/introtoresearch" %}
https://tryhackme.com/room/introtoresearch
{% endembed %}

## Task 2 Example Research Question

#### In the Burp Suite Program that ships with Kali Linux, what mode would you use to manually send a request?

{% hint style="success" %}
`Repeater`
{% endhint %}

#### **What hash format are modern Windows login passwords stored in?**

{% hint style="success" %}
`NTLM`
{% endhint %}

#### **What are automated tasks called in Linux?**

{% hint style="success" %}
`Cron Jobs`
{% endhint %}

**What number base could you use as a shorthand for base 2 (binary)?**

{% hint style="success" %}
`base 16`
{% endhint %}

#### **If a password hash starts with $6$, what format is it?**

{% hint style="success" %}
`sha512crypt`
{% endhint %}

## Task 3 Vulnerability Searching

#### **What is the CVE for the 2020 Cross-Site Scripting (XSS) vulnerability found in WPForms?**

```bash
searchsploit -w wpforms
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 22-17-02.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-24 16-15-27.png>)

{% hint style="success" %}
`CVE-2020-10385`
{% endhint %}

#### There was a Local Privilege Escalation vulnerability found in the Debian version of Apache Tomcat, back in 2016. What's the CVE for this vulnerability?

```
searchsploit -w debian tomcat
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 22-20-48.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-24 16-17-03.png>)

{% hint style="success" %}
`CVE-2016-1240`
{% endhint %}

#### **What is the very first CVE found in the VLC media player?**

![](<../../.gitbook/assets/Screenshot from 2020-08-31 23-09-47.png>)

{% hint style="success" %}
`CVE-2007-0017`
{% endhint %}

#### **If I wanted to exploit a buffer overflow in the sudo program, which CVE would I use?**

![](<../../.gitbook/assets/Screenshot from 2020-08-31 23-17-34.png>)

{% hint style="success" %}
`CVE-2019-18634`
{% endhint %}

## Task 4 Manual Pages

#### SCP is a tool used to copy files from one computer to another. What switch would you use to copy an entire directory?

{% hint style="success" %}
`-r`
{% endhint %}

#### fdisk is a command used to view and alter the partitioning scheme used on your hard drive. What switch would you use to list the current partitions?

{% hint style="success" %}
`-l`
{% endhint %}

#### nano is an easy-to-use text editor for Linux. What switch would you use to make a backup when opening a file with nano?

{% hint style="success" %}
`-B`
{% endhint %}

#### **Netcat is a basic tool used to manually send and receive network requests.** **What command would you use to start netcat in listen mode, using port 12345?**

{% hint style="success" %}
`nc -l -p 12345`
{% endhint %}
