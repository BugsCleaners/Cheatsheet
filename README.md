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

## Services  
 ### SMB
   #### Enumerating SMB
      * enum4linux [options] ip
      * use option  ```-a``` all of the above (full basic enumeration)

  #### SMB Exploit
      * smbclient //[IP]/[SHARE]
      * smbclient //10.10.10.2/sharefilename -U username -p 445
 ### Telnet
