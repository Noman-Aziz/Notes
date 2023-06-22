# Packet Manipulation

### Scapy

We can use this framework to Send Custom Packets, Sniff Traffic and DOS Attack etc.

According to documentation, "Scapy is a powerful interactive packet manipulation program. It is able to forge or decode packets of a wide number of protocols, send them on the wire, capture them, match requests and replies, and much more. It can easily handle most classical tasks like scanning, tracerouting, probing, unit tests, attacks or network discovery (it can replace hping, 85% of nmap, arpspoof, arp-sk, arping, tcpdump, tethereal, p0f, etc.). It also performs very well at a lot of other specific tasks that most other tools can’t handle, like sending invalid frames, injecting your own 802.11 frames, combining technics (VLAN hopping+ARP cache poisoning, VOIP decoding on WEP encrypted channel."

#### Send Packet

```bash
send(IP(src="x.x.x.x",dst="y.y.y.y")/ICMP()/"Hello World")
```

#### DOS Attack

```bash
send(IP(src="x.x.x.x",dst="y.y.y.y")/TCP(sport="x",dport="y"), count=n)
```

***
