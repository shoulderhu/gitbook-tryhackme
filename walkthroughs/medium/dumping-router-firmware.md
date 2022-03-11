---
description: https://tryhackme.com/room/rfirmware
---

# Dumping Router Firmware

## Task 1 Preparation

```bash
git clone https://github.com/Sq00ky/Dumping-Router-Firmware-Image/   
cd Dumping-Router-Firmware-Image 
7z x FW_WRT1900ACSV2_2.0.3.201002_prod.zip
sha256sum FW_WRT1900ACSV2_2.0.3.201002_prod.img
```

## Task 2 Investigating Firmware

#### While running a strings on the file, there is a lot of notable clear text. This is due to certain aspects of the firmware image not being encrypted. This likely means that with Binwalk, we will be able to dump the firmware from the image.

#### Running strings on the file, what does the first clear text line say?

```bash
strings FW_WRT1900ACSV2_2.0.3.201002_prod.img | head -n1
```

![strings FW\_WRT1900ACSV2\_2.0.3.201002\_prod.img | head -n1](<../../.gitbook/assets/Screenshot from 2022-02-20 13-58-04.png>)

{% hint style="success" %}
`Linksys WRT1900ACS Router`
{% endhint %}

#### Also using strings, what operating system is the device running?

```bash
strings FW_WRT1900ACSV2_2.0.3.201002_prod.img | sed -n '6p'
# Uncompressing Linux...
```

{% hint style="success" %}
`Linux`
{% endhint %}

#### Scrolling through with strings, you may notice some other interesting lines like /bin/busybox and various other lua files. It really makes you wonder whats going on inside there...

#### Next we will be dumping the filesystem from the image file. To do so, we will be using a tool called binwalk.

#### Binwalk is a tool that checks for well known file signatures within a given file. This can be useful for many things, it even has its uses in Steganography. A file could be hidden within the photo and Binwalk would reveal that, and help us extract it. We will be using it to extract the filesystem of the router in this instance.

#### What option within Binwalk will allow us to extract files from the firmware image?

{% hint style="success" %}
`-e`
{% endhint %}

#### Now that we know how to extract the contents of the firmware image, what was the first item extracted?

```bash
binwalk -e FW_WRT1900ACSV2_2.0.3.201002_prod.img 
```

![binwalk -e FW\_WRT1900ACSV2\_2.0.3.201002\_prod.img](<../../.gitbook/assets/Screenshot from 2022-02-20 14-17-35.png>)

{% hint style="success" %}
`uImage header`
{% endhint %}

#### What was the creation date?

{% hint style="success" %}
`2020-04-22 11:07:26`
{% endhint %}

#### The Cyclical Redundancy Check is used in a similar way that file hashing is, to ensure that the file contents were not corrupted and or modified in transit.

#### What is the CRC of the **image**?

{% hint style="success" %}
`0xABEBC439`
{% endhint %}

#### What is the image size?

{% hint style="success" %}
`4229755 bytes`
{% endhint %}

#### What architecture does the device run?

{% hint style="success" %}
`ARM`
{% endhint %}

#### Researching the results to question 10, is that true?

{% hint style="success" %}
`yes`
{% endhint %}

#### You will notice two files got extracted; one being the jffs2 file system and another that Binwalk believes it to be gzip compressed data. You can attempt to extract the data, however, you won't get anywhere. Binwalk misinterpreted the data, however, we can still do some analysis of it.

#### Running strings on 6870, we notice a large chunk of clear text. We can actually run binwalk again on this file to receive even more files to investigate. Interestingly enough, a copy of the Linux kernel is included. What version is it for?

```bash
cd _FW_WRT1900ACSV2_2.0.3.201002_prod.img.extracted
strings 6870 | grep linux | head -n5
```

![strings 6870 | grep linux | head -n5](<../../.gitbook/assets/Screenshot from 2022-02-20 14-29-48.png>)

{% hint style="success" %}
`3.10.39`
{% endhint %}

#### If you run extract the contents of 6870 with Binwalk and run strings on 799E38.cpio, you may see a lot of hex towards the bottom of the file. Some of it can be translated into human readable text. Some of it is interesting to see and really makes you wonder what its purpose was for. Maybe some additional investigation will reveal its purpose.

```bash
binwalk -e 6870
cd _6870.extracted
strings 799E38.cpio | tail -n88 | head -n47
```

#### Continuing on with the analysis, we have a jffs2 file system that we can examine the contents of. First, we need to mount it though, which brings us into the next section

```bash
cd ..
```

## Task 3 Mounting and Analysis of the Router's Filesystem

```bash
sudo rm -rf /dev/mtdblock0
sudo mknod /dev/mtdblock0 b 31 0

sudo modprobe jffs2
sudo modprobe mtdram
sudo modprobe mtdblock

sudo dd if=600000.jffs2 of=/dev/mtdblock0

sudo mkdir /mnt/jffs2
sudo mount -t jffs2 /dev/mtdblock0 /mnt/jffs2
cd /mnt/jffs2
```

#### Running an ls -la reveals a lot of interesting information. First we notice that a lot of files are symbolically linked.

```bash
ls -la
```

![ls -la](<../../.gitbook/assets/Screenshot from 2022-02-20 15-03-23.png>)

#### Where does linuxrc link to?

{% hint style="success" %}
/bin/busybox
{% endhint %}

#### What parent folder does mnt, opt, and var link to?

{% hint style="success" %}
`/tmp/`
{% endhint %}

#### What folder would store the router's HTTP server?

{% hint style="success" %}
`/www/`
{% endhint %}

#### Scanning through a lot of these folders, you may begin to notice that they are empty. This is extremely strange, but that is because the router is not up and running. Remember, we are mearly looking at a template of the filesystem that is going to be flashed onto the router, not the firmware from a router that has been dumped. Other information about the router may be contained in the previous section within the 6870 block.

#### The first of the folders that isn't empty is /bin/, where do a majority of the files link to? Why is that? Well, [busybox is more or less a tool suite of common executable commands within the Unix environment](https://ubuntuforums.org/archive/index.php/t-846852.html).

```bash
ls -l bin/
```

![ls -l bin](<../../.gitbook/assets/Screenshot from 2022-02-20 15-11-03.png>)

{% hint style="success" %}
`busybox`
{% endhint %}

#### Within the bin folder, interestingly enough, what database would be running if the router was online?

```bash
ls bin | grep -i sql
```

{% hint style="success" %}
`sqlite3`
{% endhint %}

#### The next notable folder of interest is /etc/. This folder contains a lot of configuration files for the router, such as Access Point power levels regulated by certain countries. One you might recognize is the FCC (Federal Communications Commission).

#### We can even see the build date of the device. What is the build date?&#x20;

```bash
ls etc | grep -i date
cat etc/builddate
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 15-16-19.png>)

{% hint style="success" %}
`2020-04-22 11:44`
{% endhint %}

#### <mark style="color:red;">There are even files related to the SSH server on the device. What SSH server does the device run?</mark>

![](<../../.gitbook/assets/Screenshot from 2022-02-20 16-19-38.png>)

{% hint style="success" %}
<mark style="color:red;background-color:blue;">`dropbear`</mark>
{% endhint %}

#### We can even see the file for the media server, which company developed it? This company use to own Linksys at one point in time, which is likely why it is still being used.

```bash
ls etc | grep -i media
head etc/mediaserver.ini
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 15-27-44.png>)

#### Which file within /etc/ contains a list of common Network services and their associated port numbers?

```bash
ls etc | grep -i service
cat etc/services | grep -v '^#' | head
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 15-31-15.png>)

{% hint style="success" %}
`services`
{% endhint %}

#### Which file contains the default system settings?

```bash
ls etc | grep -i default 
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 15-33-47.png>)

{% hint style="success" %}
`system_defaults`
{% endhint %}

#### Within the /etc/ folder, what is the version specific firmware version?

```bash
cat etc/version
```

{% hint style="success" %}
`2.0.3.201002`
{% endhint %}

#### Backing out into the JNAP folder, the JNAP API has been a potential attack vector and vulnerability in the past, which this article highlights [here](https://routersecurity.org/hnap.php). Interestingly enough, reminense of it is still here today on Linksys devices. Going to  http://\<Default\_Gateway>/JNAP/ on a Linksys router reveals an interesting 404. Much different than the standard 404.

#### which makes you wonder if something is still really there. If you investigate within /JNAP/modules folder back on the dumped filesystem, you will see some contents related to the device and what services it offers, some of them are firewalls, http proxies, QoS, VPN servers, uPnP, SMB, MAC filtering, FTP, etc.

#### What 3 networks have a folder within /JNAP/modules?

```bash
find JNAP/modules/ -type d
```

![find JNAP/modules/ -type d](<../../.gitbook/assets/Screenshot from 2022-02-20 15-44-39.png>)

{% hint style="success" %}
`guest_lan, wan, lan`
{% endhint %}

#### After then JNAP folder, lib is the only other folder that really has any contents whatsoever and whats in there is pretty standard in terms of libraries. The rest of the file system is relatively bare which leads us to the end of this room.

## Reference

{% embed url="https://github.com/jakekara/jnap" %}
