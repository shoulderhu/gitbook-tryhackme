---
description: https://tryhackme.com/room/scripting
---

# Scripting

## :basketball: Base64

```python
from base64 import b64decode

with open("b64.txt") as f:
    line = f.read().encode()

for _ in range(50):
    line = b64decode(line)

print(line.decode())
```

## :baseball: Gotta Catch em All

```python
from requests import get
from requests.exceptions import ConnectionError
from bs4 import BeautifulSoup
from time import sleep

addr = "10.10.2.21"
num = 0.0
stop = True

resp = get("http://{}:3010".format(addr))
soup = BeautifulSoup(resp.text, "html.parser")
port = int(soup.find(id="onPort").string)

while True:
    try:
        resp = get("http://{}:{}".format(addr, port))
    except ConnectionError:
        continue

    if resp.text == "STOP":
        print(resp.text, round(num, 2))
        port = 1337
        num = 0.0
    else:
        print(resp.text)
        text = resp.text.split()
        port = int(text[2])

        try:
            if text[0] == "add":
                num += float(text[1])
            elif text[0] == "minus":
                num -= float(text[1])
            elif text[0] == "multiply":
                num *= float(text[1])
            elif text[0] == "divide":
                num /= float(text[1])
        except ValueError:
            pass

    sleep(4)
```

## :secret: Encrypted Server Chit Chat

```python
import hashlib
from cryptography.hazmat.primitives.ciphers import Cipher
from cryptography.hazmat.primitives.ciphers.algorithms import AES
from cryptography.hazmat.primitives.ciphers.modes import GCM
from cryptography.hazmat.backends import default_backend
from socket import socket, AF_INET, SOCK_DGRAM

sock = socket(AF_INET, SOCK_DGRAM)
address = ("10.10.232.94", 4000)
sock.sendto(b"hello", address)
recv = sock.recvfrom(1024)[0]

sock.sendto(b"ready", address)
recv = sock.recvfrom(1024)[0].split(b" ")
key = recv[0].split(b":")[1]
iv = recv[1].split(b":")[1]
hash = recv[14].hex()

while True:
    sock.sendto(b"final", address)
    flag = sock.recvfrom(1024)[0]

    sock.sendto(b"final", address)
    tag = sock.recvfrom(1024)[0]

    aes = Cipher(AES(key), GCM(iv, tag, min_tag_length=4), 
                 backend=default_backend()).decryptor()
    ans = aes.update(flag) + aes.finalize()

    sha256 = hashlib.sha256()
    sha256.update(ans)
    if sha256.hexdigest() == hash:
        print(ans.decode())
        break
```
