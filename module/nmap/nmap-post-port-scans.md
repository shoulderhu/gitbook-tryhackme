---
description: https://tryhackme.com/room/nmap04
---

# Nmap Post Port Scans

## Task 2 Service Detection

#### Start the target machine for this task and launch the AttackBox. Run `nmap -sV --version-light MACHINE_IP`via the AttackBox. What is the detected version for port 143?

```bash
nmap -n -sV --version-light 10.10.169.199
```

![nmap -n -sV --version-light 10.10.169.199](<../../.gitbook/assets/Screenshot from 2022-02-19 18-51-44.png>)

{% hint style="success" %}
`Dovecot imapd`
{% endhint %}

#### Which service did not have a version detected with `--version-light`?

{% hint style="success" %}
`rpcbind`
{% endhint %}

## Task 3 OS Detection and Traceroute

#### Run `nmap` with `-O` option against `10.10.169.199`. What OS did Nmap detect?

```bash
sudo nmap -n -O 10.10.169.199
```

![sudo nmap -n -O 10.10.169.199](<../../.gitbook/assets/Screenshot from 2022-02-19 18-59-54.png>)

{% hint style="success" %}
`linux`
{% endhint %}

## Task 4 Nmap Scripting Engine (NSE)

#### Knowing that Nmap scripts are saved in `/usr/share/nmap/scripts` on the AttackBox. What does the script `http-robots.txt` check for?

```bash
nmap --script-help=http-robots.txt
```

![nmap --script-help=http-robots.txt](<../../.gitbook/assets/Screenshot from 2022-02-19 19-38-27.png>)

{% hint style="success" %}
`disallowed entries`
{% endhint %}

#### Can you figure out the name for the script that checks for the remote code execution vulnerability MS15-034 (CVE2015-2015-1635)?

```bash
grep -R 'MS15-034'  /usr/share/nmap/scripts/
```

![grep -R 'MS15-034' /usr/share/nmap/scripts/](<../../.gitbook/assets/Screenshot from 2022-02-19 19-41-46.png>)

{% hint style="success" %}
`http-vuln-cve2015-1635`
{% endhint %}

#### Launch the AttackBox if you haven't already. After you ensure you have terminated the VM from Task 2, start the target machine for this task. On the AttackBox, run Nmap with the default scripts `-sC` against `10.10.5.180`. You will notice that there is a service listening on port 53. What is its full version value?

```bash
nmap -n -p53 -sC 10.10.5.180
```

![nmap -n -p53 -sC 10.10.5.180](<../../.gitbook/assets/Screenshot from 2022-02-19 19-47-43.png>)

{% hint style="success" %}
`9.9.5-9+deb8u19-Debian`
{% endhint %}

#### Based on its description, the script `ssh2-enum-algos` “reports the number of algorithms (for encryption, compression, etc.) that the target SSH2 server offers.” What is the name of the key exchange algorithms (kex\_algorithms) that relies upon “sha1” and is supported by `10.10.5.180`?

```bash
nmap -n -p22 --script=ssh2-enum-logs 10.10.5.180
```

![nmap -n -p22 --script=ssh2-enum-logs 10.10.5.180](<../../.gitbook/assets/Screenshot from 2022-02-19 19-50-30.png>)

{% hint style="success" %}
`diffie-hellman-group14-sha1`
{% endhint %}

## Task 5 Saving the Output

#### Terminate the target machine of the previous task and start the target machine for this task. On the AttackBox terminal, issue the command `scp pentester@MACHINE_IP:/home/pentester/* .` to download the Nmap reports in normal and grepable formats from the target virtual machine.

#### Note that the username `pentester` has the password `THM17577`

```bash
scp pentester@10.10.53.105:/home/pentester/* . 
```

![scp pentester@10.10.53.105:/home/pentester/\* .](<../../.gitbook/assets/Screenshot from 2022-02-19 20-00-58.png>)

#### Check the attached Nmap logs. How many systems are listening on the HTTPS port?

```bash
cat scan_172_17_network.gnmap | grep https
```

![cat scan\_172\_17\_network.gnmap | grep https](<../../.gitbook/assets/Screenshot from 2022-02-19 20-03-17.png>)

{% hint style="success" %}
3
{% endhint %}

#### What is the IP address of the system listening on port 8089?

```bash
cat scan_172_17_network.gnmap | grep 8089
```

![cat scan\_172\_17\_network.gnmap | grep 8089](<../../.gitbook/assets/Screenshot from 2022-02-19 20-04-37.png>)

{% hint style="success" %}
`172.17.20.147`
{% endhint %}
