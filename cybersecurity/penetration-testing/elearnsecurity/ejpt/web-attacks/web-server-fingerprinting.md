# Web Server Fingerprinting

### Banner Grabbing

To grab banner, you just have to connect to a listening daemon and then read the banner it send back to your client

#### With Netcat

```bash
$ nc targetip port
HEAD / HTTP/1.0
// Two Empty
// Lines
SERVER RESPONSE
```

***

### Fingerprinting with Httprint

It is a fingerprinting tool which uses **signature based techniques** to identify web servers.

```bash
httprint -P0 -h <target hosts> -s <signature file>
```

* P0 to avoid pinging hosts
