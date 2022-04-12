---
description: https://tryhackme.com/room/nmap03
---

# Nmap Advanced Port Scans

{% embed url="https://tryhackme.com/room/nmap03" %}
https://tryhackme.com/room/nmap03
{% endembed %}

## Task 2 TCP Null Scan, FIN Scan, and Xmas Scan

#### In a null scan, how many flags are set to 1?

{% hint style="success" %}
`0`
{% endhint %}

#### In a FIN scan, how many flags are set to 1?

{% hint style="success" %}
`1`
{% endhint %}

#### In a Xmas scan, how many flags are set to 1?

{% hint style="success" %}
`3`
{% endhint %}

#### Start the VM and load the AttackBox. Once both are ready, open the terminal on the AttackBox and use nmap to launch a FIN scan against the target VM. How many ports appear as open|filtered?

```bash
sudo nmap -n -sF 10.10.79.148
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 05-15-59.png>)

{% hint style="success" %}
`7`
{% endhint %}

#### Repeat your scan launching a null scan against the target VM. How many ports appear as open|filtered?

```bash
sudo nmap -n -sN 10.10.79.148
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 05-16-38 (1).png>)

{% hint style="success" %}
`7`
{% endhint %}

## Task 3 TCP Maimon Scan

* In this scan, the FIN and ACK bits are set.
* Certain BSD-derived systems drop the packet if it is an open port exposing the open ports.
* This scan won’t work on most targets encountered in modern networks

#### In the Maimon scan, how many flags are set?

{% hint style="success" %}
`2`
{% endhint %}

## Task 4 TCP ACK, Window, and Custom Scan

* The target would respond to the ACK with RST regardless of the state of the port.
  * This kind of scan would be helpful if there is a firewall in front of the target.
* The TCP window scan is almost the same as the ACK scan; however, it examines the TCP Window field of the RST packets returned.

#### In TCP Window scan, how many flags are set?

{% hint style="success" %}
`1`
{% endhint %}

#### You decided to experiment with a custom TCP scan that has the reset flag set. What would you add after `--scanflags`?&#x20;

{% hint style="success" %}
`RST`
{% endhint %}

#### The VM received an update to its firewall ruleset. A new port is now allowed by the firewall. After you make sure that you have terminated the VM from Task 2, start the VM for this task. Launch the AttackBox if you haven't done that already. Once both are ready, open the terminal on the AttackBox and use Nmap to launch an ACK scan against the target VM. How many ports appear unfiltered?

```bash
sudo nmap -n -sA 10.10.36.71
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 05-35-18.png>)

{% hint style="success" %}
`4`
{% endhint %}

#### What is the new port number that appeared?

{% hint style="success" %}
`443`
{% endhint %}

#### Is there any service behind the newly discovered port number?

```bash
sudo nmap -n -p443 10.10.36.71
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 05-36-40.png>)

{% hint style="success" %}
`N`
{% endhint %}

## Task 5 Spoofing and Decoys

#### What do you need to add to the command `sudo nmap 10.10.36.71` to make the scan appear as if coming from the source IP address `10.10.10.11` instead of your IP address?

{% hint style="success" %}
`-S 10.10.10.11`
{% endhint %}

#### What do you need to add to the command `sudo nmap 10.10.36.71` to make the scan appear as if coming from the source IP addresses `10.10.20.21` and `10.10.20.28` in addition to your IP address?

{% hint style="success" %}
`-D 10.10.120.21,10.10.20.28,ME`
{% endhint %}

## Task 6 Fragmented Packets

#### If the TCP segment has a size of 64, and `-ff` option is being used, how many IP fragments will you get?

{% hint style="success" %}
`4`
{% endhint %}

## Task 7 Idle/Zombie Scan

The idle scan, or zombie scan, requires an idle system connected to the network that you can communicate with. The idle (zombie) scan requires the following three steps to discover whether a port is open:

1. Trigger the idle host to respond so that you can record the current IP ID on the idle host.
2. Send a SYN packet to a TCP port on the target. The packet should be spoofed to appear as if it was coming from the idle host (zombie) IP address.
3. Trigger the idle machine again to respond so that you can compare the new IP ID with the one received earlier.

#### You discovered a rarely-used network printer with the IP address `10.10.5.5`, and you decide to use it as a zombie in your idle scan. What argument should you add to your Nmap command?

{% hint style="success" %}
`-sI 10.10.5.5`
{% endhint %}

## Task 8 Getting More Details

#### Launch the AttackBox if you haven't done so already. After you make sure that you have terminated the VM from Task 4, start the VM for this task. Wait for it to load completely, then open the terminal on the AttackBox and use Nmap with `nmap -sS -F --reason 10.10.36.71` to scan the VM. What is the reason provided for the stated port(s) being open?

```bash
sudo nmap -n -sS -F --reason 10.10.181.82
```

![](<../../.gitbook/assets/Screenshot from 2022-04-13 06-05-32.png>)

{% hint style="success" %}
`syn-ack`
{% endhint %}
