---
description: https://tryhackme.com/room/idor
---

# IDOR

## Task 1 What is an IDOR?

#### What does IDOR stand for?

{% hint style="success" %}
`Insecure Direct Object Reference`
{% endhint %}

## &#x20;Task 2 An IDOR Example

#### What is the Flag from the IDOR example website?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 07-29-02.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-08 07-29-41.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-08 07-29-57.png>)

{% hint style="success" %}
`THM{IDOR-VULN-FOUND}`
{% endhint %}

## Task 3 Finding IDORs in Encoded IDs

#### What is a common type of encoding used by websites?

{% hint style="success" %}
`base64`
{% endhint %}

## Task 4 Finding IDORs in Hashed IDs

#### What is a common algorithm used for hashing IDs?

{% hint style="success" %}
`md5`
{% endhint %}

## Task 5 Finding IDORs in Unpredictable IDs

#### What is the minimum number of accounts you need to create to check for IDORs between accounts?

{% hint style="success" %}
`2`
{% endhint %}

## Task 7 A Practical IDOR Example

![](<../../.gitbook/assets/Screenshot from 2022-03-08 19-45-48.png>)

#### What is the username for user id 1?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 19-46-39.png>)

{% hint style="success" %}
`adam84`
{% endhint %}

#### What is the email address for user id 3?

![](<../../.gitbook/assets/Screenshot from 2022-03-08 19-46-59.png>)

{% hint style="success" %}
`j@fakemail.thm`
{% endhint %}
