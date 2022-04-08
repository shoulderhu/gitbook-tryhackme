# Packets & Frames

{% embed url="https://tryhackme.com/room/packetsframes" %}
https://tryhackme.com/room/packetsframes
{% endembed %}

## Task 1 What are Packets and Frames

#### What is the name for a piece of data when it **does have** IP addressing information?

{% hint style="success" %}
`packet`
{% endhint %}

#### What is the name for a piece of data when it **does not have** IP addressing information?

{% hint style="success" %}
`frame`
{% endhint %}

## Task 2 TCP/IP (The Three-Way Handshake)

#### What is the header in a TCP packet that ensures the integrity of data?

{% hint style="success" %}
`checksum`
{% endhint %}

#### Provide the order of a normal Three-way handshake (with each step separated by a comma)

{% hint style="success" %}
`SYN,SYN/ACK,ACK`
{% endhint %}

## Task 3 Practical - Handshake

#### What is the value of the flag given at the end of the conversation?

* SYN：Can you hear me Bob?
* SYN/ACK：Yes, I can hear you!
* ACK：Okay Great
* DATA：Cheesecake is on sale!
* ACK：I Hear ya!
* FIN/ACK：I'm all done
* FIN/ACK：Yeah Me Too
* ACK：Okay, Goodbye

![](<../../.gitbook/assets/Screenshot from 2022-04-08 05-59-36.png>)

{% hint style="success" %}
`THM{TCP_CHATTER}`
{% endhint %}

## Task 4 UDP/IP

#### What does the term "UDP" stand for?

{% hint style="success" %}
`User Datagram Protocol`
{% endhint %}

#### What type of connection is "UDP"?

{% hint style="success" %}
`stateless`
{% endhint %}

#### What protocol would you use to transfer a file?

{% hint style="success" %}
`TCP`
{% endhint %}

#### What protocol would you use to have a video call?

{% hint style="success" %}
`UDP`
{% endhint %}

## Task 5 Ports 101 (Pratical)

#### What is the flag received from the challenge?

![](<../../.gitbook/assets/Screenshot from 2022-04-08 06-13-46.png>)

{% hint style="success" %}
`THM{YOU_CONNECTED_TO_A_PORT}`
{% endhint %}
