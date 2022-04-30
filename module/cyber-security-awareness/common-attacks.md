# Common Attacks

{% embed url="https://tryhackme.com/room/commonattacks" %}
https://tryhackme.com/room/commonattacks
{% endembed %}

## Common Attacks

### Task 2 Social Engineering

#### What was the original target of Stuxnet?

{% hint style="success" %}
`the Iran nuclear programme`
{% endhint %}

### Task 3 Social Engineering: Phishing

#### The static site will display a series of emails and text messages. You will be asked to identify which of these messages are genuine and which are phishing attempts. Once you have successfully identified all of the messages you will be presented with a flag to enter, here.

#### What is the flag?

![](<../../.gitbook/assets/Screenshot from 2022-04-30 17-10-18.png>)

{% hint style="success" %}
`THM{I_CAUGHT_ALL_THE_PHISH}`
{% endhint %}

### Task 4 Malware and Ransomware

#### What currency did the Wannacry attackers request payment in?

{% hint style="success" %}
`Bitcoin`
{% endhint %}

### Task 5 Passwords and Authentication

#### Based on the content of the website, you have generated a list of likely passwords, which is as follows:

```
TryH@ckMe
TryHackMe123
THM123456
qwertyuiop123
TryHackMe2021
TryHackMe123!
TryHackMe345
TryHackM3!
```

#### Copy the list of passwords into the "Password List" field of the hash cracker, then click "Go"!

#### Look at the "Current Word / Hash" section of the hash cracker.

#### Notice that for each word in the list you entered, the cracker is creating an MD5 hash of the word then comparing it to the Target Hash. If the two hashes match then the password has been found! The hash cracker should find the password that matches the target hash very quickly.

#### What is the password?

![](<../../.gitbook/assets/Screenshot from 2022-04-30 17-45-44.png>)

{% hint style="success" %}
`TryHackMe123!`
{% endhint %}

#### This is a very simple, browser-based example; however, in reality local hash cracking with a wordlist isn't any more complex from a high-level perspective — it's the same technique, but with a lot more potential passwords!

#### Hopefully this example illustrates why it is so important to choose a strong password — even if the passwords are hashed appropriately.

#### In the next task we will look at some of the common account protection measures, as well as how to generate secure passwords.

## Staying Safe

### Task 6 Multi-Factor Authentication and Password Managers

#### Where you have the option, which should you use as a second authentication factor between SMS based TOTPs or Authenticator App based TOTPs?

{% hint style="success" %}
`App`
{% endhint %}

### Task 8 Backups

#### What is the minimum number of up-to-date backups you should make?

{% hint style="success" %}
`3`
{% endhint %}

#### Of these, how many (at minimum) should be stored in another location?

{% hint style="success" %}
`1`
{% endhint %}
