# NIS-Linux Part I

## Task 1 What is this room about?

#### What is the user you are logged in to in the first room of Linux Fundamentals Part 1?

{% hint style="success" %}
`tryhackme`
{% endhint %}

#### What badge do you receive when you complete all the Linux Fundamentals rooms?

{% hint style="success" %}
`cat linux.txt`
{% endhint %}

## Task 2 ls

#### How do you run the ls command?

{% hint style="success" %}
`ls`
{% endhint %}

#### How do you run the ls command to show all the files inside the folder?

{% hint style="success" %}
`ls -a`
{% endhint %}

#### How do you run the ls command to not show the current directory and the previous directory in the output?

{% hint style="success" %}
`ls -A`
{% endhint %}

#### How do you show the information in a long listing format using ls?

{% hint style="success" %}
`ls -l`
{% endhint %}

#### How do you show the size in readable format?

{% hint style="success" %}
`ls -h`
{% endhint %}

#### How do you do a recursive ls?

{% hint style="success" %}
`ls --recursive`
{% endhint %}

#### How many files did you locate in the home folder of the user?

```
ls
```

{% hint style="success" %}
`13`
{% endhint %}

## Task 3 cat

#### What is the content of cat.txt?

```
cat cat.txt
```

{% hint style="success" %}
`THM{11adbee391acdffee901}`
{% endhint %}

#### What is the content of tac.txt?

```
cat tac.txt
```

{% hint style="success" %}
`THM{acab0111aaa687912139}`
{% endhint %}

#### What is the content of head.txt?

```
cat head.txt
```

{% hint style="success" %}
`THM{894abac55f7962abc166}`
{% endhint %}

#### What is the content of tail.txt?

```
cat tail.txt
```

{% hint style="success" %}
`THM{1689acafdd20751acff6}`
{% endhint %}

#### What is the content of xxd.txt?

```
cat xxd.txt
```

{% hint style="success" %}
`THM{fac1aab210d6e4410acd}`
{% endhint %}

#### What is the content of base64.txt?

```
cat base64.txt
```

{% hint style="success" %}
`THM{aa462c1b2d44801c0a31}`
{% endhint %}

## Task 4 find

#### How many .txt files did you find in the current folder?

```bash
find . -type f -name '*.txt'
```

{% hint style="success" %}
`8`
{% endhint %}

#### How many SUID files have you found inside the home folder?

```
find . -type f -perm -4000
```

{% hint style="success" %}
`0`
{% endhint %}

## Task 5 grep

#### How many times does the word "hacker" appear in the grep files?

```
grep -oh --color hacker grep*
```

{% hint style="success" %}
`15`
{% endhint %}

## Task 6 sudo&#x20;

#### Is the user allowed to run the above command?

```
sudo -l
```

{% hint style="success" %}
`Nay`
{% endhint %}

## Task 8 echo

#### What command would you use to echo the word "Hackerman" ?

{% hint style="success" %}
`echo "Hackerman"`
{% endhint %}

## Task 9 xargs

#### How would you read all files with extension .bak using xargs?

{% hint style="success" %}
find / -name \*.bak -type f -print | xargs /bin/cat
{% endhint %}

## Task 11 curl

#### How would you grab the headers silently of https://tryhackme.com but grepping only the HTTP status code?

{% hint style="success" %}
`curl -I -s https://tryhackme.com | grep HTTP`
{% endhint %}

## Task 12 wget

#### What command would you run to get the flag.txt from https://tryhackme.com/ ?

{% hint style="success" %}
`wget https://tryhackme.com/flag.txt`
{% endhint %}

#### What command would you run to download recursively up to level 5 from https://tryhackme.com ?

{% hint style="success" %}
`wget -r -l 05 https://tryhackme.com`
{% endhint %}

## Task 13 tar

#### What is the flag from the tar file?

```bash
tar xvf tarball.tar
cat flag.txt
```

{% hint style="success" %}
`THM{C0FFE1337101}`
{% endhint %}

## Task 14 gzip

#### What is the content of gzip.txt?

```bash
gzip -d gzip.txt.gz
cat gzip.txt
```

{% hint style="success" %}
`THM{0AFDECC951A}`
{% endhint %}

## Task 15 7zip

#### What is the flag inside the 7zip file?

```bash
7z x zip.7z
cat 7zip.txt
```

{% hint style="success" %}
`THM{526accdf94}`
{% endhint %}

## Task 16 binwalk

#### What is the content of binwalk.txt?

```bash
binwalk -Me binwalk.png
cat /home/chad/_binwalk.png.extracted/binwalk.txt
```

{% hint style="success" %}
`THM{af5548a12bc2de}`
{% endhint %}
