---
description: >-
  Power-up your Linux skills and get hands-on with some common utilities that
  you are likely to use day-to-day!
---

# Linux Fundamentals Part 3

{% embed url="https://tryhackme.com/room/linuxfundamentalspart3" %}
https://tryhackme.com/room/linuxfundamentalspart3
{% endembed %}

## Task 3 Terminal Text Editors

#### Edit "task3" located in "tryhackme"'s home directory using Nano. What is the flag?

```bash
vim tryhackme
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 07-23-27.png>)

{% hint style="success" %}
`THM{TEXT_EDITORS}`
{% endhint %}

## Task 4 General/Useful Utilities

#### Now, use Python 3's "HTTPServer" module to start a web server in the home directory of the "tryhackme" user on the deployed instance.

```bash
python3 -m http.server
curl http://10.10.201.198:8000/.flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 07-31-43.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 07-31-53.png>)

{% hint style="success" %}
`THM{WGET_WEBSERVER}`
{% endhint %}

## Task 5 Processes 101

#### If we were to launch a process where the previous ID was "300", what would the ID of this new process be?

{% hint style="success" %}
`301`
{% endhint %}

#### If we wanted to **cleanly** kill a process, what signal would we send it?

{% hint style="success" %}
`SIGTERM`
{% endhint %}

#### Locate the process that is running on the deployed instance (10.10.201.198). What flag is given?

```bash
ps aux -q 639
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 07-40-09.png>)

{% hint style="success" %}
`THM{PROCESSES}`
{% endhint %}

#### What command would we use to stop the service "myservice"?

{% hint style="success" %}
`systemctl stop myservice`
{% endhint %}

#### What command would we use to start the same service on the boot-up of the system?

{% hint style="success" %}
`systemctl enable myservice`
{% endhint %}

#### What command would we use to bring a previously backgrounded process back to the foreground?

{% hint style="success" %}
`fg`
{% endhint %}

## Task 6 Maintaining Your System: Automation

#### When will the crontab on the deployed instance (10.10.201.198) run?

```bash
crontab -l
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 07-52-16.png>)

{% hint style="success" %}
`@reboot`
{% endhint %}

## Task 7 Maintaining Your System: Package Management

#### Sublime Text Installation

{% tabs %}
{% tab title="Install" %}
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" \
| sudo tee /etc/apt/sources.list.d/sublime-text.list
```

```
sudo apt-get update
sudo apt-get install sublime-text
```
{% endtab %}

{% tab title="Unstall" %}
```bash
sudo rm /etc/apt/sources.list.d/sublime-text.list
sudo apt autoremove sublime-text
```

```bash
add-apt-repository --remove ppa:PPA_Name/ppa
```
{% endtab %}
{% endtabs %}

## Task 8 Maintaining Your System: Logs

```bash
cat /var/log/apache2/access.log.1
```

#### Look for the apache2 logs on the deployable Linux machine. What is the IP address of the user who visited the site?

{% hint style="success" %}
`10.9.232.111`
{% endhint %}

#### What file did they access?

{% hint style="success" %}
/catsanddogs.jpg
{% endhint %}

## Reference

{% embed url="https://crontab-generator.org" %}

{% embed url="https://crontab.guru" %}
