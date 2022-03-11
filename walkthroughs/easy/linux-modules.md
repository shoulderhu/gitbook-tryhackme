---
description: https://tryhackme.com/room/linuxmodules
---

# Linux Modules

## Task 3 Grep, Egrep, Fgrep

#### Is there a difference between egrep and fgrep?

{% hint style="success" %}
`Yea`
{% endhint %}

#### Which flag do you use to list out all the lines NOT containing the 'PATTERN'?

{% hint style="success" %}
`-v`
{% endhint %}

#### Download the above given file and answer the following questions.

#### What user did you find in that file?

```bash
grep -i user grep.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-10 07-27-37.png>)

{% hint style="success" %}
`bobthebuilder`
{% endhint %}

#### What is the password of that user?

```bash
grep -i pass grep.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-10 07-28-23.png>)

{% hint style="success" %}
`LinuxIsGawd`
{% endhint %}

#### Can you find the comment that user just left?

```bash
grep -i comment grep.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-10 07-30-00.png>)

{% hint style="success" %}
`fs0ciety`
{% endhint %}

## Task 5 tr

## Task 14 Is it night yet?

#### Press F to pay respect

{% hint style="success" %}
`F`
{% endhint %}
