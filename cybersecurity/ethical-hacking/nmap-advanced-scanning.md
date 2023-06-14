# Nmap Advanced Scanning

### Inverse Scans

It does not work on windows since windows tcp/ip stack does not know how to respond to inverse scans therefore showing all ports closed. It is a really stealthy scan used in linux machines.

* If we receive no response this means port is open
* If we receive RST or ACK, it means port is closed

#### 1. XMAS Scan

It is an inverse TCP scan. It has **urge, push and fin** bits on.

#### 2. FIN Scan

#### 3. Null Scan

***

### Reason Flag

`--reason` tells us the reason why the port is marked as open/filtered/closed.

***

### Firewall Detection

#### ACK Probing

We send a request with ACK flag set. It works on any OS.

* if we do not get a response from the target, it means that there is a firewall in place.
* If we do get a RST response, it means that there is no firewall present and traffic is unfiltered

***

### Firewall Evasion (Deprecated)

#### Decoy

Spoof sender ip

```
$ nmap -sV -F -D ip target
$ nmap -sV -F -D RND:n target
```

RND mean use random generated Ips

#### Packet Fragmentation

Split packet in smaller packets

```
$ nmap -sV -F -f target // 4 bytes //
$ nmap -sV -F -f --send-eth target // 8 bytes //
```

#### Minimum Transmission Unit

```
$ nmap -sV -F --mtu 16 --send-eth // 16 bytes //
```

***

### Scan, Timing and Performance (IDS Evasion)

#### Timing Templates

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* Used to run scans slowest (T0) to fastest (T5)
* T1 used in evading IDS
* T3 is default timing template
* T4 used normally for speedup

#### Parallelism

* Nmap will by default setup min amount of parallel tasks to speed or slow down scans
* `--min-parallelism` flag is used
* higher means speed up scan
* lower means slow down scan
* Increasing speed will most likely make results unreliable
* `--max-parallelism` flag can also be used

#### Host Group Sizes

* Specify how many hosts you want to scan simultaneously
* Used in Class C or Class C subnets
* `nmap -sS -F --min-hostgroup 30 192.168.1.1/24`
* Higher means fast and unreliable
* `--max-hostgroup` is also used

#### Host Timeout

* Used to specify time to elapse when scanning a host when it not responds
* Allows to specify timeout period
* `nmap -Pn -p- 192.168.1-255.1-255 --host-timeout 30s`

#### Scan Delay

* Similar to host timeout
* Used to specify time which nmap waits before sending each probe
* `--scan-delay 5s`

#### Packet Rate

* Allows to specify min and max amount of packets to send per second
* `--min-rate 20`
* `--max-rate 2`

***
