# MySQL Enumeration Tools

### Nmap's mysql-enum script

Performs valid-user enumeration against MySQL server using a bug discovered and published by [Kingcope](http://seclists.org/fulldisclosure/2012/Dec/9) Server version 5.x are susceptible to an user enumeration attack due to different messages during login when using old authentication mechanism from versions 4.x and earlier.



### Metasploit "mysql\_sql" module

This module allows for simple SQL statements to be executed against a MySQL instance given the appropriate credentials.



### Metasploit "mysql\_schemadump" module

This module extracts the schema information from a MySQL DB server.



### Metasploit "mysql\_hashdump" module

This module extracts the usernames and encrypted password hashes from a MySQL server and stores them for later cracking.

