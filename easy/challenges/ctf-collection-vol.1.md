---
description: https://tryhackme.com/room/ctfcollectionvol1
---

# CTF collection Vol.1

## What does the base said?

```bash
echo -n 'VEhNe2p1NTdfZDNjMGQzXzdoM19iNDUzfQ==' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 07-59-46.png>)

### Meta meta

```bash
exiftool Findme.jpg | grep 'Owner Name'
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-02-19.png>)

### Mon, are we going to be okay?

```bash
steghide extract -sf Extinction.jpg
cat Final_message.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-06-22.png>)

### Erm......Magick

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-07-34.png>)

### QRrrrr

```
zbarimg QR.png 2>&1 | head -1
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-09-46.png>)

### Reverse it or read it?

```
strings hello.hello | grep THM
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-11-30.png>)

### Another decoding stuff

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-13-28.png>)

### Left or right

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-14-31.png>)

### Make a comment

![](<../../.gitbook/assets/Screenshot from 2020-09-25 13-50-11.png>)

### Can you fix it?

```
pngcheck spoil.png
hexeditor spoil.png
eog spoil.png
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-17-07.png>)

### Read it

![](<../../.gitbook/assets/Screenshot from 2020-09-25 14-06-11.png>)

### Spin my head

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-21-18.png>)

### An exclusive!

```
python 
>>> hex(0x44585d6b2368737c65252166234f20626d ^ 0x1010101010101010101010101010101010)
>>> "54484d7b3378636c75353176335f30727d".decode("hex")
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 15-44-37.png>)

### Binary walk

```
binwalk hell.jpg
binwalk -D '.*' hell.jpg
unzip _hell.jpg.extracted/40E75
cat hello_there.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-24-24.png>)

### Darkness

```
java -jar Stegsolve.jar
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-26-27.png>)

### A sounding QR

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-28-22.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-34-25.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-33-43.png>)

### Dig up the past

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-36-53.png>)

### Uncrackable!

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-38-03.png>)

### Small bases

```
python
>>> hex(581695969015253365094191591547859387620042736036246486373595515576333693)
>>> "54484d7b31375f6a7535375f346e5f307264316e3472795f62343533357d".decode("hex")
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 15-29-23.png>)

### Read the packet

```
wireshark flag.pcapng
```

![](<../../.gitbook/assets/Screenshot from 2020-09-25 08-43-09.png>)
