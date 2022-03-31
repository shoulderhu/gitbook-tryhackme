# SSRF

{% embed url="https://tryhackme.com/room/ssrfqi" %}
https://tryhackme.com/room/ssrfqi
{% endembed %}

## Task 1 What is an SSRF?

#### What is an SSRF?

{% hint style="success" %}
`Server-Side Request Forgery`
{% endhint %}

#### As opposed to a regular SSRF, what is the other type?

{% hint style="success" %}
`Blind`
{% endhint %}

## Task 2 SSRF Examples

#### What is the flag from the SSRF Examples site?

![](<../../.gitbook/assets/Screenshot from 2022-03-31 19-41-31.png>)

{% hint style="success" %}
`THM{SSRF_MASTER}`
{% endhint %}

## Task 3 Finding an SSRF

#### What website can be used to catch HTTP requests from a server?

{% hint style="success" %}
`requestbin.com`
{% endhint %}

## Task 4 Defeating Common SSRF Defenses

#### Open Redirect

An open redirect is an endpoint on the server where the website visitor gets automatically redirected to another website address. Take, for example, the link https://website.thm/link?url=https://tryhackme.com. This endpoint was created to record the number of times visitors have clicked on this link for advertising/marketing purposes.

#### What method can be used to bypass strict rules?

{% hint style="success" %}
`Open Redirect`
{% endhint %}

#### What IP address may contain sensitive data in a cloud environment?

{% hint style="success" %}
`169.254.169.254`
{% endhint %}

#### What type of list is used to **permit** only certain input?

{% hint style="success" %}
`Allow List`
{% endhint %}

#### What type of list is used to **stop** certain input?

{% hint style="success" %}
`Deny List`
{% endhint %}

## Task 5 SSRF Practical

#### What is the flag from the /private directory?

![](<../../.gitbook/assets/Screenshot from 2022-03-31 20-06-44.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-31 20-11-34.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-31 20-12-02.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-31 20-13-03.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-31 20-14-59.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-31 20-15-15.png>)

{% hint style="success" %}
`THM{YOU_WORKED_OUT_THE_SSRF}`
{% endhint %}
