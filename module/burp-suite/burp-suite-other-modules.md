# Burp Suite: Other Modules

{% embed url="https://tryhackme.com/room/burpsuiteom" %}
https://tryhackme.com/room/burpsuiteom
{% endembed %}

## Decoder

### Task 3 Encoding/Decoding

#### Base64 encode the phrase: `Let's Start Simple`. What is the base64 encoded version of this text?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 11-51-16.png>)

{% hint style="success" %}
`TGV0J3MgU3RhcnQgU2ltcGxl`
{% endhint %}

#### URL Decode this data: `%4e%65%78%74%3a%20%44%65%63%6f%64%69%6e%67`. What is the plaintext returned?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 11-52-47.png>)

{% hint style="success" %}
`Next: Decoding`
{% endhint %}

#### Use Smart Decode to decode this data: `&#x25;&#x33;&#x34;&#x25;&#x33;&#x37;`. What is the decoded text?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 11-56-18.png>)

{% hint style="success" %}
`47`
{% endhint %}

#### Encode this phrase: `Encoding Challenge`. Start with _base64_ encoding. Take the output of this and convert it into _ASCII Hex_. Finally, encode the hex string into _octal._ What is the final string?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 11-57-40.png>)

{% hint style="success" %}
`24034214a720270024142d541357471232250253552c1162d1206c`
{% endhint %}

### Task 4 Hashing

#### Using Decoder, what is the SHA-256 hashsum of the phrase: `Let's get Hashing!`? Convert this into an `ASCII Hex` string for the answer to this question.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 12-06-36.png>)

{% hint style="success" %}
`6b72350e719a8ef5af560830164b13596cb582757437e21d1879502072238abe`
{% endhint %}

#### Generate an MD4 hashsum of the phrase: `Insecure Algorithms`. Encode this as **base64**  before submitting.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 12-17-12.png>)

{% hint style="success" %}
`TcV4QGZZN7y7lwYFRMMoeA==`
{% endhint %}

#### Let's look at an in-context example: First, download the file attached to this task.

```bash
wget http://10.10.151.95:9999/AlteredKeys.zip
```

#### Now read the problem specification below:

#### _"Some joker has messed with my SSH key! There are four keys in the directory, and I have no idea which is the real one. The MD5 hashsum for my key is `3166226048d6ad776370dc105d40d9f8` -- could you find it for me?"_

#### Submit the correct key name as your answer.

```bash
md5sum keys/key1 keys/key2 keys/key3 keys/key4
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 12-11-11.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 12-15-40.png>)

{% hint style="success" %}
`key3`
{% endhint %}

## Comparer

### Task  6 Example

#### Navigate to `http://10.10.131.123/support/login`

#### Try to login with an invalid username and password -- capture the request in the [Burp Proxy](https://tryhackme.com/room/burpsuitebasics).

![](<../../.gitbook/assets/Screenshot from 2022-03-27 16-49-49.png>)

#### Send the request to [Repeater](https://tryhackme.com/room/burpsuiterepeater) with Ctrl + R (or Mac equivalent), or by right-clicking on the request in Proxy and choosing to "Send to Repeater".

![](<../../.gitbook/assets/Screenshot from 2022-03-27 16-52-14.png>)

#### Send the request, then right-click on the response and choose "Send to Comparer".

#### In the Repeater tab, change the credentials to:

* Username: `support_admin`
* Password: `w58ySK4W`

![](<../../.gitbook/assets/Screenshot from 2022-03-27 16-53-24.png>)

#### Send the request again, then pass the new response into Comparer.  Compare the two responses by word. Can you identify the main differences?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 16-54-44.png>)

## Sequencer

### Task 7 Overview

In short, Sequencer allows us to measure the _**entropy**_ (or randomness, in other words) of "tokens" -- strings that are used to identify something and should, in theory, be generated in a cryptographically secure manner. For example, we may wish to analyze the randomness of a session cookie or a **C**ross-**S**ite **R**equest **F**orgery (CSRF) token protecting a form submission. If it turns out that these tokens are not generated securely, then we can (in theory) predict the values of upcoming tokens.

There are two main methods we can use to perform token analysis with Sequencer:

* **Live capture** is the more common of the two methods -- this is the default sub-tab for Sequencer. Live capture allows us to pass a request to Sequencer, which we know will create a token for us to analyze. For example, we may wish to pass a POST request to a login endpoint into Sequencer, as we know that the server will respond by giving us a cookie. With the request passed in, we can tell Sequencer to start a live capture: it will then make the same request thousands of times automatically, storing the generated token samples for analysis. Once we have accumulated enough samples, we stop Sequencer and allow it to analyze the captured tokens.
* **Manual load** allows us to load a list of pre-generated token samples straight into Sequencer for analysis. Using Manual Load means we don't have to make thousands of requests to our target (which is both loud and resource intensive), but it does mean that we need to obtain a large list of pre-generated tokens!

### Task 8 Live Capture

#### Follow the steps above to perform entropy analysis on the `loginToken` set by the `/admin/login` route of our target web app.

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-04-17.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-05-16.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-08-00.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-15-40.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-28-59.png>)

#### Try performing the capture again, but this time monitor your requests in [Wireshark](https://tryhackme.com/room/wireshark). Can you see why live capturing the requests for this analysis can be described as "loud"?

![](<../../.gitbook/assets/Screenshot from 2022-03-27 17-28-07.png>)
