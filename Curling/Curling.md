# Curling HTB Machine

https://app.hackthebox.com/machines/Curling

## Rustscan & Nmap scan

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_17-02.png)

Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-13 17:04 SAST
Stats: 0:00:16 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 98.61% done; ETC: 17:04 (0:00:00 remaining)
Nmap scan report for 10.10.10.150
Host is up (0.39s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8a:d1:69:b4:90:20:3e:a7:b6:54:01:eb:68:30:3a:ca (RSA)
|   256 9f:0b:c2:b2:0b:ad:8f:a1:4e:0b:f6:33:79:ef:fb:43 (ECDSA)
|_  256 c1:2a:35:44:30:0c:5b:56:6a:3f:a5:cc:64:66:d9:a9 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: Joomla! - Open Source Content Management
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Home
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.19, Linux 5.0 - 5.14
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using proto 1/icmp)
HOP RTT       ADDRESS
1   425.21 ms 10.10.16.1
2   214.25 ms 10.10.10.150

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.04 seconds

### Port 80 (Website)

I started The Proxy Caido to run while i explore the website ,The nmap scan Its running Joomla CMS 

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_17-08.png)

ran ffuf 

![alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_17-11.png)

also ran nuclei to get some easy wins and found a few vulnerabilities.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_17-19.png)

while reading at the blogs found a username **Floris** in case we need to brute force later.Since The website is running Joomla I Downloaded Joomscan to scan for vulnerabilities I could find on The Website.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/Joomla%20Screenshot.png)

found the version Joomla 3.8.8 so googled If It has any Vulnerabilities and Mostly It showed Up to Be Vulnerable to XSS and LFI,So Read more about those vulns.
According to its self-reported version number, the detected Joomla! application is affected by multiple vulnerabilities :
- Local file inclusion with PHP 5.3 affects Joomla 2.5.0 through 3.8.8
- XSS vulnerability in language switcher module affects Joomla 1.6.0 through 3.8.8

Those took me no where so while the tools were running i look at the source code of the website found a comment on the page of **secret.txt**

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/secret.png)

on that secret.txt there is this base64 string "Q3VybGluZzIwMTgh" so i just decoded it **echo "Q3VybGluZzIwMTgh" | base64 -d** and got This **Curling2018!** so im guessing its a password either for the Admin user or Floris.The creds work for Floris on The Admin Page **Floris:Curling2018!** .I went to the Templates and Tried to Replace the Beez3 template error.php file with a PHP reverse shell 

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/Revshell.png)

And Went to the path of the error.php (http://10.10.10.150/templates/beez3/error.php) and got a reverse shell.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/shell.png)

On Floris's Home Directory found a **password_backup** that looks like its some hexdump so i used **xxd** and **Cyberchef** to get the Password And got Floris's SSH Creds.**Floris:5d<wdCbdZu)|hChXll** After logging in to SSH I got The user flag.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_18-05.png)
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_18-07.png)

## PrivEsc
For PrivEsc First I tried Checking the Configuration file **/var/www/html/configuration.php** for credentials i could use.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/config.png)

I tried switching to root with those creds no luck so i continue with the manual enumeration,after a while i downloaded Linpeas and Pspy64 and ran them on the target machine.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/Lin.png)
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_18-22.png)

After a while i saw something was being curlled so i looked at it and it was just curling at the local host **http://127.0.0.1** so i tried changing the protocol to file and just read the root.txt **file:///root/root.txt** 

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/curl.png)
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Curling/Screenshots/2025-09-13_18-46.png)

Got the root flag You Can also get the shadow and Passwd files and Try tracking the hashes.




