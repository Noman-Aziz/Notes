# NMAP - Port Scanning

nmap will connect to each port of the target in turn. Depending on how the port responds, it can be determined as being open, closed, or filtered (usually by a firewall). Once we know which ports are open, we can then look at enumerating which services are running on each port – either manually, or more commonly using nmap.

***

### **Switches**:

* Syn Scan : -sS
* Udp Scan : -sU
* OS Scan : -O
* Service Version Scan : -sV
* Increase Verbosity : -v
* Verbosity Level 2 : -vv
* Save Output in 3 Major Formats : -oA
* Scan all Ports : -p-

***

### **Scan Types**:

#### Basic Scans

* TCP Connect Scans (-sT)
* SYN "Half-open", "Stealth" Scans (-sS)
  * if we identify closed and filtered ports, the exact same rules as with a TCP Connect scan apply.
  * If a port is closed then the server responds with a RST TCP packet. If the port is filtered by a firewall then the TCP SYN packet is either dropped, or **spoofed** with a TCP reset.
* UDP Scans (-sU)
  * If a UDP port doesn't respond to an Nmap scan, it will be marked as open | filtered
  * If a UDP port is closed, icmp "Port Unreachable" message is sent back

#### Other Scans (stealthier)

* TCP Null Scans (-sN)
  * TCP request is sent with no flags set at all.
  * The target host should respond with a RST if the port is closed according to RFC.
* TCP FIN Scans (-sF)
  * a request is sent with the FIN flag (usually used to gracefully close an active connection)
  * expects a RST if the port is closed.
* TCP Xmas Scans (-sX)
  * send a malformed TCP packet.
  * expects a RST response for closed ports.
  * flags that it sets (PSH, URG and FIN) give it the appearance of a blinking christmas tree when viewed as a packet capture in Wireshark.
* The expected response for open ports with these scans is also identical, and is very similar to that of a UDP scan
  * If the port is open then there is no response to the malformed packet.
  * If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.
  * In particular Microsoft Windows (and a lot of Cisco network devices) are known to respond with a RST to any malformed TCP packet -- regardless of whether the port is actually open or not. This results in all ports showing up as being closed.
* Many firewalls are configured to drop incoming TCP packets to blocked ports which have the SYN flag set (thus blocking new connection initiation requests).
* By sending requests which do not contain the SYN flag, we effectively bypass this kind of firewall.
* Most modern IDS solutions are savvy to these scan types, so don't rely on them to be 100% effective when dealing with modern systems.

#### ICMP Network Scanning

* we want to see which IP addresses contain active hosts, and which do not.
* ping sweep : -sn
* dont scan any ports -- forcing it to rely primarily on ICMP echo packets (or ARP requests on a local network, if run with sudo or directly as the root user) to identify targets.
* also cause nmap to send a TCP SYN packet to port 443 of the target, as well as a TCP ACK (or TCP SYN if not run as root) packet to port 80 of the target.

***

### **Scripting Engine**

* NSE Scripts are written in the Lua programming language
* do a variety of things: from scanning for vulnerabilities, to automating exploits for them.
* **Categories**
  * safe:- Won't affect the target
  * intrusive:- Not safe: likely to affect the target
  * vuln:- Scan for vulnerabilities
  * exploit:- Attempt to exploit a vulnerability
  * auth:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
  * brute:- Attempt to bruteforce credentials for running services
  * discovery:- Attempt to query running services for further information about the network (e.g. query an SNMP server).
  * [Others](https://nmap.org/book/nse-usage.html)
* Some scripts require arguments (for example, credentials, if they're exploiting an authenticated vulnerability). These can be given with the --script-args Nmap switch.
* Nmap scripts come with built-in help menus, which can be accessed using nmap --script-help "script-name"
* Nmap stores its scripts on Linux at /usr/share/nmap/scripts

#### Enumerating SMB Shares

`nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse <IP>`

#### Enumerating Remote Procedure Call (RPC) NFS Shares

Port 111 runs the service rpcbind. This is just a server that converts remote procedure call (RPC) program number into universal addresses. When an RPC service is started, it tells rpcbind the address at which it is listening and the RPC program number its prepared to serve. If port 111 is access to a network file system. Nmap command to enumerate this: `nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount <IP>`

***

### **Firewall Evasion**

* Your typical Windows host will, with its default firewall, block all ICMP packets
  * This means that Nmap will register a host with this firewall configuration as dead and not bother scanning it at all.
* \-Pn tells Nmap to not bother pinging the host before scanning it.
  * If the host really is dead then Nmap will still be checking and double checking every specified port.
* It's worth noting that if you're already directly on the local network, Nmap can also use ARP requests to determine host activity.
* Switches for [firewall evasion](https://nmap.org/book/man-bypass-firewalls-ids.html)
* The following switches are of particular note:
  * \-f:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
  * An alternative to -f, but providing more control over the size of the packets: --mtu "number", accepts a maximum transmission unit size to use for the packets sent. This must be a multiple of 8.
  * \--scan-delay "time"ms :- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
  * \--badsum :- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.
