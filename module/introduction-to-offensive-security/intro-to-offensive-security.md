# Intro to Offensive Security

{% embed url="https://tryhackme.com/room/introtooffensivesecurity" %}
https://tryhackme.com/room/introtooffensivesecurity
{% endembed %}

## Task 1 Hacking your first machine

```bash
nmap -n -sVC 10.10.176.168
```

![](<../../.gitbook/assets/Screenshot from 2022-05-04 05-28-08.png>)

![](<../../.gitbook/assets/Screenshot from 2022-05-04 05-28-26.png>)

```bash
gobuster dir -u http://10.10.176.168/ \
             -w wordlist.txt \
             -t128 
```

#### When you've transferred money to your account, go back to your bank account page. What is the answer shown on your bank balance page?

![](<../../.gitbook/assets/Screenshot from 2022-05-04 05-36-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-05-04 05-37-31.png>)

{% hint style="success" %}
`BANK-HACKED`
{% endhint %}
