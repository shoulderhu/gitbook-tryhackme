# OWASP Juice Shop

## Task 2 Let's go on an adventure!

#### **What's the Administrator's email address?**&#x20;

The reviews show each user's email address. Which, by clicking on the Apple Juice product, shows us the Admin email!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-18-39.png>)

{% hint style="success" %}
`admin@juice-sh.op`
{% endhint %}

#### **What paramater is used for searching?**

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-13-32.png>)

{% hint style="success" %}
`q`
{% endhint %}

#### **What show does Jim reference in his review?**

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-17-20.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-14-42.png>)

{% hint style="success" %}
`Star Trek`
{% endhint %}

## **Task 3** Inject the juice

#### **Log into the administrator account!**

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-21-41.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-20-51.png>)

{% hint style="success" %}
`32a5e0f21372bcc1000a6088b93b458e41f0e02a`
{% endhint %}

#### **Log into the Bender account!**

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-28-57.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-25-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-26-07.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-26-37.png>)

{% hint style="success" %}
`fb364762a3c102b2db932069c0e6b78e738d4066`
{% endhint %}

## Task 4 Who broke my lock?!

#### Bruteforce the Administrator account's password!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-45-01.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-46-28.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-45-35.png>)

{% hint style="success" %}
`c2110d06dc6f81c67cd8099ff0ba601241f1ac0e`
{% endhint %}

#### Reset Jim's password!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-50-45.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-41-11.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-41-37.png>)

{% hint style="success" %}
`094fbc9b48e525150ba97d05b942bbf114987257`
{% endhint %}

## Task 5 AH! Don't look!

#### Access the Confidential Document!

```bash
curl http://10.10.184.117/ftp/acquisitions.md
```

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-48-26.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-36-20.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-50-14.png>)

{% hint style="success" %}
`edf9281222395a1c5fee9b89e32175f1ccf50c5b`
{% endhint %}

#### Log into MC SafeSearch's account!

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-55-39.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-55-58.png>)

{% hint style="success" %}
`66bdcffad9e698fd534003fbb3cc7e2b7b55d7f0`
{% endhint %}

#### Download the Backup file!

A Poison Null Byte is actually a NULL terminator. By placing a NULL character in the string at a certain byte, the string will tell the server to terminate at that point, nulling the rest of the string.

```
wget 'http://10.10.184.117/ftp/package.json.bak%2500.md'
```

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-58-54.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-03-14.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 11-59-07.png>)

{% hint style="success" %}
`bfc1e6b4a16579e85e06fee4c36ff8c02fb13795`
{% endhint %}

## Task 6 Who's flying this thing?

#### Access the administration page!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-31-30.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 12-09-11.png>)

{% hint style="success" %}
`946a799363226a24822008503f5d1324536629a0`
{% endhint %}

#### View another user's shopping basket!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-26-31.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 12-12-33.png>)

{% hint style="success" %}
`41b997a36cc33fbe4f0ba018474e19ae5ce52121`
{% endhint %}

#### Remove all 5-star reviews!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-33-10.png>)

{% hint style="success" %}
`50c97bcce0b895e446d61c83a21df371ac2266ef`
{% endhint %}

## **Task 7** Where did that come from?

#### Perform a DOM XSS!

```
<iframe src="javascript:alert(`xss`)"> 
```

![](<../../.gitbook/assets/Screenshot from 2022-04-17 12-18-27.png>)

{% hint style="success" %}
`9aaf4bbea5c30d00a1f5bbcfce4db6d4b0efe0bf`
{% endhint %}

#### Perform a persistent XSS!

The _True-Client-IP_  header is similar to the _X-Forwarded-For_ header, both tell the server or proxy what the IP of the client is. Due to there being no sanitation in the header we are able to perform an XSS attack.&#x20;

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-55-05.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-55-48.png>)

{% hint style="success" %}
`149aa8ce13d7a4a8a931472308e269c94dc5f156`
{% endhint %}

#### Perform a reflected XSS!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-51-52.png>)

{% hint style="success" %}
`23cefee1527bde039295b2616eeb29e1edc660a0`
{% endhint %}

## Task 8 Exploration!

**Access the /#/score-board/ page**

![](<../../.gitbook/assets/Screenshot from 2020-08-30 22-03-06.png>)

{% hint style="success" %}
`7efd3174f9dd5baa03a7882027f2824d2f72d86e`
{% endhint %}
