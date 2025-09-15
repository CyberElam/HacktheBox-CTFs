
# Help CTF Machine HTB

**Help** is a Linux Machine rated **Easy** on HackTheBox , So we will start with an Nmap scan whatever Tool you want to use like nmap,rustscan etc.

## Rustscan / Nmap Scan

**sudo rustscan -a 10.10.10.121 -r 1-65535 --ulimit 5000 -A**

```
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e5:bb:4d:9c:de:af:6b:bf:ba:8c:22:7a:d8:d7:43:28 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCZY4jlvWqpdi8bJPUnSkjWmz92KRwr2G6xCttorHM8Rq2eCEAe1ALqpgU44L3potYUZvaJuEIsBVUSPlsKv+ds8nS7Mva9e9ztlad/fzBlyBpkiYxty+peoIzn4lUNSadPLtYH6khzN2PwEJYtM/b6BLlAAY5mDsSF0Cz3wsPbnu87fNdd7WO0PKsqRtHpokjkJ22uYJoDSAM06D7uBuegMK/sWTVtrsDakb1Tb6H8+D0y6ZQoE7XyHSqD0OABV3ON39GzLBOnob4Gq8aegKBMa3hT/Xx9Iac6t5neiIABnG4UP03gm207oGIFHvlElGUR809Q9qCJ0nZsup4bNqa/
|   256 d5:b0:10:50:74:86:a3:9f:c5:53:6f:3b:4a:24:61:19 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBHINVMyTivG0LmhaVZxiIESQuWxvN2jt87kYiuPY2jyaPBD4DEt8e/1kN/4GMWj1b3FE7e8nxCL4PF/lR9XjEis=
|   256 e2:1b:88:d3:76:21:d4:1e:38:15:4a:81:11:b7:99:07 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHxDPln3rCQj04xFAKyecXJaANrW3MBZJmbhtL4SuDYX
80/tcp   open  http    syn-ack ttl 63 Apache httpd 2.4.18
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Did not follow redirect to **http://help.htb/**
|_http-server-header: Apache/2.4.18 (Ubuntu)
3000/tcp open  http    syn-ack ttl 63 Node.js Express framework
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Site doesn't have a title (application/json; charset=utf-8).
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.19, Linux 5.0 - 5.14
TCP/IP fingerprint:
OS:SCAN(V=7.95%E=4%D=9/15%OT=22%CT=%CU=39279%PV=Y%DS=2%DC=T%G=N%TM=68C7CEDC
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=101%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)OPS(
OS:O1=M542ST11NW7%O2=M542ST11NW7%O3=M542NNT11NW7%O4=M542ST11NW7%O5=M542ST11
OS:NW7%O6=M542ST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(
OS:R=Y%DF=Y%T=40%W=FAF0%O=M542NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=
OS:R%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%R
OS:UD=G)IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 47.688 days (since Tue Jul 29 18:00:29 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=257 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: Host: 127.0.1.1; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   420.73 ms 10.10.16.1
2   217.78 ms 10.10.10.121

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:31
Completed NSE at 10:31, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:31
Completed NSE at 10:31, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:31
Completed NSE at 10:31, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 35.03 seconds
           Raw packets sent: 42 (2.682KB) | Rcvd: 20 (1.538KB)
```

So we Basically Have 3 ports open **SSH(22),HTTP(80) running Apache 2.4.18, and HTTP(3000) Running some Node.js Express framework** There is nothing we can do with SSH for now i normally skip it ,We will focus on The other 2 ports,Port 80 seems to be redirecting me to **http://help.htb** so put the help.htb to the **/etc/hosts** file if your using linux or just google The hosts file for windows.

### Port 80 HTTP
The web server shows The Default Apache Web Page  and wappalyzer shows Its running PHP , also viewed the source code nothing interesting.
![Alt-text](apache)

Used **ffuf** to brute force for files or directories i could find.
**ffuf -u http://help.htb/FUZZ -w <PATH>**
![Alt-text](ffuf)

Found **/javascript and /support** support looks more interesting so i checked it and it showed The **Help Desk Software by HelpDeskZ** since I open Caido Proxy I looked around and also used ffuf to fuzz for directoris and files,while fuzzing i found a readme file that has information about the version of helpDeskZ
![Alt-text](helpversion)

so i Google **helpdeskz Version: 1.0.2 exploit** Found a Github exploit for a File Upload Vulnerability read the python code a little to try and Understand what It is doing, and Found another CVE SQLi vuln but requires Authentication so skipped it , Github exploit by **JubJubMcGrub** https://github.com/JubJubMcGrub/HelpDeskZ-1.0.2-File-Uplaod.**So from my understanding The HelpdeskZ software allows php files to be uploaded on the Submit Ticket tab http://help.htb/support/?v=submit_ticket when you upload a php file it would say the file aint allow but it's uploaded then the github script executes the scripts Im guessing I could just execute it manually but anyway .
- Step 1 downloaded a php reverse shell
- Step 2 uploaded it here http://help.htb/support/?v=submit_ticket
- Step 3 used the script **python2 helpdeskz.py http://help.htb/support/uploads/tickets/ php-reverse-shell.php** then got a shell.

Dont forget to change the IP address on The php reverse shell then use nc to receive the connection

![Alt-text](shell)
Got The User.txt 

#PrivEsc

For PrivEsc i tried some manual aproach i didnt want to start with linpeas or stuff like that i explored the file system a little the check what priviledges I have I think i could read logs.
![Alt-text](helppriv)

so i checked if the kernel version has any exploit normally i would save that for the last but i saw it has some exploit https://www.exploit-db.com/exploits/44298 so i downloaded the exploit to the machine then used gcc to compile it then executed it and got root.
![Alt-text](root)

After Im done with a machine I normally look at the Machine Info to see anything i missed or other ways to exploit the machine looks like we could have used the port 3000 for SQLi and get ssh creds

![Alt-text](help)

Well box completed Happy Hacking.


