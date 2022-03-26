---
description: >-
  Embark on the journey of learning the fundamentals of Linux. Learn to run some
  of the first essential commands on an interactive terminal.
---

# Linux Fundamentals Part 1

{% embed url="https://tryhackme.com/room/linuxfundamentalspart1" %}
https://tryhackme.com/room/linuxfundamentalspart1
{% endembed %}

## Task 2 A Bit of Background on Linux

#### Research: What year was the first release of a Linux operating system?

{% hint style="success" %}
`1991`
{% endhint %}

## Task 4 Running Your First few Commands

#### If we wanted to output the text "TryHackMe", what would our command be?

{% hint style="success" %}
`echo TryHackMe`
{% endhint %}

#### What is the username of who you're logged in as on your deployed Linux machine?

![](<../../.gitbook/assets/Screenshot from 2022-03-26 11-43-31.png>)

{% hint style="success" %}
`tryhackme`
{% endhint %}

## Task 5 Interacting With the Filesystem!

#### On the Linux machine that you deploy, how many folders are there?

```bash
ls -lA
```

![](<../../.gitbook/assets/Screenshot from 2022-03-26 11-54-21.png>)

{% hint style="success" %}
`4`
{% endhint %}

#### Which directory contains a file?

```bash
ls -lA folder*
```

![](<../../.gitbook/assets/Screenshot from 2022-03-26 11-55-17.png>)

{% hint style="success" %}
`folder4`
{% endhint %}

#### What is the contents of this file?

```bash
cat folder4/note.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-26 11-56-35.png>)

{% hint style="success" %}
`Hello World!`
{% endhint %}

#### Use the cd command to navigate to this file and find out the new current working directory. What is the path?

```bash
cd folder4
pwd
```

![](<../../.gitbook/assets/Screenshot from 2022-03-26 11-57-39.png>)

{% hint style="success" %}
`/home/tryhackme/folder4`
{% endhint %}

## Task 6 Searching for Files

#### Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag?

```bash
egrep -o 'THM{[^}]*}' access.log
```

{% hint style="success" %}
`THM{ACCESS}`
{% endhint %}

## Task 7 An Introduction to Shell Operators

#### If we wanted to run a command in the background, what operator would we want to use?

{% hint style="success" %}
`&`
{% endhint %}

#### If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?

{% hint style="success" %}
`echo password123 > passwords`
{% endhint %}

#### Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be

{% hint style="success" %}
`echo tryhackme >> passwords`
{% endhint %}
