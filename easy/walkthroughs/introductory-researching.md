# Introductory Researching

## :question: Example Research Question

### #1 In the Burp Suite Program that ships with Kali Linux, what mode would you use to manually send a request?

```
Repeater
```

### #2 **What hash format are modern Windows login passwords stored in?**

```
NTLM
```

### #3 **What are automated tasks called in Linux?**

```
Cron Jobs
```

### #4 **What number base could you use as a shorthand for base 2 (binary)?**

```
base 16
```

### #5 **If a password hash starts with $6$, what format is it?**

```
sha512crypt
```

## :mag\_right: Vulnerability Searching

### #1 **What is the CVE for the 2020 Cross-Site Scripting (XSS) vulnerability found in WPForms?**

```bash
searchsploit -w wpforms
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 22-17-02.png>)

### #2 There was a Local Privilege Escalation vulnerability found in the Debian version of Apache Tomcat, back in 2016. What's the CVE for this vulnerability?

```
searchsploit -w debian tomcat
```

![](<../../.gitbook/assets/Screenshot from 2020-08-31 22-20-48.png>)

### #3 **What is the very first CVE found in the VLC media player?**

![](<../../.gitbook/assets/Screenshot from 2020-08-31 23-09-47.png>)

### #4 **If I wanted to exploit a buffer overflow in the sudo program, which CVE would I use?**

![](<../../.gitbook/assets/Screenshot from 2020-08-31 23-17-34.png>)

## :male\_sign: Manual Pages

### #1 SCP is a tool used to copy files from one computer to another. What switch would you use to copy an entire directory?

```
-r
```

### #2 fdisk is a command used to view and alter the partitioning scheme used on your hard drive. What switch would you use to list the current partitions?

```
-l
```

### #3 nano is an easy-to-use text editor for Linux. What switch would you use to make a backup when opening a file with nano?

```
-B
```

### #4 **Netcat is a basic tool used to manually send and receive network requests.** **What command would you use to start netcat in listen mode, using port 12345?**

```
nc -l -p 12345
```
