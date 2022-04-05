# Team

{% embed url="https://tryhackme.com/room/teamcw" %}
https://tryhackme.com/room/teamcw
{% endembed %}

## Task 2 Flags

#### user.txt

```bash
rustscan -a 10.10.124.139 -- -n -sVC
```

```bash
echo '10.10.124.139' | sudo tee -a /etc/hosts
gobuster dir -u http://team.thm/ \
             -w /usr/share/dirb/wordlists/common.txt  \
             -t128
gobuster dir -u http://team.thm/scripts \
             -w /usr/share/dirb/wordlists/common.txt \
             -x txt,js -t128
```

{% hint style="success" %}

{% endhint %}

#### root.txt

{% hint style="success" %}

{% endhint %}

