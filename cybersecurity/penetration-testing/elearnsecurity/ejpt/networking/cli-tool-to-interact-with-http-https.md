# CLI Tool to interact with HTTP/HTTPS

### Http Interaction (Netcat)

You can interact with an http website using netcat

```bash
$ nc -v elearnsecurity.com 80
GET / HTTP/1.1
Host: www.elearnsecurity.com

--Response--
```

***

### Https Interaction (Openssl)

Since, netcat does not support ssl/tls, we use openssl client to interact with https enabled websites.

```bash
$ openssl s_client -connect elearnsecurity.com:443
GET / HTTP/1.1
Host: www.elearnsecurity.com

--Response--
```

Some interesting openssl flags are -quiet to disable handshake showing and -debug to see the handshake details

You can also use `OPTIONS / HTTP/1.1` to see all the available options that website accepts.

***
