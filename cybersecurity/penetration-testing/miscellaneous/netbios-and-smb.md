# NetBIOS & SMB

### Netbios

Stands for Nework Basic Input & Output System. It uses port **137**. It facilitates communicated bw computers in local network. Service most likely used in windows os.

It can give us information about network shares and which group that computer belongs to.

***

### Tools for Enumeration

#### Powershell (nbtstat)

```bash
nbtstat -A x.x.x.x
```

#### Kali (nbtscan)

```bash
nbtscan -v -r x.x.x.x
```

***

### SMB

Stands for Server Message Block protocol. Runs on port **139** (if running over netbios service) and port **445** (if it is running over tcp).

***
