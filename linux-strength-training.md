# Linux Strength Training

## Task 2 Finding your way around linux

#### What is the correct option for finding files based on group

{% hint style="success" %}
`-group`
{% endhint %}

#### What is format for finding a file with the user named Francis and with a size of 52 kilobytes in the directory /home/francis/

{% hint style="success" %}
`find /home/francis -type f -user Francis -size 52k`
{% endhint %}

#### Go to the /home/topson/chatlogs directory and type the following: grep -iRl 'keyword'. What is the name of the file that you found using this command?

```bash
cd chatlogs
grep -iR 'keyword'
# 2019-10-11:commodo porkeywordttitor ut enim. vitae, ac, aliquet elementum felis eleifend justo,
```

{% hint style="success" %}
`2019-10-11`
{% endhint %}

#### What are the characters subsequent to the word you found?

{% hint style="success" %}
`ttitor`
{% endhint %}

#### Read the file named 'ReadMeIfStuck.txt'. What is the Flag?

```bash
find / -type f -name ReadMeIfStuck.txt -exec cat {} \; 2>/dev/null
# Looking for flag 2?: look for a file named readME_hint.txt


find / -type f -name additionalHINT -exec cat {} \; 2>/dev/null
# try to find a directory called telephone numbers... Oh wait.. it  contains a space.. I wonder how we can find that....
find / -type d -name 'telephone numbers' 2>/dev/null
# /home/topson/corperateFiles/xch/telephone numbers
cat /home/topson/corperateFiles/xch/telephone\ numbers/readME.txt 
# use the Find command to find a file with a modified date of 2016-09-12 from the /workflows directory
find /home/topson/workflows/ -type f -newermt 2016-09-11 ! -newermt 2016-09-13 2>/dev/null
# /home/topson/workflows/xft/eBQRhHvx
cat /home/topson/workflows/xft/eBQRhHvx | egrep -o '.{4}{[^}]*}'
# Flag{81726350827fe53g}


find / -type f -name readME_hint.txt 2>/dev/null
# /home/topson/corperateFiles/RecordsFinances/readME_hint.txt
cd /home/topson/corperateFiles/RecordsFinances/
cat readME_hint.txt
# Instructions: Move the MoveMe.txt file to the march folder directory and then execute the SH program to reveal the second flag.
mv -- '-MoveMe.txt' '-march folder'/
cd -- '-march folder'/
./-runME.sh
# Flag{234@i4s87u5hbn$3}
```

{% hint style="success" %}
`Flag{81726350827fe53g}`
{% endhint %}

## Task 3 Working with files

#### Hypothetically, you find yourself in a directory with many files and want to move all these files to the directory of /home/francis/logs. What is the correct command to do this?

{% hint style="success" %}
`mv * /home/francis/logs`
{% endhint %}

#### Hypothetically, you want to transfer a file from your /home/james/Desktop/ with the name script.py to the remote machine (192.168.10.5) directory of /home/john/scripts using the username of john. What would be the full command to do this?

{% hint style="success" %}
`scp /home/james/Desktop/script.py john@192.168.10.5:/home/john/scripts`
{% endhint %}

#### How would you rename a folder named -logs to -newlogs

{% hint style="success" %}
`mv -- -logs -newlogs`
{% endhint %}

#### How would you copy the file named encryption keys to the directory of /home/john/logs

{% hint style="success" %}
`cp 'encryption keys' /home/john/logs`
{% endhint %}

#### Find a file named readME\_hint.txt inside topson's directory and read it. Using the instructions it gives you, get the second flag.

{% hint style="success" %}
`Flag{234@i4s87u5hbn$3}`
{% endhint %}

## Task 4 Hashing - introduction

#### Download the hash file attached to this task and attempt to crack the MD5 hash. What is the password?

```bash
hashcat -a 0 -m 0 hash1.txt /usr/share/wordlists/rockyou.txt
```

{% hint style="success" %}
`secret123`
{% endhint %}

#### What is the hash type stored in the file hashA.txt

```bash
find / -type f -name hashA.txt -exec cat {} \; 2>/dev/null
# f9d4049dd6a4dc35d40e5265954b2a46
```

```bash
hash-identifier f9d4049dd6a4dc35d40e5265954b2a46
```

{% hint style="success" %}
`MD4`
{% endhint %}

#### Crack hashA.txt using john the ripper, what is the password?

```bash
echo -n 'f9d4049dd6a4dc35d40e5265954b2a46' > hash.txt
john --format=raw-md4 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt 
```

{% hint style="success" %}
`admin`
{% endhint %}

#### What is the hash type stored in the file hashB.txt

```bash
find / -type f -name hashB.txt -exec cat {} \; 2>/dev/null
# b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
```

```
hash-identifier b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
```

{% hint style="success" %}
`SHA-1`
{% endhint %}

#### Find a wordlist with the file extention of '.mnf' and use it to crack the hash with the filename hashC.txt. What is the password?

```bash
find / -type f -name '*.mnf' 2>/dev/null
# /home/sarah/system AB/db/ww.mnf
find / -type f -name hashC.txt -exec cat {} \; 2>/dev/null
# c05e35377b5a31f428ccda9724a9dfbd0c5d71dccac691228d803c78e2e8da29
```

```bash
hash-identifier c05e35377b5a31f428ccda9724a9dfbd0c5d71dccac691228d803c78e2e8da29
# SHA-256
scp sarah@10.10.5.159:'/home/sarah/system\ AB/db/ww.mnf' .
echo -n 'c05e35377b5a31f428ccda9724a9dfbd0c5d71dccac691228d803c78e2e8da29' > hash.txt
john --format=raw-sha256 --wordlist=ww.mnf hash.txt
```

{% hint style="success" %}
`unacvaolipatnuggi`
{% endhint %}

#### Crack hashB.txt using john the ripper, what is the password?

```bash
echo -n 'b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3' > hash.txt
john --format=Raw-SHA1 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt 
```

{% hint style="success" %}
`letmein`
{% endhint %}

## Task 5 Decoding base64

#### what is the name of the tool which allows us to decode base64 strings?

{% hint style="success" %}
`base64`
{% endhint %}

#### find a file called encoded.txt. What is the special answer?

```bash
find / -type f -name encoded.txt -exec cat {} \; 2>/dev/null \
| base64 -d | grep special
# special: the answer is in a file called ent.txt
find / -type f -name ent.txt -exec cat {} \; 2>/dev/null 
# bfddc35c8f9c989545119988f79ccc77
```

```bash
hash-identifier bfddc35c8f9c989545119988f79ccc77
echo -n 'bfddc35c8f9c989545119988f79ccc77' > hash.txt
hashcat -a 0 -m 900 hash.txt /usr/share/wordlists/rockyou.txt
```

{% hint style="success" %}
`john`
{% endhint %}

## Task 6 Encryption/Decryption using gpg

#### You wish to encrypt a file called history\_logs.txt using the AES-128 scheme. What is the full command to do this?

{% hint style="success" %}
`gpg --cipher-algo AES-128 --symmetric history_logs.txt`
{% endhint %}

#### What is the command to decrypt the file you just encrypted?

{% hint style="success" %}
`gpg history_logs.txt.gpg`
{% endhint %}

#### Find an encrypted file called layer4.txt, its password is bob. Use this to locate the flag. What is the flag?

```bash
find / -type f -name layer4.txt -exec gpg {} \; 2>/dev/null
cat layer4.txt 
# 1. Find a file called layer3.txt, its password is james.

find / -type f -name layer3.txt -exec gpg {} \; 2>/dev/null
cat layer3.txt 
# 1. Find a file called layer2.txt, its password is tony.

find / -type f -name layer2.txt -exec gpg {} \; 2>/dev/null
cat layer2.txt | base64 -d
# 1. Find a file called layer1.txt, its password is hacked.

find / -type f -name layer1.txt -exec gpg {} \;  2>/dev/null
cat layer1.txt 
```

{% hint style="success" %}
`Flag{B07$f854f5ghg4s37}`
{% endhint %}

## Task 7 Cracking encrypted gpg files

#### Find an encrypted file called personal.txt.gpg and find a wordlist called data.txt. Use tac to reverse the wordlist before brute-forcing it against the encrypted file. What is the password to the encrypted file?

```bash
find / -type f -name personal.txt.gpg 2>/dev/null
# /home/sarah/oldLogs/units/personal.txt.gpg
find / -type f -name data.txt 2>/dev/null
# /home/sarah/logs/zmn/old stuff/-mvLp/data.txt
```

```bash
scp sarah@10.10.58.33:/home/sarah/oldLogs/units/personal.txt.gpg .
scp sarah@10.10.58.33:'/home/sarah/logs/zmn/old\ stuff/-mvLp/data.txt' . 
gpg2john personal.txt.gpg > gpg.hash
tac data.txt > tac.txt
john --format=gpg --wordlist=tac.txt gpg.hash
```

{% hint style="success" %}
`valamanezivonia`
{% endhint %}

#### What is written in this now decrypted file?

```
gpg personal.txt.gpg
cat personal.txt
```

{% hint style="success" %}
`GETTING STRONGER IN LINUX`
{% endhint %}

## Task 8 Reading SQL databases

#### Find a file called employees.sql and read the SQL database. (Sarah and Sameer can log both into mysql using the password: password). Find the flag contained in one of the tables. What is the flag?

```bash
find / -type f -name employees.sql 2>/dev/null
# /home/sarah/serverLx/employees.sql
cd /home/sarah/serverLx/
mysql -u sarah -p
mysql> source employees.sql
mysql> show tables;
mysql> SELECT * FROM employees WHERE first_name LIKE '%flag%' OR last_name LIKE '%flag%';
```

{% hint style="success" %}
`Flag{13490AB8}`
{% endhint %}

## Task 9 Final Challenge

```bash
cd /home/shared/chatlogs/
cat LpnQ
# James is the only one with root access.
```

#### What is Sameer's SSH password?

```bash
grep -ir --color ssh *
# All I remember is that the password began with ebq. 
# You will need Sameer’s account. His SSH password is: thegreatestpasswordever000. 
```

{% hint style="success" %}
`thegreatestpasswordever000`
{% endhint %}

```bash
ssh sameer@10.10.58.33
cd /home/shared/chatlogs/
```

#### What is the password for the sql database back-up copy

```bash
grep -ir --color sql *
find /home/shared/sql/conf/ -type f -size 50M 2>/dev/null
# /home/shared/sql/conf/JKpN
cat /home/shared/sql/conf/JKpN | sed -n 3p | cut -d ' ' -f3 | base64 -d
# home/sameer/History LB/labmind/latestBuild/configBDB
egrep -Rh '^ebq' '/home/sameer/History LB/labmind/latestBuild/configBDB/'
# ebqiojsdfioj
# ebqiojsiodj
# ebqiojdifoj
# ebqiopsjdfopj
# ebqnice
# ebqops
# ebqiuiud
# ebqjoisjdfij
# ebqkjjdd
# ebqijsji
# ebqopkopk
# ebqattle
ls /home/shared/sql/
# 2020-08-13.zip.gpg
gpg /home/shared/sql/2020-08-13.zip.gpg
# gpg2john not working for 2020-08-13.zip.gpg
```

{% hint style="success" %}
`ebqattle`
{% endhint %}

#### Find the SSH password of the user James. What is the password?

```bash
unzip /home/shared/sql/2020-08-13.zip
cd 2020-08-13/
mysql -u sameer -p
mysql> source employees.sql
mysql> show tables;
mysql> SELECT * FROM employees WHERE first_name = 'James';
```

{% hint style="success" %}
`vuimaxcullings`
{% endhint %}

#### What is the root flag?

```bash
ssh james@10.10.58.33
sudo su -
cat root.txt 
```

{% hint style="success" %}
`Flag{6$8$hyJSJ3KDJ3881}`
{% endhint %}

## Reference

{% embed url="https://www.cyberciti.biz/faq/linuxunix-move-file-starting-with-a-dash/" %}

{% embed url="https://www.hackingarticles.in/beginner-guide-john-the-ripper-part-1/" %}

{% embed url="https://stackoverflow.com/questions/19858176/how-do-i-escape-spaces-in-path-for-scp-copy-in-linux" %}
