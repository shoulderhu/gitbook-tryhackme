# Burp Suite

## :left\_facing\_fist: Overview of Features

### Which tool in Burp Suite can we use to perform a 'diff' on responses and other pieces of data?

{% hint style="success" %}
Comparer
{% endhint %}

### What tool could we use to analyze randomness in different pieces of data such as password reset tokens?

{% hint style="success" %}
Sequencer
{% endhint %}

### **Which tool can we use to set the scope of our project?**

{% hint style="success" %}
**Target**
{% endhint %}

### While only available in the premium versions of Burp Suite, which tool can we use to automatically identify different vulnerabilities in the application we are examining?

{% hint style="success" %}
Scanner
{% endhint %}

### Encoding or decoding data can be particularly useful when examining URL parameters or protections on a form, which tool allows us to do just that?

{% hint style="success" %}
Decoder
{% endhint %}

### **Which tool allows us to redirect our web traffic into Burp for further examination?**

{% hint style="success" %}
**Proxy**
{% endhint %}

### **Simple in concept but powerful in execution, which tool allows us to reissue requests?**

{% hint style="success" %}
**Repeater**
{% endhint %}

### With four modes, which tool in Burp can we use for a variety of purposes such as field fuzzing?

{% hint style="success" %}
Intruder
{% endhint %}

### **Last but certainly not least, which tool allows us to modify Burp Suite via the addition of extensions?**

{% hint style="success" %}
**Extender**
{% endhint %}

## :u7981: Proxy

### By default, the Burp Suite proxy listens on only one interface. What is it?

{% hint style="success" %}
127.0.0.1:8080
{% endhint %}

### Which **shortcut** allows us to forward the request to Repeater?

{% hint style="success" %}
Ctrl-R
{% endhint %}

### **How about if we wanted to forward our request to Intruder?**

{% hint style="success" %}
Ctrl-**I**
{% endhint %}

### What is the name of the first section wherein general web requests (GET/POST) are saved?

{% hint style="success" %}
HTTP history
{% endhint %}

### What is the name of the second section of our saved history in Burp Suite? These are commonly used in collaborate application which require real-time updates

{% hint style="success" %}
WebSockets history
{% endhint %}

### **Move over to the Options section of the Proxy tab and scroll down to Intercept Client Requests. Here we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type?**

{% hint style="success" %}
**URL**
{% endhint %}

### How about it's 'Relationship'?

{% hint style="success" %}
Is in target scope
{% endhint %}

## :dart: Target Definition

### Once you've visited most of the pages of the site return to Burp Suite and expand the various levels of the application directory. What do we call this representation of the collective web application?

{% hint style="success" %}
site map
{% endhint %}

### What is the term for browsing the application as a normal user prior to examining it further?

{% hint style="success" %}
happy path
{% endhint %}

### Which poisoning issue arises when an application behind a cache process input that is not included in the cache key?

{% hint style="success" %}
Web cache poisoning
{% endhint %}

## :repeat: Puttin' it on Repeat\[er]

### Try logging in with invalid credentials. What error is generated when login fails?

![](<../../.gitbook/assets/Screenshot from 2020-09-10 14-14-52.png>)

### Now that we've sent the request to Repeater, let's try adjusting the request such that we are sending a single quote (') as both the email and password. What error is generated from this request?

![](<../../.gitbook/assets/Screenshot from 2020-09-10 14-17-23.png>)

### **What field do we have to modify in order to submit a zero-star review?**

![](<../../.gitbook/assets/Screenshot from 2020-09-10 14-21-45.png>)

## :japanese\_goblin: **** Help! There's an Intruder!

### Which attack type allows us to select multiple payload sets (one per position) and iterate through them simultaneously?

{% hint style="success" %}
Pitchfork
{% endhint %}

### How about the attack type which allows us to use one payload set in every single position we've selected simultaneously?

{% hint style="success" %}
Battering Ram
{% endhint %}

### Which attack type allows us to select multiple payload sets (one per position) and iterate through all possible combinations?

{% hint style="success" %}
Cluster Bomb
{% endhint %}

### Perhaps the most commonly used, which attack type allows us to cycle through our payload set, putting the next available payload in each position in turn?

{% hint style="success" %}
Sniper
{% endhint %}

### Finally, click 'Start attack'. What is the first payload that returns a 200 status code, showing that we have successfully bypassed authentication?

