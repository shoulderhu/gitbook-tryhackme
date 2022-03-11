---
description: https://tryhackme.com/room/ninjaskills
---

# Ninja Skills

```bash
find / -type f \( -name 8V2L \
                  -o -name bny0 \
                  -o -name c4ZX \
                  -o -name D8B3 \
                  -o -name FHl1 \
                  -o -name oiMO \
                  -o -name PFbD \
                  -o -name rmfX \
                  -o -name SRSq \
                  -o -name uqyw \
                  -o -name v2Vb \
                  -o -name X1Uy \) 2>/dev/null
find / -type f \( -name 8V2L \
                  -o -name bny0 \
                  -o -name c4ZX \
                  -o -name D8B3 \
                  -o -name FHl1 \
                  -o -name oiMO \
                  -o -name PFbD \
                  -o -name rmfX \
                  -o -name SRSq \
                  -o -name uqyw \
                  -o -name v2Vb \
                  -o -name X1Uy \) 2>/dev/null | tr '\n' ' ' > files.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 12-20-17.png>)

### **Which of the above files are owned by the best-group group**

```bash
ls -l $(cat files.txt) | grep best-group
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 12-26-31.png>)

### **Which of these files contain an IP address?**

```bash
egrep '[0-9]{1,3}(\.[0-9]{1,3}){1,3}' $(cat files.txt)
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 12-24-27.png>)

### **Which file has the SHA1 hash of 9d54da7584015647ba052173b84d45e8007eba94**

```bash
sha1sum $(cat files.txt) | grep 9d54da7584015647ba052173b84d45e8007eba94
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 12-25-34.png>)

### **Which file contains 230 lines?**

```bash
wc $(cat files.txt)
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 12-27-50.png>)

### **Which file's owner has an ID of 502?**

```bash
ls -ln $(cat files.txt)
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 12-31-14.png>)

### **Which file is executable by everyone?**

> /etc/8V2L
