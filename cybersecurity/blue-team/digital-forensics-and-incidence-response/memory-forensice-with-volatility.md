# Memory Forensice with Volatility

### Introduction

* It is open source memory forensics framework and is written in python and is multi platform compatible
* We can use it to analyze and extract important information from a memory dump
* It will help us analyze identify
  * Running processes
  * Files
  * Users information
  * hashes
  * etc
* It has 2 versions i.e volatility2 and volatility3
  * volatility2 is written in python2
    * It has large number of plugins written by community
  * volatility3 is written in python3
* It does not support memory acquisition ability

***

### Usage

`volatility -f <dump-file> <plugin-name>`

***

### Plugins

`volatility --info` can be used to display all plugins and their info.

1. `imageinfo` : Tells us about OS of the mem dump
2. `pslist` : list running processes
3. `pstree` : also list hidden processes (childs etc)
4. `cmdline -p <process_id>` : display command used to execute the process, accepts process id as parameter which can be get from previous plugin i.e pstree
5. `consoles` : extract command history by scanning for console information
6. `filescan` : scan for files present, display their permissions and location, can be used with grep to fetch information for specific file
7. `dumpfiles -Q <offset_of_file> -D <where_to_extract>` : used to dump a file based on its offset (extracted from previous plugin i.e filescan)
8. `hashdump` : used to dump the account hashes which can be cracked
9. `envvars` : used to dump all environmental variables
10. `dumpregistry -D <where_to_dump>` : used to dump the registry.
