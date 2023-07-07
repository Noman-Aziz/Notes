# Mapping Networks

Ping Sweeping to check which hosts are alive in network or not.



### Fping

`fping -a -g IPRANGE`

* `-a` used to check for alive hosts
* `-g` to perform ping sweep instead of normal ping



### Nmap

`nmap -sn -iL hostlists.txt`

* `-iL` to read hosts from file

