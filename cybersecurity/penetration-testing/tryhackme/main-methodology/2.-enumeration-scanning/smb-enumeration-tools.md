# SMB Enumeration Tools

### Intro

SMB has two ports, 445 and 139.&#x20;

<figure><img src="../../../../../.gitbook/assets/image (42) (1).png" alt=""><figcaption></figcaption></figure>

***

### **smbmap**

is one of the best ways to enumerate samba. smbmap allows pen-testers to run commands(given proper permissions), download and upload files, and overall is just incredibly useful for smb enumeration.

***

### **smbclient**

allows you to do most of the things you can do with smbmap, and it also offers you and interactive prompt.

#### List Shares

`smbclient -L ip` It list all the samba shares on the network

***

### **impacket**

is a collection of extremely useful windows scripts. It is worth mentioning here, as it has many scripts available that use samba to enumerate and even gain shell access to windows machines. All scripts can be found ([https://github.com/SecureAuthCorp/impacket](https://github.com/SecureAuthCorp/impacket)) ; Note: impacket has scripts that use other protocols and services besides samba.

***

### **enum4linux**

Enum4linux is a tool used to enumerate SMB shares on both Windows and Linux systems. It is basically a wrapper around the tools in the Samba package and makes it easy to quickly extract information from the target pertaining to SMB. The syntax of Enum4Linux is nice and simple: `enum4linux [options] ip`

***
