# Burp Suite

{% embed url="https://tryhackme.com/room/rpburpsuite" %}
https://tryhackme.com/room/rpburpsuite
{% endembed %}

## Task 4 Overview of Features

#### Which tool in Burp Suite can we use to perform a 'diff' on responses and other pieces of data?

{% hint style="success" %}
`Comparer`
{% endhint %}

#### What tool could we use to analyze randomness in different pieces of data such as password reset tokens?

{% hint style="success" %}
`Sequencer`
{% endhint %}

#### **Which tool can we use to set the scope of our project?**

{% hint style="success" %}
`Target`
{% endhint %}

#### While only available in the premium versions of Burp Suite, which tool can we use to automatically identify different vulnerabilities in the application we are examining?

{% hint style="success" %}
`Scanner`
{% endhint %}

#### Encoding or decoding data can be particularly useful when examining URL parameters or protections on a form, which tool allows us to do just that?

{% hint style="success" %}
`Decoder`
{% endhint %}

#### **Which tool allows us to redirect our web traffic into Burp for further examination?**

{% hint style="success" %}
`Proxy`
{% endhint %}

#### **Simple in concept but powerful in execution, which tool allows us to reissue requests?**

{% hint style="success" %}
`Repeater`
{% endhint %}

#### With four modes, which tool in Burp can we use for a variety of purposes such as field fuzzing?

{% hint style="success" %}
`Intruder`
{% endhint %}

#### **Last but certainly not least, which tool allows us to modify Burp Suite via the addition of extensions?**

{% hint style="success" %}
`Extender`
{% endhint %}

## Task 6 Proxy

#### By default, the Burp Suite proxy listens on only one interface. What is it?

{% hint style="success" %}
`127.0.0.1:8080`
{% endhint %}

#### Take a look at the actions, which **shortcut** allows us to forward the request to Repeater?

{% hint style="success" %}
`Ctrl-R`
{% endhint %}

#### **How about if we wanted to forward our request to Intruder?**

{% hint style="success" %}
`Ctrl-`**`I`**
{% endhint %}

#### What is the name of the first section where in general web requests (GET/POST) are saved?

{% hint style="success" %}
`HTTP history`
{% endhint %}

#### Defined in RFC 6455 as a low-latency communication protocol that doesn't require HTTP encapsulation, what is the name of the second section of our saved history in Burp Suite? These are commonly used in collaborate application which require real-time updates (Google Docs is an excellent example here).

{% hint style="success" %}
`WebSockets history`
{% endhint %}

#### Move over to the Options section of the Proxy tab and scroll down to Intercept Client Requests. Here we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 05-55-04.png>)

{% hint style="success" %}
`URL`
{% endhint %}

#### How about it's 'Relationship'? _In this situation, enabling this match rule can be incredibly useful following target definition as we can effectively leave intercept on permanently as it won't disturb sites which are outside of our scope - something which is particularly nice if we need to Google something in the same browser._

{% hint style="success" %}
`Is in target scope`
{% endhint %}

## Task 7 Target Definition

#### Before leaving the Proxy tab, switch Intercept to disabled. We'll still see the pages we navigate to in our history and the target tab, just having Intercept constantly stopping our requests for this next bit will get old fast.

#### Navigate to the Target tab in Burp. In our last task, Proxy, we browsed to the website on our target machine (in this case OWASP Juice Shop). Find our target site in this list and right-click on it. Select 'Add to scope'.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-20-22.png>)

#### Clicking 'Add to scope' will trigger a pop-up. This will stop Burp from sending out-of-scope items to our site map. **** Select 'Yes' to close the popup.

#### Browse around the rest of the application to build out our page structure in the target tab. Once you've visited most of the pages of the site return to Burp Suite and expand the various levels of the application directory. What do we call this representation of the collective web application?

{% hint style="success" %}
site map
{% endhint %}

#### What is the term for browsing the application as a normal user prior to examining it further?

{% hint style="success" %}
happy path
{% endhint %}

#### One last thing before moving on. Within the target tab, you may have noticed a sub-tab for issue definitions. Click into that now.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-22-41.png>)

#### The issue definitions found here are how Burp Suite defines issues within reporting. While getting started, these issue definitions can be particularly helpful for understanding and categorizing various findings we might have. Which poisoning issue arises when an application behind a cache process input that is not included in the cache key?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-24-12.png>)

{% hint style="success" %}
Web cache poisoning
{% endhint %}

## Task 8 Puttin' it on Repeat\[er]

#### To start, click 'Account' (this might be 'Login' depending on the version of Juice Shop) in the top right corner of Juice Shop in order to navigate to the login page.

#### Try logging in with invalid credentials. What error is generated when login fails?

![](<../../.gitbook/assets/Screenshot from 2020-09-10 14-14-52.png>)

{% hint style="success" %}
`Invalid email or password.`
{% endhint %}

#### But wait, didn't we want to send that request to Repeater? Even though we didn't send it to Repeater initially via intercept, we can still find the request in our history. Switch over to the HTTP sub-tab of Proxy. Look through these requests until you find our failed login attempt. **Right-click on this request and send it to Repeater and then send it to Intruder, too!**

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-09-38.png>)

#### Now that we've sent the request to Repeater, let's try adjusting the request such that we are sending a single quote (') as both the email and password. What error is generated from this request?

![](<../../.gitbook/assets/Screenshot from 2020-09-10 14-17-23.png>)

{% hint style="success" %}
`SQLITE_ERROR`
{% endhint %}

#### Now that we've leveraged Repeater to gain proof of concept that Juice Shop's login is vulnerable to SQLi, let's try something a little more mischievous and attempt to leave a devastating zero-star review. First, click on the drawer button in the top-left of the application. **If this isn't present for you, just skip to the next question.**

#### Next, click on 'Customer Feedback' (depending on the version of Juice Shop this also might be along the top of the page next to 'Login' under 'Contact Us')

#### With the Burp proxy on submit feedback. Once this is done, find the POST request in your HTTP History in Burp and send it to Repeater.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-12-45.png>)

#### **What field do we have to modify in order to submit a zero-star review?**

![](<../../.gitbook/assets/Screenshot from 2020-09-10 14-21-45.png>)

{% hint style="success" %}
`rating`
{% endhint %}

#### Submit a zero-star review and complete this challenge in Juice Shop!

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-13-14.png>)

## Task 9 Help! There's an Intruder!

1\. _Sniper_ - The most popular attack type, this cycles through our selected positions, putting the next available payload (item from our wordlist) in each position in turn. This uses only one set of payloads (one wordlist).

2\. _Battering Ram_ - Similar to Sniper, Battering Ram uses only one set of payloads. Unlike Sniper, Battering Ram puts every payload into every selected position. Think about how a battering ram makes contact across a large surface with a single surface, hence the name battering ram for this attack type.

3\. _Pitchfork_ - The Pitchfork attack type allows us to use multiple payload sets (one per position selected) and iterate through both payload sets _simultaneously_. For example, if we selected two positions (say a username field and a password field), we can provide a username and password payload list. Intruder will then cycle through the combinations of usernames and passwords, resulting in a total number of combinations equalling the smallest payload set provided. __&#x20;

4\. _Cluster Bomb_ - The Cluster Bomb attack type allows us to use multiple payload sets (one per position selected) and iterate through all combinations of the payload lists we provide. For example, if we selected two positions (say a username field and a password field), we can provide a username and password payload list. Intruder will then cycle through the combinations of usernames and passwords, resulting in a total number of combinations equalling usernames x passwords. _Do note, this can get pretty lengthy if you are using the community edition of Burp._&#x20;

#### Which attack type allows us to select multiple payload sets (one per position) and iterate through them simultaneously?

{% hint style="success" %}
`Pitchfork`
{% endhint %}

#### How about the attack type which allows us to use one payload set in every single position we've selected simultaneously?

{% hint style="success" %}
`Battering Ram`
{% endhint %}

#### Which attack type allows us to select multiple payload sets (one per position) and iterate through all possible combinations?

{% hint style="success" %}
`Cluster Bomb`
{% endhint %}

#### Perhaps the most commonly used, which attack type allows us to cycle through our payload set, putting the next available payload in each position in turn?

{% hint style="success" %}
Sniper
{% endhint %}

#### Download the wordlist attached to this room, this is a shortened version of the [fuzzdb SQLi platform detection list](https://github.com/fuzzdb-project/fuzzdb/blob/master/attack/sql-injection/detect/xplatform.txt).

#### Return to the Intruder in Burp. In our previous task, we passed our failed login attempt to both Repeater and Intruder for further examination. Open up the Positions sub-tab in the Intruder tab with this request now and verify that 'Sniper' is selected as our attack type.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-47-10.png>)

#### Burp attempts to automatically highlight possible fields of interest for Intruder, however, it doesn't have it quite right for what we'll be looking at in this instance. Hit 'Clear' on the right-hand side to clear all selected fields.

#### Next, let's highlight the email field between the double quotes ("). _This will be whatever you entered in the email field for our previous failed login attempt._

#### Now click 'Add' to select our email field as a position for our payloads.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-49-14.png>)

#### Next, let's switch to the payloads sub-tab of Intruder. Once there, hit 'Load' and select the wordlist you previously downloaded in question five that is attached to this task.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-50-59.png>)

#### Almost there! Scroll down and uncheck 'URL-encode these characters'. We don't want to have the characters sent in our payloads to be encoded as they otherwise won't be recognized by SQL.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-50-37.png>)

#### Finally, click 'Start attack'. What is the first payload that returns a 200 status code, showing that we have successfully bypassed authentication?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-57-02.png>)

{% hint style="success" %}
`a' or 1=1--`
{% endhint %}

## Task 10 As it turns out the machines are better at math than us

#### Switch over to the HTTP history sub-tab of Proxy.

#### We're going to dig for a response which issues a cookie. Parse through the various responses we've received from Juice Shop until you find one that includes a 'Set-Cookie' header.

#### Once you've found a request response that issues a cookie, right-click on the request and select 'Send to Sequencer'.

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-35-10.png>)

#### Change over Sequencer and select 'Start live capture'

#### Let Sequencer run and collect \~10,000 requests. Once it hits roughly that amount hit 'Pause' and then 'Analyze now'

#### Parse through the results. What is the effective estimated entropy measured in?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-00-49.png>)

{% hint style="success" %}
`bits`
{% endhint %}

#### In order to find the usable bits of entropy we often have to make some adjustments to have a normalized dataset. What item is converted in this process?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 07-03-54.png>)

{% hint style="success" %}
`token`
{% endhint %}

## Task 11 Decoder and Comparer

#### Let's first take a look at decoder by revisiting an old friend. Previously we discovered the scoreboard within the site JavaScript. Return to our target tab and find the API endpoint highlighted in the following request:

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-05-43.png>)

#### Copy the first line of that request and paste it into Decoder. Next, select 'Decode as ...' URL

#### What character does the %20 in the request we copied into Decoder decode as?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-07-33.png>)

{% hint style="success" %}
`space`
{% endhint %}

#### Similar to CyberChef, Decoder also has a 'Magic' mode where it will automatically attempt to decode the input it is provided. What is this mode called?

{% hint style="success" %}
`Smart decode`
{% endhint %}

#### What can we load into Comparer to see differences in what various user roles can access? This is very useful to check for access control issues.

{% hint style="success" %}
`site maps`
{% endhint %}

#### Comparer can perform a diff against two different metrics, which one allows us to examine the data loaded in as-is rather than breaking it down into bytes?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-09-35.png>)

{% hint style="success" %}
`Words`
{% endhint %}

## Task 12 Installing some Mods \[Extender]

* [Logger++](https://portswigger.net/bappstore/470b7057b86f41c396a97903377f3d81) - Adds enhanced logging to all requests and responses from all Burp Suite tools, enable this one before you need it ;)
* [Request Smuggler](https://portswigger.net/bappstore/aaaa60ef945341e8a450217a54a11646) - A relatively new extension, this allows you to attempt to smuggle requests to backend servers. See this talk by James Kettle for more details: [Link](https://www.youtube.com/watch?v=\_A04msdplXs)
* [Autorize](https://portswigger.net/bappstore/f9bbac8c4acf4aefa4d7dc92a991af2f) - Useful for authentication testing in web app tests. These tests typically revolve around navigating to restricted pages or issuing restricted GET requests with the session cookies of low-privileged users
* [Burp Teams Server](https://github.com/Static-Flow/BurpSuite-Team-Extension) - Allows for collaboration on a Burp project amongst team members. Project details are shared in a chatroom-like format
* [Retire.js](https://portswigger.net/bappstore/36238b534a78494db9bf2d03f112265c) - Adds scanner checks for outdated JavaScript libraries that contain vulnerabilities, this is a premium extension
* [J2EEScan](https://portswigger.net/bappstore/7ec6d429fed04cdcb6243d8ba7358880) - Adds scanner test coverage for J2EE (java platform for web development) applications, this is a premium extension
* [Request Timer](https://portswigger.net/bappstore/56675bcf2a804d3096465b2868ec1d65) - Captures response times for requests made by all Burp tools, useful for discovering timing attack vectors&#x20;

#### Which extension allows us to bookmark various requests?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-14-37.png>)

{% hint style="success" %}
`Bookmarks`
{% endhint %}

## Task 13 But wait, there's more!

#### Download the report attached to this task. What is the only critical issue?

![](<../../.gitbook/assets/Screenshot from 2022-04-11 06-20-02.png>)

{% hint style="success" %}
`Cross-origin resource sharing: arbitrary origin trusted`
{% endhint %}

#### How many 'Certain' low issues did Burp find?

{% hint style="success" %}
`12`
{% endhint %}
