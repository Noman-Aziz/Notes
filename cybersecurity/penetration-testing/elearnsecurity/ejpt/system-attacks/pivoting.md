# Pivoting

### Using Metasploit

First establist a meterpreter sessions, then

1. Run autoroute command to add a route
   1. `run autoroute -s <ip> <subnet>`
2. Confirm by typing `run autoroute -p`
3. Background session
4. `route print`
5. Now use auxillary scanners to target the new ip
6. After you find an open port in new target machine, you can use `portfwd` command inside meterpreter to forward that remote port to local port and continue your enumerations inside metasploit
   1. `portfwd add -l <localport> -p <remoteport> -r <remotehost>`
   2. You can confirm by `portfwd list`

***

### Using Proxychains

First establish a meterpreter sessions, then background it

1. Add a route `route add ip/subnet <session_no>`
2. Use `socks_proxy` auxiliary module to convert the meterpreter session to serve as a socks proxy:
   * ```bash
     use auxiliary/server/socks_proxy
     set VERSION 4a
     set SRVPORT 9050
     run -j
     ```
3. Now anything we sent over port 9050 would be sent over to the network we added to the route
4. Now you can add the port in proxychains and use it.
