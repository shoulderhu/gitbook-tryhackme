# Hashing - Crypto 101

{% embed url="https://tryhackme.com/room/hashingcrypto101" %}
https://tryhackme.com/room/hashingcrypto101
{% endembed %}

## Task 1 Key Terms

#### Is base64 encryption or encoding?

{% hint style="success" %}
`encoding`
{% endhint %}

## Task 2 What is a hash function?

#### **What is the output size in bytes of the MD5 hash function?**

{% hint style="success" %}
`16`
{% endhint %}

#### Can you avoid hash collisions?

{% hint style="success" %}
`Nay`
{% endhint %}

#### **If you have an 8 bit hash output, how many possible hashes are there?**

{% hint style="success" %}
`256`
{% endhint %}

## Task 3 Uses for hashing

#### Crack the hash "d0199f51d2728db6011945145a1b607a" using the rainbow table manually.

```
echo -n 'd0199f51d2728db6011945145a1b607a' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 08-51-44.png>)

{% hint style="success" %}
`basketball`
{% endhint %}

#### **Crack the hash "5b31f93c09ad1d065c0491b764d04933" using online tools**

![](<../../.gitbook/assets/Screenshot from 2020-09-14 08-55-25.png>)

{% hint style="success" %}
`tryhackme`
{% endhint %}

#### **Should you encrypt passwords?**

{% hint style="success" %}
`Nay`
{% endhint %}

## Task 4 Recognising password hashes

#### How many rounds does sha512crypt ($6$) use by default?

{% hint style="success" %}
`5000`
{% endhint %}

#### **What's the hashcat example hash for Citrix Netscaler hashes?**

{% hint style="success" %}
`1765058016a22f1b4e076dccd1c3df4e8e5c0839ccded98ea`
{% endhint %}

#### How long is a Windows NTLM hash, in characters?

{% hint style="success" %}
`32`
{% endhint %}

## Task 5 Password Cracking

#### **Crack this hash: $2a$06$7yoU3Ng8dHTXphAg913cyO6Bjs3K5lBnwq5FJyA6d01pMSrddr1ZG**

```
echo -n '$2a$06$7yoU3Ng8dHTXphAg913cyO6Bjs3K5lBnwq5FJyA6d01pMSrddr1ZG' > bcrypt.txt
hashcat -a 0 -m 3200 bcrypt.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 09-17-51.png>)

{% hint style="success" %}
`85208520`
{% endhint %}

#### Crack this hash: 9eb7ee7f551d2f0ac684981bd1f1e2fa4a37590199636753efe614d4db30e8e1

```
echo -n '9eb7ee7f551d2f0ac684981bd1f1e2fa4a37590199636753efe614d4db30e8e1' > sha256.txt
hashcat -a 0 -m 1400 sha256.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 09-20-36.png>)

{% hint style="success" %}
`halloween`
{% endhint %}

#### Crack this hash: $6$GQXVvW4EuM$ehD6jWiMsfNorxy5SINsgdlxmAEl3.yif0/c3NqzGLa0P.S7KRDYjycw5bnYkF5ZtB8wQy8KnskuWQS3Yr1wQ0

```
echo -n '$6$GQXVvW4EuM$ehD6jWiMsfNorxy5SINsgdlxmAEl3.yif0/c3NqzGLa0P.S7KRDYjycw5bnYkF5ZtB8wQy8KnskuWQS3Yr1wQ0' > sha512crypt.txt
hashcat -a 0 -m 1800 sha512crypt.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-09-14 09-22-14.png>)

{% hint style="success" %}
`spaceman`
{% endhint %}

#### **Crack this hash: b6b0d451bbf6fed658659a9e7e5598fe**

![](<../../.gitbook/assets/Screenshot from 2020-09-14 09-25-45.png>)

{% hint style="success" %}
`funforyou`
{% endhint %}

## Task 6 Hashing for integrity checking

#### What's the SHA1 sum for the amd64 Kali 2019.4 ISO?

![](<../../.gitbook/assets/Screenshot from 2020-09-14 09-33-42.png>)

{% hint style="success" %}
`186c5227e24ceb60deb711f1bdc34ad9f4718ff9`
{% endhint %}

#### **What's the hashcat mode number for HMAC-SHA512 (key = $pass)?**

{% hint style="success" %}
`1750`
{% endhint %}
