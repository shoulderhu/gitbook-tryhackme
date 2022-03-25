---
description: https://tryhackme.com/room/cryptographyfordummies
---

# Cryptography for Dummies

## Task 2 Types of cryptography

#### What type of cryptography is more secure?

{% hint style="success" %}
`Asymmetric`
{% endhint %}

#### What type of cryptography is faster?

{% hint style="success" %}
`Symmetric`
{% endhint %}

#### What type of cryptography will a Bank site use?

{% hint style="success" %}
`Asymmetric`
{% endhint %}

#### What will you use to encrypt your messages in asymmetric cryptography?

{% hint style="success" %}
`public key`
{% endhint %}

#### What will you use to decrypt messages in asymmetric cryptography?

{% hint style="success" %}
`private key`
{% endhint %}

#### Does symmetric cryptography use two different keys for encryption/decryption?

{% hint style="success" %}
`nay`
{% endhint %}

## Task 3 What is a hash?

#### What's the MD5 hash of "hashes are cool"?

```bash
echo -n 'hashes are cool' | md5sum
```

![](<../../.gitbook/assets/Screenshot from 2022-03-25 21-06-40.png>)

{% hint style="success" %}
`f762d32e3c160900d94b683e927555b9`
{% endhint %}

#### What does MD5 stand for?

{% hint style="success" %}
`Message Digest 5`
{% endhint %}

#### Who created MD5?

{% hint style="success" %}
`Ronald Rivest`
{% endhint %}

## Task 4 Decoding/encoding

#### Encode the string "cryptographyisuseful" with Base64

```bash
echo -n 'cryptographyisuseful' | base64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-25 21-09-53.png>)

{% hint style="success" %}
`Y3J5cHRvZ3JhcGh5aXN1c2VmdWw=`
{% endhint %}

#### Decode the string "dGhlIHNlY3JldCB3b3JkIGlzIDogd2F0ZXJtZWxvbg==". What's the secret word?

```bash
echo -n 'dGhlIHNlY3JldCB3b3JkIGlzIDogd2F0ZXJtZWxvbg==' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-03-25 21-10-52.png>)

{% hint style="success" %}
`watermelon`
{% endhint %}
