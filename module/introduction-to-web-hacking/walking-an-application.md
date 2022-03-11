---
description: https://tryhackme.com/room/walkinganapplication
---

# Walking An Application

## Task 3 Viewing the Page Source

#### What is the flag from the HTML comment?

![view-source:https://10-10-171-222.p.thmlabs.com/](<../../.gitbook/assets/Screenshot from 2022-03-05 15-05-39.png>)

![https://10-10-171-222.p.thmlabs.com/new-home-beta](<../../.gitbook/assets/Screenshot from 2022-03-05 15-05-53.png>)

{% hint style="success" %}
`THM{HTML_COMMENTS_ARE_DANGEROUS}`
{% endhint %}

#### What is the flag from the secret link?

![view-source:https://10-10-171-222.p.thmlabs.com/](<../../.gitbook/assets/Screenshot from 2022-03-05 15-09-03.png>)

![https://10-10-171-222.p.thmlabs.com/secret-page](<../../.gitbook/assets/Screenshot from 2022-03-05 15-08-53.png>)

{% hint style="success" %}
`THM{NOT_A_SECRET_ANYMORE}`
{% endhint %}

#### What is the directory listing flag?

![http://10-10-171-222.p.thmlabs.com/assets/](<../../.gitbook/assets/Screenshot from 2022-03-05 15-11-30.png>)

![http://10-10-171-222.p.thmlabs.com/assets/flag.txt](<../../.gitbook/assets/Screenshot from 2022-03-05 15-11-44.png>)

{% hint style="success" %}
`THM{INVALID_DIRECTORY_PERMISSIONS}`
{% endhint %}

#### What is the framework flag?

```bash
wget 10-10-171-222.p.thmlabs.com/tmp.zip
unzip tmp.zip
cat flag.txt
```

![https://static-labs.tryhackme.cloud/sites/thm-web-framework/changelog.html](<../../.gitbook/assets/Screenshot from 2022-03-05 15-17-54.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-05 15-20-30.png>)

{% hint style="success" %}
`THM{KEEP_YOUR_SOFTWARE_UPDATED}`
{% endhint %}

#### Unknown

![https://static-labs.tryhackme.cloud/sites/thm-web-framework/documentation.html](<../../.gitbook/assets/Screenshot from 2022-03-05 15-16-16.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-05 15-15-49.png>)

![http://10-10-171-222.p.thmlabs.com/thm-framework-login](<../../.gitbook/assets/Screenshot from 2022-03-05 15-16-01.png>)

## Task 4 Developer Tools - Inspector

#### What is the flag behind the paywall?

![](<../../.gitbook/assets/Screenshot from 2022-03-05 15-30-41.png>)

{% hint style="success" %}
`THM{NOT_SO_HIDDEN}`
{% endhint %}

## Task 5 Developer Tools - Debugger

#### What is the flag in the red box?

![](<../../.gitbook/assets/Screenshot from 2022-03-05 15-37-26.png>)

{% hint style="success" %}
`THM{CATCH_ME_IF_YOU_CAN}`
{% endhint %}

## Task 6 Developer Tools - Network

#### What is the flag shown on the contact-msg network request?

![](<../../.gitbook/assets/Screenshot from 2022-03-05 15-42-32.png>)

{% hint style="success" %}
`THM{GOT_AJAX_FLAG}`
{% endhint %}
