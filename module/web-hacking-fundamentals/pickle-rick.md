# Pickle Rick

{% embed url="https://tryhackme.com/room/picklerick" %}
https://tryhackme.com/room/picklerick
{% endembed %}

![](<../../.gitbook/assets/Pickle Rick.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-49-59.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-53-58.png>)

## Task 1 Pickle Rick

#### What is the first ingredient Rick needs?

```bash
rustscan -a 10.10.52.110 -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-58-18.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-58-47.png>)

```bash
gobuster dir -u http://10.10.52.110/ \
             -w /usr/share/dirb/wordlists/common.txt -t128 
gobuster dir -u http://10.10.52.110/ \
             -w /usr/share/dirb/wordlists/common.txt -x php -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-55-18.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-22-44.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-57-09.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-26-53.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-27-59.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-28-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-53-56.png>)

{% hint style="success" %}
`mr. meeseek hair`
{% endhint %}

#### What's the second ingredient Rick needs?

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-53-28.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-55-53.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 06-56-22.png>)

{% hint style="success" %}
`1 jerry tear`
{% endhint %}

![](<../../.gitbook/assets/Screenshot from 2022-04-16 07-16-57.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 07-18-14.png>) ![](<../../.gitbook/assets/Screenshot from 2022-04-16 07-18-44.png>)

```bash
```



#### What's the final ingredient Rick needs?

{% hint style="success" %}

{% endhint %}

