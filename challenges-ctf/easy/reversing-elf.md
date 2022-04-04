# Reversing ELF

{% embed url="https://tryhackme.com/room/reverselfiles" %}
https://tryhackme.com/room/reverselfiles
{% endembed %}

## Task 1 Crackme1

#### What is the flag?

```bash
./crackme1
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-14-39.png>)

{% hint style="success" %}
`flag{not_that_kind_of_elf}`
{% endhint %}

## Task 2 Crackme2

#### What is the super secret password ?

```bash
ltrace ./crackme2 asdf
```

{% hint style="success" %}
`super_secret_password`
{% endhint %}

#### What is the flag ?

```bash
./crackme2 super_secret_password
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-16-40.png>)

{% hint style="success" %}
`flag{if_i_submit_this_flag_then_i_will_get_points}`
{% endhint %}

## Task 3 Crackme3

#### What is the flag?

```bash
ltrace ./crackme3 asdf
strings ./crame3
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-25-29.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-22-52.png>)

```bash
echo -n 'ZjByX3kwdXJfNWVjMG5kX2xlNTVvbl91bmJhc2U2NF80bGxfN2gzXzdoMW5nNQ==' | base64 -d
./crackme3 f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-22-03.png>)

{% hint style="success" %}
`f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5`
{% endhint %}

## Task 4 Crackme4

#### What is the password ?

```bash
ltrace ./crackme4 asdf
./crackme4 my_m0r3_secur3_pwd
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-29-07.png>)

{% hint style="success" %}
`my_m0r3_secur3_pwd`
{% endhint %}

## Task 5 Crackme5

#### What is the input ?

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-41-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-41-13.png>)

```bash
echo 'OfdlDSA|3tXb32~X3tX@sX`4tXtz' | ./crackme5
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-40-58.png>)

{% hint style="success" %}
``OfdlDSA|3tXb32~X3tX@sX`4tXtz``
{% endhint %}

## Task 6 Crackme6

#### What is the password ?

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-45-01.png>)

```bash
./crackme6 1337_pwd
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-44-44.png>)

{% hint style="success" %}
`1337_pwd`
{% endhint %}

## Task 7 Crackme7

#### What is the flag ?

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-50-09.png>)

```bash
./crackme7
[>] 31337
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-49-56.png>)

{% hint style="success" %}
`flag{much_reversing_very_ida_wow}`
{% endhint %}

## Task 8 Crackme8

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-54-54.png>)

#### What is the flag ?

```bash
./crackme8 -889262067
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 22-54-12.png>)

{% hint style="success" %}
`flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}`
{% endhint %}
