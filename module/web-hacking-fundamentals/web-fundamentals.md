# Web Fundamentals

{% embed url="https://tryhackme.com/room/webfundamentals" %}
https://tryhackme.com/room/webfundamentals
{% endembed %}

## Task 2 How do we load websites?

#### What request verb is used to retrieve page content?

{% hint style="success" %}
GET
{% endhint %}

#### What port do web servers normally listen on?

{% hint style="success" %}
80
{% endhint %}

#### What's responsible for making websites look fancy?

{% hint style="success" %}
CSS
{% endhint %}

## Task 3 More HTTP - Verbs and request formats

#### What verb would be used for a login?

{% hint style="success" %}
POST
{% endhint %}

#### What verb would be used to see your bank balance once you're logged in?

{% hint style="success" %}
GET
{% endhint %}

#### Does the body of a GET request matter?

{% hint style="success" %}
Nay
{% endhint %}

#### **What's the status code for "I'm a teapot"?**

![](<../../.gitbook/assets/Screenshot from 2022-04-16 05-17-11.png>)

{% hint style="success" %}
418
{% endhint %}

#### What status code will you get if you need to authenticate to access some content, and you're unauthenticated?

{% hint style="success" %}
401
{% endhint %}

## Task 5 Mini CTF

#### What's the GET flag?

```bash
curl -w '\n' http://10.10.100.169:8081/ctf/get
```

![](<../../.gitbook/assets/Screenshot from 2020-09-10 12-10-30.png>)

{% hint style="success" %}
`thm{162520bec925bd7979e9ae65a725f99f}`
{% endhint %}

#### What's the POST flag?

```bash
curl -d flag_please -w '\n' http://10.10.100.169:8081/ctf/post
```

![](<../../.gitbook/assets/Screenshot from 2020-09-10 12-12-23.png>)

{% hint style="success" %}
`thm{3517c902e22def9c6e09b99a9040ba09}`
{% endhint %}

#### **What's the "Get a cookie" flag?**

```bash
curl -v -w '\n' http://10.10.100.169:8081/ctf/getcookie
```

![](<../../.gitbook/assets/Screenshot from 2020-09-10 12-15-38.png>)

{% hint style="success" %}
`thm{91b1ac2606f36b935f465558213d7ebd}`
{% endhint %}

#### What's the "Set a cookie" flag?

```bash
curl --cookie 'flagpls=flagpls' -w '\n' http://10.10.100.169:8081/ctf/sendcookie
```

![](<../../.gitbook/assets/Screenshot from 2020-09-10 12-17-29.png>)

{% hint style="success" %}
`thm{c10b5cb7546f359d19c747db2d0f47b3}`
{% endhint %}
