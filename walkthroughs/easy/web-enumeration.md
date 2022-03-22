# Web Enumeration

## Task 6 Practical: Gobuster

```bash
echo '10.10.152.33 webenum.thm' | sudo tee -a /etc/hosts
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 07-20-55.png>)

#### Run a directory scan on the host. Other than the standard css, images and js directories, what other directories are available?

```bash
gobuster dir -u http://webenum.thm/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 07-27-16.png>)

{% hint style="success" %}
`public,Changes,VIDEO`
{% endhint %}

#### Run a directory scan on the host. In the "C\*\*\*\*\*\*" directory, what file extensions exist?

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-17-13.png>)

{% hint style="success" %}
`conf,js`
{% endhint %}

#### There's a flag out there that can be found by directory scanning! Find it!

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-21-05.png>)

{% hint style="success" %}
`thm{n1c3_w0rk}`
{% endhint %}

#### There are some virtual hosts running on this server. What are they?

```bash
gobuster vhost -u http://webenum.thm/ \
               -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt \
               -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-24-48.png>)

{% hint style="success" %}
`learning,products`
{% endhint %}

#### There's another flag to be found in one of the virtual hosts! Find it!

```
echo '10.10.203.171 learning.webenum.thm' | sudo tee -a /etc/hosts
echo '10.10.203.171 products.webenum.thm' | sudo tee -a /etc/hosts
```

```bash
gobuster dir -u http://products.webenum.thm/ \
             -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt \
             -x txt -t128
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-40-52.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-41-59.png>)

{% hint style="success" %}
`thm{gobuster_is_fun}`
{% endhint %}

## Task 8 WPScan Modes

#### What would be the full URL for the theme "twentynineteen" installed on the WordPress site: "http://cmnatics.playground"

{% hint style="success" %}
`http://cmnatics.playground/wp-content/themes/twentynineteen`
{% endhint %}

#### What argument would we provide to enumerate a WordPress site?

{% hint style="success" %}
`enumerate`
{% endhint %}

#### What is the name of the other aggressiveness profile that we can use in our WPScan command?

{% hint style="success" %}
`passive`
{% endhint %}

## Task 9 Practical: WPScan

```
echo '10.10.69.54 wpscan.thm' | sudo tee -a /etc/hosts
```

#### Enumerate the site, what is the name of the theme that is detected as running?

```bash
wpscan --url wpscan.thm -e t
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-51-25.png>)

{% hint style="success" %}
`twentynineteen`
{% endhint %}

#### WPScan says that this theme is out of date, what does it suggest is the number of the latest version?

{% hint style="success" %}
`2.0`
{% endhint %}

#### Enumerate the site, what is the name of the plugin that WPScan has found?

```bash
wpscan --url wpscan.thm -e p
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-53-16.png>)

{% hint style="success" %}
`nextgen-gallery`
{% endhint %}

#### Enumerate the site, what username can WPScan find?

```bash
wpscan --url wpscan.thm -e u
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-54-21.png>)

{% hint style="success" %}
`Phreakazoid`
{% endhint %}

#### Construct a WPScan command to brute-force the site with this username, using the rockyou wordlist as the password list. What is the password to this user?

```bash
wpscan --url wpscan.thm --usernames phreakazoid \
       --passwords /usr/share/wordlists/rockyou.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 19-57-14.png>)

{% hint style="success" %}
`linkinpark`
{% endhint %}

## Task 11 Nikto Modes

#### What argument would we use if we wanted to scan **port 80** and **8080** on a host?

{% hint style="success" %}
`-p 80,8080`
{% endhint %}

#### What argument would we use if we wanted to see any cookies given by the web server?

{% hint style="success" %}
`-Display 2`
{% endhint %}

## Task 12 Nikto Practical

#### What is the name & version of the web server that  Nikto has determined running on **port 80?**

```bash
nikto -h 10.10.213.107 -p 80
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 20-23-33.png>)

{% hint style="success" %}
`Apache/2.4.7`
{% endhint %}

#### There is another web server running on another port. What is the name & version of this web server?

```bash
nmap -n -sV 10.10.213.107
nikto -h 10.10.213.107 -p  -Display 2
```

![](<../../.gitbook/assets/Screenshot from 2022-03-22 20-26-22.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-22 20-32-41.png>)

{% hint style="success" %}
`Apache-Coyote/1.1`
{% endhint %}

#### What is the name of the Cookie that this JBoss server gives?

{% hint style="success" %}
`JSESSIONID`
{% endhint %}
