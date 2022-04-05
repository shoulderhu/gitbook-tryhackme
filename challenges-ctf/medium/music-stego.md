# Music Stego

{% embed url="https://tryhackme.com/room/musicalstego" %}
https://tryhackme.com/room/musicalstego
{% endembed %}

## Task 1 Musical Steganography Challenge

#### Who remixed the song?

```bash
exiftool Language\ Arts\ \ DEF\ CON\ 27\ The\ Official\ Soundtrack\ .wav
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 06-31-03 (1).png>)

{% hint style="success" %}
`Kilmanjaro`
{% endhint %}

#### What link is hiding in the music?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 07-23-01 (1).png>)

```bash
import cv2

img = cv2.imread("/media/vboxsf/qrcode.png", 2)
ret, bw_img = cv2.threshold(img, 100, 255, cv2.THRESH_BINARY)
cv2.imshow("qrcode", bw_img)
cv2.waitKey(0)
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 07-24-46 (1).png>)

{% hint style="success" %}
`https://voca.ro/imPgJC013AW`
{% endhint %}

#### What does the found audio convert to?

![](<../../.gitbook/assets/Screenshot from 2022-04-05 07-28-01.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-05 07-28-09 (1).png>)

{% hint style="success" %}
`https://pastebin.com/LZKTB4ET`
{% endhint %}

#### What was the found password?

> https://github.com/m00-git/LZKTB4ET

![](<../../.gitbook/assets/image (5).png>)

{% hint style="success" %}
`S3CR3T_P455`
{% endhint %}

#### What is the final flag?

```bash
steghide extract -sf Language\ Arts\ \ DEF\ CON\ 27\ The\ Official\ Soundtrack\ .wav \
                 -p S3CR3T_P455
cat secret
```

![](<../../.gitbook/assets/Screenshot from 2022-04-05 07-48-23.png>)

{% hint style="success" %}
`THM{f0und_m3!}`
{% endhint %}

## Reference

{% embed url="https://www.turkhackteam.org/konular/tryhackme-musical-stego-ctf-writeup.2011580" %}
![](<../../.gitbook/assets/image (5).png>)
{% endembed %}
