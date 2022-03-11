---
description: https://tryhackme.com/room/anthem
---

# Anthem

## :spider\_web: Website Analysis

### What port is for the web server?

```
nmap 10.10.68.128
```

![](<../../.gitbook/assets/Screenshot from 2020-09-30 10-13-20.png>)

### What port is for remote desktop service?

> 3389

### What is a possible password in one of the pages web crawlers check for?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 09-13-05.png>)

### What CMS is the website using?

> Umbraco

### What is the domain of the website?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 10-06-10.png>)

### What's the name of the Administrator

![](<../../.gitbook/assets/Screenshot from 2020-09-30 09-51-46.png>)

### Can we find find the email address of the administrator?

> SG@anthem.com

![](<../../.gitbook/assets/Screenshot from 2020-09-30 10-06-10.png>)

## :flag\_white: Spot the flags

### What is flag 1?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 09-38-50.png>)

### What is flag 2?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 09-38-02.png>)

### What is flag 3?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 09-39-35.png>)

### What is flag 4?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 09-40-06.png>)

## :stadium: Final stage

### Gain initial access to the machine, what is the contents of user.txt?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-08-27.png>)

### Can we spot the admin password?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-20-56.png>)

### Escalate your privileges to root, what is the contents of root.txt?

![](<../../.gitbook/assets/Screenshot from 2020-09-30 11-23-20.png>)

## :link: Support Material

{% embed url="https://github.com/noraj/Umbraco-RCE" %}
