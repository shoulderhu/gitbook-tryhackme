---
description: https://tryhackme.com/room/ffuf
---

# ffuf

## Walkthrough

### Task 2 Basics

#### What is the first file you found with a 200 status code?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/big.txt \
     -u http://10.10.85.198/FUZZ -t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 20-50-37.png>)

{% hint style="success" %}
`favicon.ico`
{% endhint %}

### Task 3 Finding pages and directories

#### What text file did you find?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt \
     -u http://10.10.3.206/FUZZ -t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 20-52-28.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-04 20-52-39.png>)

{% hint style="success" %}
`robots.txt`
{% endhint %}

#### What two file extensions were found for the index page?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt \
     -u http://10.10.3.206/indexFUZZ -t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 20-55-04.png>)

{% hint style="success" %}
`php,phps`
{% endhint %}

#### What page has a size of 4840?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt \
     -u http://10.10.3.206/FUZZ \
     -e .php,.txt -t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 20-59-16.png>)

{% hint style="success" %}
`about.php`
{% endhint %}

#### How many directories are there?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt \
     -u http://10.10.3.206/FUZZ -t 128 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-03-48.png>)

{% hint style="success" %}
`4`
{% endhint %}

### Task 4 Using filters

#### After applying the fc filter, how many results were returned?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt \
     -u http://10.10.3.206/FUZZ \
     -fc 403  -t 128 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-09-35.png>)

{% hint style="success" %}
`11`
{% endhint %}

#### After applying the mc filter, how many results were returned?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt \
     -u http://10.10.3.206/FUZZ \
     -mc 200 -t 128 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-08-44.png>)

{% hint style="success" %}
`6`
{% endhint %}

#### Which valuable file would have been hidden if you used -fc 403 instead of -fr?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt \
     -u http://10.10.3.206/FUZZ -fr '/\..*'-t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-19-12.png>)

{% hint style="success" %}
`wp-forum.phps`
{% endhint %}

### Task 5 Fuzzing parameters

#### What is the parameter you found?

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt \
     -u http://10.10.42.33/sqli-labs/Less-1/?FUZZ=1 -c -fw 39
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt \
     -u http://10.10.42.33/sqli-labs/Less-1/?FUZZ=1 -c -fw 39 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-28-02.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-33-45.png>)

{% hint style="success" %}
`id`
{% endhint %}

#### What is the highest valid id?

```bash
seq 0 255 | ffuf -w - -u http://10.10.42.33/sqli-labs/Less-1/?id=FUZZ -c -fw 33
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-39-02.png>)

{% hint style="success" %}
`14`
{% endhint %}

#### What is Dummy's password?

```bash
ffuf -w /usr/share/seclists/Passwords/Leaked-Databases/hak5.txt \
     -u http://10.10.42.33/sqli-labs/Less-11/ -c -X POST \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -d "uname=Dummy&passwd=FUZZ&submit=Submit" \
     -fr 'slap.jpg' -t 128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-04 21-55-01.png>)

{% hint style="success" %}
`p@ssword`
{% endhint %}

## Questions

### Task 8 Reviewing the options

#### How do you save the output to a markdown file (ffuf.md)?

{% hint style="success" %}
`-of md -o ffuf.md`
{% endhint %}

#### How do you re-use a raw http request file?

{% hint style="success" %}
`-request`
{% endhint %}

#### How do you strip comments from a wordlist?

{% hint style="success" %}
`-ic`
{% endhint %}

#### How would you read a wordlist from STDIN?

{% hint style="success" %}
`-w -`
{% endhint %}

#### How do you print full URLs and redirect locations?

{% hint style="success" %}
`-v`
{% endhint %}

#### What option would you use to follow redirects?

{% hint style="success" %}
`-r`
{% endhint %}

#### How do you enable colorized output?

{% hint style="success" %}
`-c`
{% endhint %}
