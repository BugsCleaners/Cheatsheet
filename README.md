# Cheatsheet

### Common 
* wget http://127.0.0.1:8000/file
* python3 -m http.server
* systemctl stop myservice

  ### Nmap

## SMB 
 ### Enumerating SMB
  * ```enum4linux [options] ip```
  * -a all of the above (full basic enumeration)

  ### SMB Exploit
  * smbclient //[IP]/[SHARE]
  * smbclient //10.10.10.2/sharefilename -U username -p 445
