# SSH Reverse Tunnels

### Introduction

Reverse SSH port forwarding specifies that the given port on the remote server host is to be forwarded to the given host and port on the local side.



### Local Tunnel vs Remote Tunnel

#### Local Tunnel

\-L is a local tunnel **(YOU <-- CLIENT)**.

If a site was blocked, you can forward the traffic to a server you own and view it.

For example, if a remote machine port say 10000 is blocked via a firewall rule from the outside but accessible internally. However, Using an SSH Tunnel we can expose the port to us (locally)!

```bash
ssh -L 10000:localhost:1000 <username>@<ip>
```

And then we can access `http://localhost:1000` to view the content.

#### Remote Tunnel

\-R is a remote tunnel (YOU --> CLIENT). You forward your traffic to the other server for others to view.

