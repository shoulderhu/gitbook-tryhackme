# Regular expressions

## Task 2 Charsets

#### Match all of the following characters: c, o, g

{% hint style="success" %}
`[cog]`
{% endhint %}

#### Match all of the following words: cat, fat, hat

{% hint style="success" %}
`[cfh]at`
{% endhint %}

#### Match all of the following words: Cat, cat, Hat, hat

{% hint style="success" %}
`[CcHh]at`
{% endhint %}

#### Match all of the following words: Cat, cat, Hat, hat

{% hint style="success" %}
`[Ff]ile[1-9]`
{% endhint %}

#### Match all of the filenames of question 4, except "File7"

{% hint style="success" %}
`[Ff]ile[^7]`
{% endhint %}

## Task 3 Wildcards and optional characters

#### Match all of the following words: Cat, fat, hat, rat

{% hint style="success" %}
`.at`
{% endhint %}

#### Match all of the following words: Cat, cats

{% hint style="success" %}
`[Cc]ats?`
{% endhint %}

#### Match the following domain name: cat.xyz

{% hint style="success" %}
`cat\.xyz`
{% endhint %}

#### Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz

{% hint style="success" %}
`[ch]ats?\.xyz`
{% endhint %}

#### Match every 4-letter string that doesn't end in any letter from n to z

{% hint style="success" %}
`...[^n-z]`
{% endhint %}

#### Match bat, bats, hat, hats, but not rat or rats

{% hint style="success" %}
`[^r]ats?`
{% endhint %}

## Task 4 Metacharacters and repetitions

#### Match the following word: catssss

{% hint style="success" %}
`cats{4}`
{% endhint %}

#### Match all of the following words: Cat, cats, catsss

{% hint style="success" %}
`[Cc]ats*`
{% endhint %}

#### Match all of the following sentences: regex go br, regex go brrrrrr

{% hint style="success" %}
`regex go br+`
{% endhint %}

#### Match all of the following filenames: ab0001, bb0000, abc1000, cba0110, c0000&#x20;

{% hint style="success" %}
`[abc]{1,3}[01]{4}`
{% endhint %}

#### Match all of the following filenames: File01, File2, file12, File20, File99

{% hint style="success" %}
`[Ff]ile\d{1,2}`
{% endhint %}

#### Match all of the following folder names: kali tools, kali tools

{% hint style="success" %}
`kali\s+tools`
{% endhint %}

#### Match all of the following filenames: notes\~, stuff@, gtfob#, lmaoo!

{% hint style="success" %}
\w{5}\W
{% endhint %}

#### Match the string in quotes: "2f0h@f0j0%! a)K!F49h!FFOK"

{% hint style="success" %}
`\S*\s*\S*`
{% endhint %}

#### Match every 9-character string (with letters, numbers, and symbols) that doesn't end in a "!" sign

{% hint style="success" %}
`\S{8}[^!]`
{% endhint %}

#### Match all of these filenames (use the + symbol): .bash\_rc, .unnecessarily\_long\_filename, and note1

{% hint style="success" %}
`\.?\w+`
{% endhint %}

## Task 5 Starts with/ ends with, groups, and either/ or

#### Match every string that starts with "Password:" followed by any 10 characters excluding "0"

{% hint style="success" %}
`^Password:[^0]{10}`
{% endhint %}

#### Match "username: " in the beginning of a line

{% hint style="success" %}
`^username:\s`
{% endhint %}

#### Match every line that doesn't start with a digit

{% hint style="success" %}
`^\D`
{% endhint %}

#### Match this string at the end of a line: EOF$

{% hint style="success" %}
`EOF\$$`
{% endhint %}

#### Match all of the following sentences:

* I use nano
* I use vim

{% hint style="success" %}
`I use (nano|vim)`
{% endhint %}

#### Match all lines that start with $, followed by any single digit, followed by $, followed by one or more non-whitespace characters

{% hint style="success" %}
`$\$\d\$\S+`
{% endhint %}

#### Match every possible IPv4 IP address

{% hint style="success" %}
`(\d{1,3}.){3}\d{1,3}`
{% endhint %}

#### Match all of these emails while also adding the username and the domain name (not the TLD) in separate groups: [hello@tryhackme.com](mailto:hello@tryhackme.com), [username@domain.com](mailto:username@domain.com), [dummy\_email@xyz.co](mailto:dummy\_email@xyz.com)m

{% hint style="success" %}
`(\w+)@(\w+)\.com`
{% endhint %}
