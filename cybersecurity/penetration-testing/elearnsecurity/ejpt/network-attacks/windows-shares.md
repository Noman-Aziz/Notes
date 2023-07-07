# Windows Shares

### Netbios

Network Basic Input Output System. It can supply name for

* Hostname
* NetBIOS name
* Domain
* Network Shares

#### Features

It uses 3 ports

1. TCP 139
   1. Used to transmit data
2. Udp Port 138
   1. Used for NetBIOS Datagrams
   2. Datagrams are used to list shares and the machines
3. Udp Port 137
   1. Used for NetBIOS Names
   2. Names are used to find workgroups



### UNC Paths

UNC stands for Universal Naming Convention Paths. An authorized user can access shares by using UNC. Its format is

```
\\ServerName\ShareName\File.dat
```



### Administrative Shares

They are used by system admins and windows itself

1. `\\ComputerName\C$`
   1. Lets an admin access a volume on the machine.
   2. Every volume has a share e.g 'D$, E$ etc'
2. `\\ComputerName\admin$`
   1. Points to windows install directory
3. `\\ComputerName\ipc$`
   1. Used for inter process communication
   2. It can not be browsed via windows explorer

