# Tshark

## Task 2 Reading PCAP Files

#### How many packets are in the dns.cap file?

```bash
tshark -r dns.cap | wc -l
```

{% hint style="success" %}
`38`
{% endhint %}

#### How many A records are in the capture?

```bash
tshark -r dns.cap -Y 'dns.qry.type == 1' | wc -l
```

{% hint style="success" %}
`6`
{% endhint %}

#### Which A record was present the most?

```bash
tshark -r dns.cap -Y 'dns.qry.type == 1' -T fields -e dns.qry.name | uniq -c
```

{% hint style="success" %}
`GRIMM.utelsystems.local`
{% endhint %}

## Task 3 DNS Exfil

#### How many packets are in this capture?

```bash
tshark -r dnsexfil.pcap | wc -l
```

{% hint style="success" %}
`125`
{% endhint %}

#### How many DNS queries are in this pcap?

```bash
tshark -r dnsexfil.pcap -Y 'dns.flags.response == 0' | wc -l
```

#### What is the DNS transaction ID of the suspicious queries?

```bash
tshark -r dnsexfil.pcap -Y 'dns.flags.response == 0' -T fields -e dns.id | sort -u
```

{% hint style="success" %}
`0xbeef`
{% endhint %}

#### What is the string extracted from the DNS queries?

```bash
tshark -r dnsexfil.pcap -Y 'dns.flags.response == 0' -T fields -e dns.qry.name \
| cut -c 1 | tr -d '\n'
```

{% hint style="success" %}
`MZWGCZ33ORUDC427NFZV65BQOVTWQX3XNF2GQMDVG5PXI43IGRZGWIL5`
{% endhint %}

#### What is the flag?

```bash
echo -n 'MZWGCZ33ORUDC427NFZV65BQOVTWQX3XNF2GQMDVG5PXI43IGRZGWIL5' | base32 -d
```

{% hint style="success" %}
`flag{th1s_is_t0ugh_with0u7_tsh4rk!}`
{% endhint %}
