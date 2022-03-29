---
description: https://tryhackme.com/room/phishingemails1tryoe
---

# Phishing Emails 1

## Task 2 The Email Address

#### Email dates back to what time frame?

{% hint style="success" %}
`1970s`
{% endhint %}

## Task 3 Email Delivery

{% embed url="https://www.blazingfibre.net/tech/email_ssl.htm" %}

#### What port is classified as Secure Transport for SMTP?

{% hint style="success" %}
`465`
{% endhint %}

#### What port is classified as Secure Transport for IMAP?

{% hint style="success" %}
`993`
{% endhint %}

#### What port is classified as Secure Transport for POP3?

{% hint style="success" %}
`995`
{% endhint %}

## Task 4 Email Headers

{% embed url="https://mediatemple.net/community/products/all/204643950/understanding-an-email-header" %}

#### What email header is the same as "Reply-to"?

![](<../../.gitbook/assets/Screenshot from 2022-03-20 12-56-15 (1).png>)

{% hint style="success" %}
`Return-Path`
{% endhint %}

#### Once you find the email sender's IP address, where can you retrieve more information about the IP?

![](<../../.gitbook/assets/Screenshot from 2022-03-20 12-56-50.png>)

{% hint style="success" %}
`http://www.arin.net`
{% endhint %}

## Task 5 Email Body

#### In the above screenshots, what is the URI of the blocked image?

![](<../../.gitbook/assets/image (4) (1).png>)

{% hint style="success" %}
`https://i.imgur.com/LSWOtDI.png`
{% endhint %}

#### In the above screenshots, what is the name of the PDF attachment?

![](<../../.gitbook/assets/image (1).png>)

{% hint style="success" %}
`Payment-updateid.pdf`
{% endhint %}

#### In the attached virtual machine, view the information in email2.txt and reconstruct the PDF using the base64 data. What is the text within the PDF?

```bash
cat email2.txt | tail -n621 | head -n619 | base64 -d > zmqpalgh.pdf
```

![](<../../.gitbook/assets/Screenshot from 2022-03-20 13-09-12.png>)

{% hint style="success" %}
`THM{BENIGN_PDF_ATTACHMENT}`
{% endhint %}

## Task 6 Types of Phishing

![](<../../.gitbook/assets/Screenshot from 2022-03-20 13-21-23.png>)

#### What trusted entity is this email masquerading as?

```bash
echo -n 'VGhhbmsgeW91ISBIb21lIERlcG90' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-03-20 13-20-20.png>)

{% hint style="success" %}
`Home Depot`
{% endhint %}

#### What is the sender's email?

{% hint style="success" %}
`support@teckbe.com`
{% endhint %}

#### What is the subject line?

```bash
echo -n 'T3JkZXIgUGxhY2VkIDogWW91ciBPcmRlciBJRCBPRDIzMjE2NTcwODkyOTEgUGxhY2VkIFN1Y2Nlc3NmdWxseQ==' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2022-03-20 13-18-27.png>)

{% hint style="success" %}
`Order Placed : Your Order ID OD2321657089291 Placed Successfully`
{% endhint %}

#### What is the URL link for - CLICK HERE?

![](<../../.gitbook/assets/Screenshot from 2022-03-20 13-34-50.png>)

{% hint style="success" %}
`hxxp[://]t[.]teckbe[.]com/p/?j3=EOowFcEwFHl6EOAyFcoUFV=TVEchwFHlUFOo6lVTTDcATE7oUE7AUET==`
{% endhint %}

## Task 7 Conclusion

A BEC is when an adversary gains control of an internal employee's account and then uses the compromised email account to convince other internal employees to perform unauthorized or fraudulent actions.

#### What is BEC?

{% hint style="success" %}
`Business Mail Compromise`
{% endhint %}
