# Intro to Digital Forensics

{% embed url="https://tryhackme.com/room/introdigitalforensics" %}
https://tryhackme.com/room/introdigitalforensics
{% endembed %}

## Task 1 Introduction To Digital Forensics

* Public-sector investigations
* Private-sector investigations

![](<../../.gitbook/assets/image (4) (1).png>)

#### Consider the desk in the photo above. In addition to the smartphone, camera, and SD cards, what would be interesting for digital forensics?

{% hint style="success" %}
`laptop`
{% endhint %}

## Task 2 Digital Forensics Process

#### It is essential to keep track of who is handling it at any point in time to ensure that evidence is admissible in the court of law. What is the name of the documentation that would help establish that?

{% hint style="success" %}
`chain of custody`
{% endhint %}

## Task 3 Practical Example of Digital Forensics

#### Using `pdfinfo`, find out the author of the attached PDF file.

```bash
unzip ransomlettter2.zip
pdfinfo 
```

![](<../../.gitbook/assets/Screenshot from 2022-03-30 05-32-37.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-30 05-40-01.png>)

{% hint style="success" %}
`Ann Gree Shepherd`
{% endhint %}

#### Using `exiftool` or any similar tool, try to find where the kidnappers took the image they attached to their document. What is the name of the street?

```bash
exiftool letter-image.jpg | grep 'GPS Position' | sed 's/ deg/°/g'
```

![](<../../.gitbook/assets/Screenshot from 2022-03-30 05-49-19.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-30 05-53-02.png>)

{% hint style="success" %}
`Milk Street`
{% endhint %}

#### What is the model name of the camera used to take this photo?

```bash
exiftool letter-image.jpg | grep 'Camera Model Name'
```

![](<../../.gitbook/assets/Screenshot from 2022-03-30 05-52-29.png>)

{% hint style="success" %}
`Canon EOS R6`
{% endhint %}
