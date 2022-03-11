---
description: https://tryhackme.com/room/pokemon
---

# Gotta Catch'em All!

### &#x20;**Find the Grass-Type Pokemon**

```
nmap 10.10.117.226
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 08-27-53.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-23 08-49-37.png>)

```
ssh pokemon@10.10.117.226
ls -a Desktop/
unzip Desktop/P0kEmOn.zip
cat P0kEmOn/grass-type.txt
cat P0kEmOn/grass-type.txt | xxd -r -p
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 08-50-37.png>)

### **Find the Water-Type Pokemon**

```
find / -name *water-type* 2>/dev/null
cat /var/www/html/water-type.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-09-22.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-03-55.png>)

### **Find the Fire-Type Pokemon**

```
find / -name *fire-type* 2>/dev/null
cat /etc/why_am_i_here\?/fire-type.txt
cat /etc/why_am_i_here\?/fire-type.txt | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-05-01.png>)

### **Who is Root's Favorite Pokemon?**

```
ls -a Videos/
cat Videos/Gotta/Catch/Them/ALL\!/Could_this_be_what_Im_looking_for\?.cplusplus
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 09-16-44.png>)

```bash
su - ash
ls -a /home/
cat /home/roots-pokemon.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-23 08-54-45.png>)

****
