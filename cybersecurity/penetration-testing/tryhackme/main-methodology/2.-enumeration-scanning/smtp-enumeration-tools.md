# SMTP Enumeration Tools

### Enumerating Server Details

Poorly configured or vulnerable mail servers can often provide an initial foothold into a network, but prior to launching an attack, we want to fingerprint the server to make our targeting as precise as possible. We're going to use the "**smtp\_version**" module in MetaSploit to do this. As its name implies, it will scan a range of IP addresses and determine the version of any mail servers it encounters.

***

### Enumerating Users from SMTP

The SMTP service has two internal commands that allow the enumeration of users:

1. **VRFY** (confirming the names of valid users)
2. **EXPN** (which reveals the actual address of user’s aliases and lists of e-mail (mailing lists)

Using these SMTP commands, we can reveal a list of valid users. We can do this manually, over a telnet connection or metasploit module called "**smtp\_enum**". Using the module is a simple matter of feeding it a host or range of hosts to scan and a wordlist containing usernames to enumerate.

***

### smtp-user-enum

It is a non-metasploit tool work even better for enumerating OS-level user accounts on Solaris via the SMTP service. Enumeration is performed by inspecting the responses to VRFY, EXPN, and RCPT TO commands. It's an alternative that's worth keeping in mind if you're trying to distance yourself from using Metasploit e.g. in preparation for OSCP.

***
