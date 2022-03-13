---
description: https://tryhackme.com/room/johntheripper0
---

# John The Ripper

## Task 2 Setting Up John the Ripper

#### What is the most popular extended version of John the Ripper?

{% hint style="success" %}
`Jumbo John`
{% endhint %}

## Task 3 Wordlists

#### What website was the rockyou.txt wordlist created from a breach on?

{% hint style="success" %}
`rockyou.com`
{% endhint %}

## Task 4 Cracking Basic Hashes

```bash
unzip firsttaskhashes.zip
cd firsttaskhashes/
```

#### What type of hash is hash1.txt?

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-12-19.png>)

```bash
cat hash1.txt | hash-identifier
```

{% hint style="success" %}
`MD5`
{% endhint %}

#### What is the cracked value of hash1.txt?

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-14-24.png>)

```bash
john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
```

{% hint style="success" %}
`biscuit`
{% endhint %}

#### What type of hash is hash2.txt?

```bash
cat hash2.txt | hash-identifier 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-16-32.png>)

{% hint style="success" %}
`SHA1`
{% endhint %}

#### What is the cracked value of hash2.txt

```bash
john --format=Raw-SHA1 --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-17-45.png>)

{% hint style="success" %}
`kangeroo`
{% endhint %}

#### What type of hash is hash3.txt?

```bash
cat hash3.txt | hash-identifier
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-19-54.png>)

{% hint style="success" %}
`SHA256`
{% endhint %}

#### What is the cracked value of hash3.txt

```bash
john --format=Raw-SHA256 --wordlist=/usr/share/wordlists/rockyou.txt hash3.txt  
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-20-38.png>)

{% hint style="success" %}
`microphone`
{% endhint %}

#### What type of hash is hash4.txt?

```bash
cat hash4.txt | hash-identifier
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-22-26.png>)

{% hint style="success" %}
`Whirlpool`
{% endhint %}

#### What is the cracked value of hash4.txt

```bash
john --format=whirlpool --wordlist=/usr/share/wordlists/rockyou.txt hash4.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-23-52.png>)

{% hint style="success" %}
`colossal`
{% endhint %}

## Task 5 Cracking Windows Authentication Hashes

#### What do we need to set the "format" flag to, in order to crack this?

{% hint style="success" %}
`NT`
{% endhint %}

#### What is the cracked value of this password?

```bash
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt ntlm.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-47-15.png>)

{% hint style="success" %}
`mushroom`
{% endhint %}

## Task 6 Cracking /etc/shadow Hashes

#### What is the root password?

```bash
cat etchashes.txt | sed -n '3p' > passwd
cat etchashes.txt | sed -n '4p' > shadow
unshadow passwd shadow > crackme
john --wordlist=/usr/share/wordlists/rockyou.txt crackme 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 18-56-59.png>)

{% hint style="success" %}
`1234`
{% endhint %}

## Task 7 Single Crack Mode

```bash
awk '{print "Joker:" $0}' hash7.txt > hash.txt
cat hash7.txt | hash-identifier
john --format=Raw-MD5 --single hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-09-53.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-10-36.png>)

{% hint style="success" %}
`Jok3r`
{% endhint %}

## Task 8 Custom Rules

#### What do custom rules allow us to exploit?

{% hint style="success" %}
`password complexity predictability`
{% endhint %}

#### What rule would we use to add all capital letters to the end of the word?

{% hint style="success" %}
`Az"[A-Z]"`
{% endhint %}

#### What flag would we use to call a custom rule called "THMRules"

{% hint style="success" %}
`--rule=THMRules`
{% endhint %}

## Task 9 Cracking Password Protected Zip Files

#### What is the password for the secure.zip file?

```bash
zip2john secure.zip > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-47-27.png>)

{% hint style="success" %}
`pass123`
{% endhint %}

#### What is the contents of the flag inside the zip file?

```bash
unzip secure.zip
cat zippy/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-48-35.png>)

{% hint style="success" %}
`THM{w3ll_d0n3_h4sh_r0y4l}`
{% endhint %}

## Task 10 Cracking Password Protected RAR Archives

#### What is the password for the secure.rar file?

```bash
rar2john secure.rar > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-54-12.png>)

{% hint style="success" %}
`password`
{% endhint %}

#### What is the contents of the flag inside the zip file?

```bash
unrar e secure.rar
cat flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-54-48.png>)

{% hint style="success" %}
`THM{r4r_4rch1ve5_th15_t1m3}`
{% endhint %}

## Task 11 Cracking SSH Keys with John

#### What is the SSH private key password?

```bash
ssh2john idrsa.id_rsa > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-05 19-58-50.png>)

{% hint style="success" %}
`mango`
{% endhint %}
