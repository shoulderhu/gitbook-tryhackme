---
layout: landing
---

# Burp Suite: Intruder

{% embed url="https://tryhackme.com/room/burpsuiteintruder" %}
https://tryhackme.com/room/burpsuiteintruder
{% endembed %}

## Intruder

### Task 2 What is Intruder?

#### Which section of the _Options_ sub-tab allows you to control what information will be captured in the Intruder results?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-46-22.png>)

{% hint style="success" %}
`Attack Results`
{% endhint %}

#### In which Intruder sub-tab can we define the "Attack type" for our planned attack?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-46-40.png>)

{% hint style="success" %}
`Positions`
{% endhint %}

## Attack Types

### Task 5 Sniper

A wordlist with 3 words in it: burp, suite, and intruder.

| username     | password     |
| ------------ | ------------ |
| **burp**     | Expl101ted   |
| **suite**    | Expl101ted   |
| **intruder** | Expl101ted   |
| pentester    | **burp**     |
| pentester    | **suite**    |
| pentester    | **intruder** |

#### If you were using Sniper to fuzz _three_ parameters in a request, with a wordlist containing 100 words, how many requests would Burp Suite need to send to complete the attack?

{% hint style="success" %}
`300`
{% endhint %}

#### How many sets of payloads will Sniper accept for conducting an attack?

{% hint style="success" %}
`1`
{% endhint %}

#### Sniper is good for attacks where we are only attacking a single parameter, aye or nay?

{% hint style="success" %}
`Aye`
{% endhint %}

### Task 6 Battering Ram

A wordlist with 3 words in it: burp, suite, and intruder.

| username | password |
| -------- | -------- |
| burp     | burp     |
| suite    | suite    |
| intruder | intruder |

#### As a hypothetical question: you need to perform a Battering Ram Intruder attack on the example request above. If you have a wordlist with two words in it (`admin` and `Guest`) and the positions in the request template look like this: `username=§pentester§&password=§Expl01ted§`

#### What would the body parameters of the _first_ request that Burp Suite sends be?

{% hint style="success" %}
`username=admin&password=admin`
{% endhint %}

### Task 7 Pitchfork

Two wordlists with 3 words in each wordlist:&#x20;

* username.txt: joel, harriet, alex.&#x20;
* password.txt: J03l, Emma1815, Sk1ll.

| username | password |
| -------- | -------- |
| joel     | J03l     |
| harriet  | Emma1815 |
| alex     | Sk1ll    |

#### What is the maximum number of payload sets we can load into Intruder in Pitchfork mode?

{% hint style="success" %}
`20`
{% endhint %}

### Task 8 Cluster Bomb

Two wordlists with 3 words in each wordlist:&#x20;

* username.txt: joel, harriet, alex.&#x20;
* password.txt: J03l, Emma1815, Sk1ll.

| username | password |
| -------- | -------- |
| joel     | J03l     |
| joel     | Emma1815 |
| joel     | Sk1ll    |
| harriet  | J03l     |
| harriet  | Emma1815 |
| harriet  | Sk1ll    |
| alex     | J03l     |
| alex     | Emma1815 |
| alex     | Sk1ll    |

#### We have three payload sets. The first set contains 100 lines; the second contains 2 lines; and the third contains 30 lines. How many requests will Intruder make using these payload sets in a Cluster Bomb attack?

{% hint style="success" %}
`6000`
{% endhint %}

## Intruder

### Task 9 Payloads

#### Which payload type lets us load a list of words into a payload set?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-07-09.png>)

{% hint style="success" %}
`Simple list`
{% endhint %}

#### Which Payload Processing rule could we use to add characters at the end of each payload in the set?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-07-24.png>)

{% hint style="success" %}
`Add Suffix`
{% endhint %}

## Practical

### Task 10 Example

#### Download and unzip the `BastionHostingCreds.zip` zipfile.

```bash
wget http://10.10.209.126:9999/Credentials/BastionHostingCreds.zip
unzip BastionHostingCreds.zip
```

#### The zip file should contain four wordlists:

* `emails.txt`
* `usernames.txt`
* `passwords.txt`
* `combined.txt`

#### These contain lists of leaked emails, usernames, and passwords, respectively. The last list contains the combined email and password lists. We will be using the `usernames.txt` and `passwords.txt` lists.

#### Navigate to `http://10.10.209.126/support/login` in your browser. Activate the Burp Proxy and try to log in, catching the request in your proxy.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-16-19.png>)

#### Send the request from the Proxy to Intruder by right-clicking and selecting "Send to Intruder" or by using the `Ctrl + I` shortcut.

#### Looking in the "Positions" sub-tab, we should see that the auto-selection should have chosen the username and password parameters, so we don't need to do anything else in terms of defining our positions.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-18-04.png>)

#### We also need the Attack type to be "Pitchfork":

#### Let's switch over to the "Payloads" sub-tab. We should find that we have two payload sets available:

#### Although these aren't named, we know from the fact that the username field is to the left of the password field that the first position will be for usernames, and the second position will be for passwords. We can leave both of these as the "Simple list" payload type.

#### In the first payload set, go to "Payload Options", choose "Load", then select our list of usernames. Do the same thing for the second payload set and the list of passwords.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-20-05.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-20-18.png>)

#### Once the attack has completed, we will be presented with a new window giving us the results -- but we have a new problem. Burp sent 100 requests: how are we supposed to know which one(s), if any, are valid?

#### The most common solution to this problem is to use the status code of the response to differentiate between successful or unsuccessful login attempts; this only works if there _is_ a difference in the status codes, however. Ideally, successful login requests would give us a 200 response code, and failed login requests would provide us with a 401; however, in many cases, we are just given a 302 redirect for all requests instead. That solution is out.

#### The next most common solution is to use the _Length_ of the responses to identify differences between them. For example, a successful login attempt may have a response with 400 bytes in it, whereas an unsuccessful login attempt may yield a response with 600 bytes in it.

#### We can sort by byte length by clicking on the header for the "Length" column:&#x20;

#### Once we have sorted our results, one request should stand out as being different!

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-26-01.png>)

#### As you may have guessed, the request with the shorter response length was made with the valid credentials -- a fact we can confirm by attempting to log in with the credentials used in the successful request.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-27-15.png>)

### Task 11 Challenge

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-29-50.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-31-29.png>)

#### Which attack type is best suited for this task?

{% hint style="success" %}
`Sniper`
{% endhint %}

#### Configure an appropriate position and payload (the tickets are stored at values between 1 and 100), then start the attack.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-32-11.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-33-03.png>)

#### You should find that at least five tickets will be returned with a status code of 200, indicating that they exist.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 18-39-26.png>)

#### Either using the Response tab in the Attack Results window or by looking at each successful (i.e. 200 code) request manually in your browser, find the ticket that contains the flag.

#### What is the flag?

{% hint style="success" %}
`THM{MTMxNTg5NTUzMWM0OWRlYzUzMDVjMzJl}`
{% endhint %}

## Extra Mile

### Task 12 CSRF Token Bypass

#### Navigate to  `http://10.10.166.236/admin/login/`. Activate the Burp Proxy and attempt to log in. Capture the request and send it to Intruder.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 19-50-52.png>)

#### Configure the positions the same way as we did for bruteforcing the support login:

* Set the attack type to be "Pitchfork".
* Clear all of the predefined positions and select _only_ the username and password form fields. The other two positions will be handled by our macro.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 19-52-09.png>)

#### Now switch over to the Payloads sub-tab and load in the same username and password wordlists we used for the support login attack.

#### Up until this point, we have configured Intruder in almost the same way as our previous credential stuffing attack; this is where things start to get more complicated.

#### With the username and password parameters handled, we now need to find a way to grab the ever-changing loginToken and session cookie. Unfortunately, Recursive Grep won't work here due to the redirect response, so we can't do this entirely within Intruder -- we will need to build a macro.

#### Macros allow us to perform the same set of actions repeatedly. In this case, we simply want to send a GET request to `/admin/login/`.

#### Fortunately, setting this up is a very easy process.

* Switch over to the "Project Options" tab, then the "Sessions" sub-tab.
* Scroll down to the bottom of the sub-tab to the "Macros" section and click the "Add" button.
* The menu that appears will show us our request history. If there isn't a GET request to `http://10.10.166.236/admin/login/` in the list already, navigate to this location in your browser and you should see a suitable request appear in the list.
* With the request selected, click Ok.
* Finally, give the macro a suitable name, then click "Ok" again to finish the process.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 19-55-48.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 19-56-59.png>)

#### Now that we have a macro defined, we need to set Session Handling rules that define how the macro should be used.

* Still in the "Sessions" sub-tab of Project Options, scroll up to the "Session Handling Rules" section and choose to "Add" a new rule.
* A new window will pop up with two tabs in it: "Details" and "Scope". We are in the Details tab by default.
* Fill in an appropriate description, then switch over to the Scope tab.
* In the "Tools Scope" section, deselect every checkbox other than Intruder -- we do not need this rule to apply anywhere else.
* In the "URL Scope" section, choose "Use suite scope"; this will set the macro to only operate on sites that have been added to the global scope (as was discussed in [Burp Basics](https://tryhackme.com/room/burpsuitebasics)). If you have not set a global scope, keep the "Use custom scope" option as default and add `http://10.10.166.236/` to the scope in this section.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 19-58-11.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 20-04-27.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 20-01-14.png>)

#### Now we need to switch back over to the Details tab and look at the "Rule Actions" section.

* Click the "Add" button -- this will cause a dropdown menu to appear with a list of actions we can add.
* Select "Run a Macro" from this list.
* In the new window that appears, select the macro we created earlier.

#### As it stands, this macro will now overwrite all of the parameters in our Intruder requests before we send them; this is great, as it means that we will be getting the loginTokens and session cookies added straight into our requests. That said, we should restrict which parameters and cookies are being updated before we start our attack:

* Select "Update only the following parameters", then click the "Edit" button next to the input box below the radio button.
* In the "Enter a new item" text field, type "loginToken". Press "Add", then "Close".
* Select "Update only the following cookies", then click the relevant "Edit" button.
* Enter "session" in the "Enter a new item" text field, press "Add", then "Close".
* Finally, press "Ok" to confirm our action.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 20-04-00.png>)

#### You should now have a macro defined that will substitute in the CSRF token and session cookie. All that's left to do is switch back to Intruder and start the attack!

#### As with the support login credential stuffing attack we carried out, the response codes here are all the same (302 Redirects). Once again, order your responses by Length to find the valid credentials. Your results won't be quite as clear-cut as last time -- you will see quite a few different response lengths: however, the response that indicates a successful login should still stand out as being quite significantly shorter.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 20-07-15.png>)

#### Use the credentials you just found to log in (you may need to refresh the login page before entering the credentials).

![](<../../.gitbook/assets/Screenshot from 2022-03-27 20-08-27.png>)
