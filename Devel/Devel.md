
# Devel HTB Machine

Link = https://app.hackthebox.com/machines/Devel

Devel is a Windows machine Rated Easy on HackTheBox

## Rustcan / Nmap scan

```
PORT   STATE SERVICE REASON          VERSION
21/tcp open  ftp     syn-ack ttl 127 Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  02:06AM       <DIR>          aspnet_client
| 03-17-17  05:37PM                  689 iisstart.htm
|_03-17-17  05:37PM               184946 welcome.png
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp open  http    syn-ack ttl 127 Microsoft IIS httpd 7.5
|_http-title: IIS7
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|phone|specialized
Running (JUST GUESSING): Microsoft Windows 2008|7|Vista|Phone|2012|8.1 (97%)
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_vista cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_8.1
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (97%), Microsoft Windows Server 2008 R2 or Windows 7 SP1 (92%), Microsoft Windows Vista or Windows 7 (92%), Microsoft Windows 8.1 Update 1 (92%), Microsoft Windows Phone 7.5 or 8.0 (92%), Microsoft Windows Server 2012 R2 (91%), Microsoft Windows Embedded Standard 7 (91%), Microsoft Windows Server 2008 R2 (89%), Microsoft Windows Server 2008 R2 or Windows 8.1 (89%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (89%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.95%E=4%D=9/16%OT=21%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=68C93864%P=x86_64-pc-linux-gnu)
SEQ(SP=102%GCD=1%ISR=109%TI=I%II=I%SS=S%TS=7)
SEQ(SP=FE%GCD=1%ISR=101%TI=RD%II=I%TS=7)
OPS(O1=M542NW8ST11%O2=M542NW8ST11%O3=M542NW8NNT11%O4=M542NW8ST11%O5=M542NW8ST11%O6=M542ST11)
WIN(W1=2000%W2=2000%W3=2000%W4=2000%W5=2000%W6=2000)
ECN(R=Y%DF=Y%TG=80%W=2000%O=M542NW8NNS%CC=N%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=Y%DFI=N%TG=80%CD=Z)

Uptime guess: 0.005 days (since Tue Sep 16 12:07:16 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=254 (Good luck!)
IP ID Sequence Generation: Randomized
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 21/tcp)
HOP RTT       ADDRESS
1   326.90 ms 10.10.16.1
2   492.20 ms 10.10.10.5

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 12:13
Completed NSE at 12:13, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 12:13
Completed NSE at 12:13, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 12:13
Completed NSE at 12:13, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.10 seconds
           Raw packets sent: 90 (7.644KB) | Rcvd: 42 (2.963KB)
```

Looks Like There are 2 ports open FTP (21) and HTTP (80).

## FTP 21
Looks like FTP Allows Anonymous Access.I looked Around The FTP Server nothing much just some image and html file and a directory with other directories.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/FTP.png)

## HTTP 80
Looks Like The Website is running **Microsoft IIS httpd 7.5** Probably Vulnerable to some exploit.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/http.png)

While using ffuf looks like the directory from FTP is accessible from HTTP so i'm guessing maybe i could upload a asp or aspx reverse shell on the ftp server then execute the shell from The HTTP Server.Also while using nuclei i found a vulnerability **[CVE-2015-1635] [http] [critical] http://10.10.10.5/** But first i want to test my theory

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/cve.png)

so first i made a simple file **echo "Test" > test.txt** Then logged in to the ftp server and put the files and tried Accessing it from the Website.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/put.png)
Accessing The file from the webserver.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/test_website.png)

Afterwards so i uploaded a aspx reverse shell on the ftp server and got a shell.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/shell.png)
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/dir.png)

So I went to the website **https://www.revshells.com/** generated a Powershell reverse shell and started nc then paste the powershell reverse shell on the web shell.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/reverse%20shell.png)

# PrivEsc
I made a msfvenom payload.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/msfvenom.png)

Uploaded it on The machine executed it and got a meterpreter shell.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/meterpreter.png)

I ran the **local_exploit_suggester** to find a way to Privesc and i use the **exploit/windows/local/ms10_015_kitrap0d** and got **nt authority\system** And both of the Flags.
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/local_ex.png)
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/flags.png)
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/Devel/Screenshot/2025-09-16_13-16.png)

Afterwards I checked The Walkthrough for anything a missed but mostly It was The same approach Anyway We completed The box Happy Hacking.

