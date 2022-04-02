# The Lay of the land

{% embed url="https://tryhackme.com/room/thelayoftheland" %}
https://tryhackme.com/room/thelayoftheland
{% endembed %}

## Task 4 **** Active Directory (AD) environment

#### Before going any further, ensure the attached machine is deployed and try what we discussed. **Is the attached machine part of the AD environment? (Y|N)**

```bash
systeminfo | findstr Domain
```

{% hint style="success" %}
`Y`
{% endhint %}

#### If it is part of an AD environment, **what is the domain name of the AD?**

{% hint style="success" %}
`thmredteam.com`
{% endhint %}

## Task 5 Users and Groups Management

#### Use the Get-ADUser -Filter \* -SearchBase command to list the available user accounts within THM OU in the thmredteam.com domain. How many users are available?

```bash
 Get-ADUser -Filter * -SearchBase 'OU=THM,DC=THMREDTEAM,DC=COM' `
 | select Name, ObjectClass, UserPrincipalName
```

{% hint style="success" %}
`6`
{% endhint %}

#### Once you run the previous command, what is the UserPrincipalName (email) of the admin account?

{% hint style="success" %}
`thmadmin@thmredteam.com`
{% endhint %}

## Task 6&#x20;
