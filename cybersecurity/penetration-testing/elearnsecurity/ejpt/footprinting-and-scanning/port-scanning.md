# Port Scanning

### Open Port Behaviour

Syn -> Syn + Ack -> Ack

***

### Closed Port Behaviour

Syn -> Rst + Ack

***

### Nmap Version Scan (-sV) Behaviour

Syn -> SYN + Ack -> Ack -> Banner -> Rst + Ack

***

### Tcpwrapped Port Status

It means that TCP Handshake was completed but remote host closed the connection without receiving any data. It could be an indicator for **FIREWALL**.

***

### Get Reason for Open or Closed Ports

Use nmap `--reason` switch to show explanation. We may learn from it that remote host sent an `RST` packet during TCP Handshake which probably means firewall prevented the handshake.

***

### Masscan

Useful for large networks to fastly map the network. `masscan -p22,80,443,445,53,8080 -Pn --rate=800 --banners 192.168.18.0/24 -e tap0 --router-ip 192.168.18.1 --echo > masscan.conf`

* rate means 800 packets per second
* banners used to fingerprint services
* `-e` tells which network interface to use
* `-echo` file generates a template to use for scan
  * Can be used with `-c` switch

***
