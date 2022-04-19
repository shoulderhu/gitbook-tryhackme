# Encryption - Crypto 101

{% embed url="https://tryhackme.com/room/encryptioncrypto101" %}
https://tryhackme.com/room/encryptioncrypto101
{% endembed %}

## Task 2 Key terms

#### Are SSH keys protected with a passphrase or a password?

{% hint style="success" %}
`Passphrase`
{% endhint %}

## Task 3 Why is Encryption important?

#### What does SSH stand for?

{% hint style="success" %}
`Secure Shell`
{% endhint %}

#### How do webservers prove their identity?

{% hint style="success" %}
`Certificate`
{% endhint %}

#### What is the main set of standards you need to comply with if you store or process payment card details?

{% hint style="success" %}
`PCI-DSS`
{% endhint %}

## Task 4 Crucial Crypto Maths

#### What's 30 % 5?

{% hint style="success" %}
`0`
{% endhint %}

#### What's 25 % 7

{% hint style="success" %}
`4`
{% endhint %}

#### What's 118613842 % 9091

{% hint style="success" %}
`3565`
{% endhint %}

## Task 5 Types of Encryption

#### Should you trust DES?

{% hint style="success" %}
`Nay`
{% endhint %}

#### What was the result of the attempt to make DES more secure so that it could be used for longer?

{% hint style="success" %}
`Triple DES`
{% endhint %}

#### Is it ok to share your public key?

{% hint style="success" %}
`Yea`
{% endhint %}

## Task 6 RSA - Rivest Shamir Adleman

#### p = 4391, q = 6659. What is n?

{% hint style="success" %}
`29239669`
{% endhint %}

## Task 8 Digital signatures and Certificates

#### Who is TryHackMe's HTTPS certificate issued by?

![](<../../.gitbook/assets/Screenshot from 2022-04-19 05-14-15.png>)

{% hint style="success" %}
`E1`
{% endhint %}

## Task 9 SSH Authentication

#### What algorithm does the key use?

```bash
cat idrsa.id_rsa
```

![](<../../.gitbook/assets/Screenshot from 2022-04-19 05-26-22.png>)

{% hint style="success" %}
`RSA`
{% endhint %}

#### Crack the password with John The Ripper and rockyou, what's the passphrase for the key?

```bash
ssh2john idrsa.id_rsa > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-19 05-27-28.png>)

{% hint style="success" %}
`delicious`
{% endhint %}

## Task 10 Explaining Diffie Hellman Key Exchange

#### You have the private key, and a file encrypted with the public key. Decrypt the file. What's the secret word?

```bash
gpg --import tryhackme.key
gpg -d message.gpg
```

{% hint style="success" %}
`Pineapple`
{% endhint %}
