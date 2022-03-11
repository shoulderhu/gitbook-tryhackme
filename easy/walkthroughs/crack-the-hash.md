---
description: Cracking hashes challenges
---

# Crack the hash

## :closed\_lock\_with\_key: Level 1

Can you complete the level 1 tasks by cracking the hashes?

### #1 MD5

| Hash   | 48bb6e862e54f2a795ffc4e541caed4d |
| ------ | -------------------------------- |
| Answer | easy                             |

```bash
echo '48bb6e862e54f2a795ffc4e541caed4d' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-23 22-32-01.png>)



### #2 SHA1

| Hash   | CBFDAC6008F9CAB4083784CBD1874F76618D2A97 |
| ------ | ---------------------------------------- |
| Answer | password123                              |

```bash
echo 'CBFDAC6008F9CAB4083784CBD1874F76618D2A97' > sha1.txt
hashcat -a 0 -m 100 sha1.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-23 22-47-02.png>)



### #3 SHA-256

| Hash   | 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 |
| ------ | ---------------------------------------------------------------- |
| Answer | letmein                                                          |

```bash
echo '1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032' > sha256.txt
hashcat -a 0 -m 1400 sha256.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-23 22-54-13.png>)



### #4 bcrypt

| Hash   | **$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom** |
| ------ | ---------------------------------------------------------------- |
| Answer | bleh                                                             |

```bash
echo '$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom' > bcrypt.txt
hashcat -a 0 -m 3200 bcrypt.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 00-07-37.png>)



### # 5 MD4

| Hash   | 279412f945939ba78ce0758d3fd83daa |
| ------ | -------------------------------- |
| Answer | Eternity22                       |

![](<../../.gitbook/assets/Screenshot from 2020-08-23 23-16-36.png>)

## :closed\_lock\_with\_key: Level 2

### #1 SHA-256

| Hash   | F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 |
| ------ | ---------------------------------------------------------------- |
| Answer | paule                                                            |

```bash
echo 'F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85' > sha256.txt
hashcat -a 0 -m 1400 sha256.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 00-10-03.png>)



### #2 NTLM

| Hash   | 1DFECA0C002AE40B8619ECF94819CC1B |
| ------ | -------------------------------- |
| Answer | n63umy8lkf4i                     |

```bash
echo '1DFECA0C002AE40B8619ECF94819CC1B' > ntlm.txt
hashcat -a 0 -m 1000 ntlm.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 00-13-33.png>)



### #3 sha512crypt

| Hash   | $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02. |
| ------ | --------------------------------------------------------------------------------------------------------- |
| Answer | waka99                                                                                                    |

```bash
echo '$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.' > sha512.txt
hashcat -a 0 -m 1800 sha512.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 00-27-22.png>)



### #4 HMAC-SHA1

| Hash   | e5d8870e5bdd26602cab8dbe07a942c8669e56d6 |
| ------ | ---------------------------------------- |
| Salt   | tryhackme                                |
| Answer | 481616481616                             |

```bash
echo 'e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme' > sha1.txt
hashcat -a 0 -m 160 sha1.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-24 00-29-26.png>)

## :link: Support Material

{% embed url="https://hashcat.net/wiki/doku.php?id=example_hashes" %}

{% embed url="https://md5decrypt.net/en/Md4/" %}

