# Snort

{% embed url="https://tryhackme.com/room/snort" %}
https://tryhackme.com/room/snort
{% endembed %}

## Task 2 Interactive Material and VM

#### Navigate to the Task-Exercises folder and run the command "./.easy.sh" and write the output

```bash
cd Desktop/Task-Exercise
./.easy.sh
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 06-34-30.png>)

{% hint style="success" %}
`Too Easy!`
{% endhint %}

## Task 3 Introduction to IDS/IPS

#### Which snort mode can help you stop the threats on a local machine?

{% hint style="success" %}
`HIPS`
{% endhint %}

#### Which snort mode can help you detect threats on a local network?

{% hint style="success" %}
`NIDS`
{% endhint %}

#### Which snort mode can help you detect the threats on a local machine?

{% hint style="success" %}
`HIDS`
{% endhint %}

#### Which snort mode can help you stop the threats on a local network?

{% hint style="success" %}
`NIPS`
{% endhint %}

#### Which snort mode works similar to NIPS mode?

{% hint style="success" %}
`NBA`
{% endhint %}

#### According to the official description of the snort, what kind of NIPS is it?

{% hint style="success" %}
`full-blown`
{% endhint %}

#### NBA training period is also known as ...

{% hint style="success" %}
`baselining`
{% endhint %}

## Task 4 First Interaction with Snort

#### Run the Snort instance and check the build number.

```bash
snort -V
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 06-59-55.png>)

{% hint style="success" %}
`149`
{% endhint %}

#### Test the current instance with "**/etc/snort/snort.conf**" file and check how many rules are loaded with the current build.

```bash
sudo snort -c /etc/snort/snort.conf -T
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 07-01-29.png>)

{% hint style="success" %}
`4151`
{% endhint %}

#### Test the current instance with "**/etc/snort/snortv2.conf**" file and check how many rules are loaded with the current build.

```bash
suod snort -c /etc/snort/snortv2.conf -T
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 07-02-47.png>)

{% hint style="success" %}
`1`
{% endhint %}

## Task 6 Operation Mode 2: Packet Logger Mode

#### Investigate the traffic with the default configuration file with ASCII mode.

```bash
cd TASK-6
sudo snort -i eth0 -dev -l . -K ASCII
```

#### Execute the traffic generator script and choose "TASK-6 Exercise". Wait until the traffic ends, then stop the Snort instance. Now analyse the output summary and answer the question.

```bash
sudo ./traffic-generator.sh
```

#### Now, you should have the logs in the current directory. Navigate to folder "145.254.160.237". What is the source port used to connect port 53?

```bash
sudo cat 145.254.160.237/UDP:3009-53
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 20-43-00.png>)

#### Use snort.log.1640048004

#### Read the snort.log file with Snort; what is the IP ID of the 10th packet?

```bash
snort -r snort.log.1640048004 -n 10
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 20-46-16 (1).png>)

{% hint style="success" %}
`49313`
{% endhint %}

#### Read the "**snort.log.1640048004"** file with Snort; what is the referer of the 4th packet?

```bash
snort -r snort.log.1640048004 -X -n 4
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 20-52-15.png>)

{% hint style="success" %}
`http://www.ethereal.com/development.html`
{% endhint %}

#### Read the "**snort.log.1640048004"** file with Snort; what is the Ack number of the 8th packet?

```bash
snort -r snort.log.1640048004 -n 8
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 20-51-45.png>)

{% hint style="success" %}
`0x38AFFFF3`
{% endhint %}

#### Read the "**snort.log.1640048004"** file with Snort; what is the number of the **"TCP port 80"** packets?

```bash
snort -r snort.log.1640048004 'tcp and port 80'
```

![](<../../.gitbook/assets/Screenshot from 2022-05-09 20-55-13.png>)

{% hint style="success" %}
`41`
{% endhint %}

## Task 7 Operation Mode 3: IDS/IP

#### Investigate the traffic with the default configuration file.

```bash
cd ../TASK-7
sudo snort -c /etc/snort/snort.conf -A full -l .
```

#### Execute the traffic generator script and choose **"TASK-7 Exercise"**. Wait until the traffic stops, then stop the Snort instance. Now analyse the output summary and answer the question.

```bash
sudo ./traffic-generator.sh
```

#### What is the number of the detected HTTP GET methods?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-19-51.png>)

{% hint style="success" %}
`2`
{% endhint %}

## Task 8 Operation Mode 4: PCAP Investigation

#### Investigate the **mx-1.pcap** file with the default configuration file.

```bash
cd ../TASK-8
sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-1.pcap
```

#### What is the number of the generated alerts?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-29-10.png>)

{% hint style="success" %}
`170`
{% endhint %}

#### Keep reading the output. How many TCP Segments are Queued?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-30-58.png>)

{% hint style="success" %}
`18`
{% endhint %}

#### Keep reading the output.How many "HTTP response headers" were extracted?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-31-52.png>)

{% hint style="success" %}
`3`
{% endhint %}

#### Investigate the mx-1.pcap file **with the second** configuration file.

```bash
sudo snort -c /etc/snort/snortv2.conf -A full -l . -r mx-1.pcap
```

#### What is the number of the generated alerts?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-34-12.png>)

{% hint style="success" %}
`68`
{% endhint %}

#### Investigate the **mx-2.pcap** file with the default configuration file.

```bash
sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-2.pcap
```

#### What is the number of the generated alerts?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-55-11.png>)

{% hint style="success" %}
`340`
{% endhint %}

#### Keep reading the output. What is the number of the detected TCP packets?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-57-00.png>)

{% hint style="success" %}
`82`
{% endhint %}

#### Investigate the mx-2.pcap and mx-3.pcap files with the default configuration file.

```bash
sudo snort -c /etc/snort/snort.conf -A full -l . \
           --pcap-list="mx-2.pcap mx-3.pcap"
```

#### What is the number of the generated alerts?

![](<../../.gitbook/assets/Screenshot from 2022-05-09 21-59-00.png>)

{% hint style="success" %}
`1020`
{% endhint %}

## Task 9 Snort Rule Structure









































