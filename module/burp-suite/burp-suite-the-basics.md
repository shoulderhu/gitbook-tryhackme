# Burp Suite: The Basics

{% embed url="https://tryhackme.com/room/burpsuitebasics" %}
https://tryhackme.com/room/burpsuitebasics
{% endembed %}

## Getting Started

### Task 2 What is Burp Suite?

#### Which edition of Burp Suite will we be using in this module?

{% hint style="success" %}
`Burp Suite Community`
{% endhint %}

#### Which edition of Burp Suite runs on a server and provides constant scanning for target web apps?

{% hint style="success" %}
`Burp Suite Enterprise`
{% endhint %}

#### Burp Suite is frequently used when attacking web applications and \_\_\_\_\_\_ applications.

{% hint style="success" %}
`mobile`
{% endhint %}

### Task 3 Features of Burp Community

#### Which Burp Suite feature allows us to intercept requests between ourselves and the target?

{% hint style="success" %}
`Proxy`
{% endhint %}

#### Which Burp tool would we use if we wanted to bruteforce a login form?

{% hint style="success" %}
`Intruder`
{% endhint %}

### Task 6 Navigation

| Shortcut           | Does                       |
| ------------------ | -------------------------- |
| `Ctrl + Shift + T` | Switch to the Target tab   |
| `Ctrl + Shift + P` | Switch to the Proxy tab    |
| `Ctrl + Shift + I` | Switch to the Intruder tab |
| `Ctrl + Shift + R` | Switch to the Repeater tab |

### Task 7 Options

* Global settings can be found in the _User options_ tab along the top menu bar.
* Project-specific settings can be found in the _Project options_ tab.

#### Change the Burp Suite theme to dark mode

![](<../../.gitbook/assets/Screenshot from 2022-04-05 14-52-48.png>)

#### In which _Project options_ sub-tab can you find reference to a "Cookie jar"?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-00-30.png>)

{% hint style="success" %}
`Sessions`
{% endhint %}

#### In which _User options_ sub-tab can you change the Burp Suite update behaviour?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 14-55-07.png>)

{% hint style="success" %}
`Misc`
{% endhint %}

#### What is the name of the section within the _User options_ "Misc" sub-tab which allows you to change the Burp Suite keybindings?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 14-55-28.png>)

{% hint style="success" %}
`Hotkeys`
{% endhint %}

#### If we have uploaded Client-Side TLS certificates in the _User options_ tab, can we override these on a per-project basis?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 14-56-17.png>)

{% hint style="success" %}
`Aye`
{% endhint %}

## Proxy

### Task 8 Introduction to the Burp Proxy

#### Which button would we choose to send an intercepted request to the target in Burp Proxy?

{% hint style="success" %}
`Forward`
{% endhint %}

#### What is the default keybind for this?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-13-13.png>)

{% hint style="success" %}
`Ctrl+F`
{% endhint %}

### Task 9 Connecting through the Proxy (FoxyProxy)

#### Read through the options in the right-click menu. There is one particularly useful option that allows you to intercept and modify the _response_ to your request.&#x20;

#### What is this option?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-25-24.png>)

{% hint style="success" %}
`Response to this request`
{% endhint %}

### Task 13 Site Map and Issue Definitions

#### Take a look around the site on `http://10.10.92.129/` -- we will be using this a lot throughout the module. Visit every page linked to from the homepage, then check your sitemap -- one endpoint should stand out as being very unusual!

#### What is the flag you receive?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-41-14.png>)

{% hint style="success" %}
`THM{NmNlZTliNGE1MWU1ZTQzMzgzNmFiNWVk}`
{% endhint %}

#### Look through the Issue Definitions list. What is the typical severity of a Vulnerable JavaScript dependency?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-42-50.png>)

{% hint style="success" %}
`Low`
{% endhint %}

## Practical

### Task 14 Example Attack

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-45-48.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-46-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-05 15-47-34.png>)
