---
description: https://tryhackme.com/room/httpindetail
---

# HTTP in detail

{% embed url="https://tryhackme.com/room/httpindetail" %}
https://tryhackme.com/room/httpindetail
{% endembed %}

## Task 1 What is HTTP(S)?

#### What does HTTP stand for?

{% hint style="success" %}
`HyperText Transfer Protocol`
{% endhint %}

#### What does the S in HTTPS stand for?

{% hint style="success" %}
`Secure`
{% endhint %}

#### On the mock webpage on the right there is an issue, once you've found it, click on it. What is the challenge flag?

![](<../../.gitbook/assets/Screenshot from 2022-03-26 10-13-13.png>)

{% hint style="success" %}
`THM{INVALID_HTTP_CERT}`
{% endhint %}

## Task 2 Requests And Responses

#### What HTTP protocol is being used in the above example?

{% hint style="success" %}
`HTTP/1.1`
{% endhint %}

#### What response header tells the browser how much data to expect?

{% hint style="success" %}
`Content-Length`
{% endhint %}

## Task 3 HTTP Methods

#### What method would be used to create a new user account?

{% hint style="success" %}
`POST`
{% endhint %}

#### What method would be used to update your email address?

{% hint style="success" %}
`PUT`
{% endhint %}

#### What method would be used to remove a picture you've uploaded to your account?

{% hint style="success" %}
`DELETE`
{% endhint %}

#### What method would be used to view a news article?

{% hint style="success" %}
`GET`
{% endhint %}

## Task 4 HTTP Status Codes

#### What response code might you receive if you've created a new user or blog post article?

{% hint style="success" %}
`201`
{% endhint %}

#### What response code might you receive if you've tried to access a page that doesn't exist?

{% hint style="success" %}
`404`
{% endhint %}

#### What response code might you receive if the web server cannot access its database and the application crashes?

{% hint style="success" %}
`503`
{% endhint %}

#### What response code might you receive if you try to edit your profile without logging in first?

{% hint style="success" %}
`401`
{% endhint %}

## Task 5 Headers

#### What header tells the web server what browser is being used?

{% hint style="success" %}
`User-Agent`
{% endhint %}

#### What header tells the browser what type of data is being returned?

{% hint style="success" %}
`Content-Type`
{% endhint %}

#### What header tells the web server which website is being requested?

{% hint style="success" %}
`Host`
{% endhint %}

## Task 6 Cookies

#### Which header is used to save cookies to your computer?

{% hint style="success" %}
`Set-Cookie`
{% endhint %}

## Task 7 Making Requests

#### Make a GET request to /room

![](<../../.gitbook/assets/Screenshot from 2022-03-26 10-52-11.png>)

{% hint style="success" %}
`THM{YOU'RE_IN_THE_ROOM}`
{% endhint %}

#### Make a GET request to /blog and using the gear icon set the id parameter to 1 in the URL field

![](<../../.gitbook/assets/Screenshot from 2022-03-26 10-53-37.png>)

{% hint style="success" %}
`THM{YOU_FOUND_THE_BLOG}`
{% endhint %}

#### Make a DELETE request to /user/1

![](<../../.gitbook/assets/Screenshot from 2022-03-26 10-54-08.png>)

{% hint style="success" %}
`THM{USER_IS_DELETED}`
{% endhint %}

#### Make a PUT request to /user/2 with the username parameter set to admin

![](<../../.gitbook/assets/Screenshot from 2022-03-26 10-54-49.png>)

{% hint style="success" %}
`THM{USER_HAS_UPDATED}`
{% endhint %}

#### POST the username of thm and a password of letmein to /login

![](<../../.gitbook/assets/Screenshot from 2022-03-26 10-55-47.png>)

{% hint style="success" %}
`THM{HTTP_REQUEST_MASTER}`
{% endhint %}
