# DNS Enumeration

### Record Types

#### A

Contains info about ipv4 address of server

#### AAAA

Contains info about ipv6 adresses of server

#### MX

Contains info about mail servers

#### NS

Constains info about name servers

#### CNAME

Contains info about the mapping of current domain to other domains

***

### Tools

* #### Host
* #### Nslookup
* #### Dig

***

### Zone Transfer Enumeration

We can enumerate domains for zone transfer queries which in terms will dump all their server informations (**zonefile** which in used in zone transfer)

#### Using Host Tool

```bash
$ host -t ns zonetransfer.me
zonetransfer.me name server testoutput2.me
zonetransfer.me name server testoutput1.me

$ host -l zonetransfer.me testoutput1.me
/// All Details are Dumped ///
```

#### Using Dig Tool

**axfr** is a dns record which means reference to zone transfer

```bash
$ dig zonetransfer.me -t ns
;; ANSWER SECTION:
zonetransfer.me .... testoutput1.me

$ dig axfr zonetransfer.me @testoutput1.me
/// All Details are Dumped ///
```

#### Using Nslookup

```bash
$ nslookup
> set type=ns
> zonetransfer.me
/// Details ... testoutput1.me ///

$ nslookup
> server testoutput1.me
> set type=any
> ls -d zonetransfer.me
/// All Details are Dumped ///
```

#### Using DNSRecon (Automated Process)

```bash
$ dnsrecon -d zonetransfer.me -t axfr
/// All Details are Dumped ///
```

***
