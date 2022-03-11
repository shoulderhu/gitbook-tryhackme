# Linux Challenges

## :point\_right: Linux Challenges Introduction

### How many visible files can you see in garrys home directory?

```
ls
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-04-49.png>)

## :basketball: The Basics

### **What is flag 1?**

```
cat flag1.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-43-03.png>)

### What is flag 2?

```
ssh bob@localhost
cat flag2.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-09-51.png>)

### **Flag 3 is located where bob's bash history gets stored.**

```
head -1 .bash_history
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-11-35.png>)

### **Flag 4 is located where cron jobs are created.**

```
crontab -lu bob | grep flag4
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-35-33.png>)

### Find and retrieve flag 5.

```
find / -name flag5.txt 2>/dev/null
cat /lib/terminfo/E/flag5.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-18-02.png>)

### **"Grep" through flag 6 and find the flag. The first 2 characters of the flag is c9.**

```
find / -name flag6.txt 2>/dev/null
egrep -o 'c9[^ ]{30}' /home/flag6.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-22-45.png>)

### Look at the systems processes. What is flag 7?

```
ps aux | grep flag7
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-23-44.png>)

### **De-compress and get flag 8.**

```
tar xzf flag8.tar.gz -O
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-25-27.png>)

### **By look in your hosts file, locate and retrieve flag 9.**

```
egrep -o '[a-z0-9]{32}' /etc/hosts
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-29-22.png>)

### **Find all other users on the system. What is flag 10?**

```
egrep -o '[a-z0-9]{32}' /etc/passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-30-45.png>)

## :construction\_site: Linux Functionality

### Locate where your command alias are stored and get flag 11.

```
grep flag11 .bashrc
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-55-03.png>)

### **Flag12 is located were MOTD's are usually found on an Ubuntu OS. What is flag12?**

```
grep -i flag12 /etc/update-motd.d/00-header
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 21-55-17.png>)

### **Find the difference between two script files to find flag 13.**

```
diff flag13/script{1,2} | egrep -o '[a-z0-9]{32}'
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-00-11.png>)

### Where on the file system are logs typically stored? Find flag 14.

```
tail -1 /var/log/flagtourteen.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-04-39.png>)

### Can you find information about the system, such as the kernel version etc. Find flag 15.

```
head -1 /etc/lsb-release
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-07-50.png>)

### **Flag 16 lies within another system mount.**

```
echo /media/f/l/a/g/1/6/is/cab4b7cae33c87794d82efa1e7f834e6/test.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-22-43.png>)

### **Login to alice's account and get flag 17. Her password is TryHackMe123**

```
su - alice
cat flag17
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-10-35.png>)

### **Find the hidden flag 18.**

```
cat .flag18
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-11-26.png>)

### **Read the 2345th line of the file that contains flag 19.**

```
sed -n '2345p' flag19
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-12-35.png>)

## Data Representation, Strings and Permissions

### **Find and retrieve flag 20.**

```
cat flag20.txt | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-31-48.png>)

### **Inspect the flag21.php file. Find the flag.**

```
strings /home/bob/flag21.php
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-34-42.png>)

### **Locate and read flag 22. Its represented as hex.**

```
cat flag22 | xxd -r -p
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-38-53.png>)

### **Locate, read and reverse flag 23.**

```
rev flag23
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-39-58.png>)

### Analyse the flag 24 compiled C program.

```
strings /home/garry/flag24 | grep flag
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-41-54.png>)

### Find flag 26 by searching the all files for a string that begins with 4bceb and is 32 characters long.

```
egrep -r '^4bceb[a-z0-9]{27}' / 2>/dev/null
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 11-13-48.png>)

### **Locate and retrieve flag 27, which is owned by the root user.**

```
sudo -l
sudo /bin/cat /home/flag27
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-54-40.png>)

### **Whats the linux kernel version?**

```
uname -r
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 22-55-33.png>)

### Find the file called flag 29 and do the following operations on it:

1. Remove all spaces in file.
2. Remove all new line spaces.
3. Split by comma and get the last element in the split.

```bash
cat /home/garry/flag29 | tr -d ' ' | tr -d '\n' | rev | cut -d ',' -f1 | rev
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 23-01-10.png>)

## :man\_surfing: **** SQL, FTP, Groups and RDP

### **Use curl to find flag 30.**

```
curl localhost
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 09-51-29.png>)

### Flag 31 is a MySQL database name.

```
mysql -u root -p
mysql> show databases;
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 09-53-03.png>)

### **Get data out of the table from the database you found above!**

```
mysql> use database_2fb1cab13bf5f4d61de3555430c917f4;
mysql> show tables;
mysql> select * from flags;
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 09-55-49.png>)

### **Using SCP, FileZilla or another FTP client download flag32.mp3 to reveal flag 32.**

```
scp alice@10.10.37.170:/home/alice/flag32.mp3 .
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 09-59-39.png>)

### **Flag 33 is located where your personal $PATH's are stored.**

```
head -1 /home/bob/.profile
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 10-06-04.png>)

### **Switch your account back to bob. Using system variables, what is flag34?**

```bash
su - bob
env | grep flag34
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 10-07-09.png>)

### **Look at all groups created on the system. What is flag 35?**

```
grep flag35 /etc/group
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 10-09-53.png>)

### **Find the user which is apart of the "hacker" group and read flag 36.**

```
find / -name flag36 2>/dev/null
getent group hacker
cat /etc/flag36
```

![](<../../.gitbook/assets/Screenshot from 2020-09-08 10-22-58.png>)







### **** ****
