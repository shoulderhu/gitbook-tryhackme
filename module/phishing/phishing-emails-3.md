---
description: https://tryhackme.com/room/phishingemails3tryoe
---

# Phishing Emails 3

## Task 3 Email header analysis

#### What is the official site name of the bank that capitai-one.com tried to resemble?

![](<../../.gitbook/assets/Screenshot from 2022-03-20 17-01-36.png>)

{% hint style="success" %}
`capitalone.com`
{% endhint %}

## Task 4 Email body analysis

#### How can you manually get the location of a hyperlink?

![](<../../.gitbook/assets/image (3) (1).png>)

{% hint style="success" %}
`Copy Link Location`
{% endhint %}

## Task 6 PhishTool

#### Look at the Strings output. What is the name of the EXE file?

{% hint style="success" %}
`454326_PDF.exe`
{% endhint %}

## Task 7 Phishing Case 1

```bash
scp ubuntu@10.10.90.231:/home/ubuntu/Desktop/Phish3Case1.eml /media/vboxsf
```

![](<../../.gitbook/assets/Screenshot from 2022-03-20 17-34-07.png>)

#### What brand was this email tailored to impersonate?

{% hint style="success" %}
`Netflix`
{% endhint %}

#### What is the From email address?

{% hint style="success" %}
`JGQ47wazXe1xYVBrkeDg-JOg7ODDQwWdR@JOg7ODDQwWdR-yVkCaBkTNp.gogolecloud.com`
{% endhint %}

#### What is the originating IP? Defang the IP address.

{% hint style="success" %}
`209[.]85[.]167[.]226`
{% endhint %}

#### <mark style="color:red;">From what you can gather, what do you think will be a domain of interest? Defang the domain.</mark>

![](<../../.gitbook/assets/Screenshot from 2022-03-20 17-56-38.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-20 17-57-58.png>)

{% hint style="success" %}
`etekno[.]xyz`
{% endhint %}

#### What is the shortened URL? Defang the URL.

![](<../../.gitbook/assets/Screenshot from 2022-03-20 17-46-15.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-20 17-49-41.png>)

{% hint style="success" %}
`hxxps[://]t[.]co/yuxfZm8KPg?amp=`
{% endhint %}

## Task 8 Phishing Case 2

{% embed url="https://app.any.run/tasks/8bfd4c58-ec0d-4371-bfeb-52a334b69f59" %}

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-03-11.png>)

#### What does AnyRun classify this email as?

{% hint style="success" %}
`Suspicious activity`
{% endhint %}

#### What is the name of the PDF file?

{% hint style="success" %}
`Payment-updateid.pdf`
{% endhint %}

#### What is the SHA 256 hash for the PDF file?

{% hint style="success" %}
`CC6F1A04B10BCB168AEEC8D870B97BD7C20FC161E8310B5BCE1AF8ED420E2C24`
{% endhint %}

#### What two IP addresses are classified as malicious? Defang the IP addresses.

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-08-37.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-14-46.png>)

{% hint style="success" %}
`2[.]16[.]107[.]24,2[.]16[.]107[.]83`
{% endhint %}

#### What Windows process was flagged as **Potentially Bad Traffic**?

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-13-23.png>)

{% hint style="success" %}
`svchost.exe`
{% endhint %}

## Task 9 Phishing Case 3

{% embed url="https://app.any.run/tasks/82d8adc9-38a0-4f0e-a160-48a5e09a6e83" %}

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-19-15.png>)

#### What is this analysis classified as?

{% hint style="success" %}
`Malicious activity`
{% endhint %}

#### What is the name of the Excel file?

{% hint style="success" %}
`CBJ200620039539.xlsx`
{% endhint %}

#### What is the SHA 256 hash for the file?

{% hint style="success" %}
`5F94A66E0CE78D17AFC2DD27FC17B44B3FFC13AC5F42D3AD6A5DCFB36715F3EB`
{% endhint %}

#### What domains are listed as malicious? Defang the URLs & submit answers in alphabetical order.

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-23-39.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-21-38.png>)

{% hint style="success" %}
`biz9holdings[.]com,findresults[.]site,ww38[.]findresults[.]site`
{% endhint %}

#### What IP addresses are listed as malicious? Defang the IP addresses & submit answers from lowest to highest.

![](<../../.gitbook/assets/Screenshot from 2022-03-20 18-24-10.png>)

{% hint style="success" %}
`75[.]2[.]11[.]242,103[.]224[.]182[.]251,204[.]11[.]56[.]48`
{% endhint %}

#### What vulnerability does this malicious attachment attempt to exploit?

{% hint style="success" %}
`CVE-2017-11882`
{% endhint %}
