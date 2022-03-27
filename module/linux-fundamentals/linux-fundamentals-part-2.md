---
description: >-
  Continue your learning Linux journey with part two. You will be learning how
  to log in to a Linux machine using SSH, how to advance your commands, file
  system interaction.
---

# Linux Fundamentals Part 2

{% embed url="https://tryhackme.com/room/linuxfundamentalspart2" %}
https://tryhackme.com/room/linuxfundamentalspart2
{% endembed %}

## Task 3 Introduction to Flags and Switches

#### What directional arrow key would we use to navigate down the manual page?

{% hint style="success" %}
`down`
{% endhint %}

#### What flag would we use to display the output in a "human-readable" way?

{% hint style="success" %}
`-h`
{% endhint %}

## Task 4 Filesystem Interaction Continued

#### How would you create the file named "newnote"?

{% hint style="success" %}
`touch newnote`
{% endhint %}

#### On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory?

```bash
file unknown1
```

![](<../../.gitbook/assets/Screenshot from 2022-03-26 18-50-01.png>)

{% hint style="success" %}
`ASCII text`
{% endhint %}

#### How would we move the file "myfile" to the directory "myfolder"

{% hint style="success" %}
`mv myfile myfolder`
{% endhint %}

#### What are the contents of this file?

![](<../../.gitbook/assets/Screenshot from 2022-03-26 18-48-11.png>)

{% hint style="success" %}
`THM{FILESYSTEM}`
{% endhint %}

## Task 5 Permissions 101

#### On the deployable machine, who is the owner of "important"?

```bash
ls -l important
```

{% hint style="success" %}
`user2`
{% endhint %}

#### What would the command be to switch to the user "user2"?

{% hint style="success" %}
su user2
{% endhint %}

#### Now switch to this user "user2" using the password "user2"

```bash
su user2
```

#### Output the contents of "important", what is the flag?

```bash
cat important
```

![](<../../.gitbook/assets/Screenshot from 2022-03-26 18-56-42.png>)

{% hint style="success" %}
`THM{SU_USER2}`
{% endhint %}

## Task 6 Common Directories

#### What is the directory path that would we expect logs to be stored in?

{% hint style="success" %}
`/var/log`
{% endhint %}

#### What root directory is similar to how RAM on a computer works?

{% hint style="success" %}
`/tmp`
{% endhint %}

#### Name the home directory of the root user

{% hint style="success" %}
`/root`
{% endhint %}
