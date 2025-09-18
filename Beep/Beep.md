
# Beep HTB Machine

Beep Is an Linux Machine Difficultly is Easy

## Nmap / Rustscan 

```
PORT      STATE SERVICE  REASON         VERSION
22/tcp    open  ssh      syn-ack ttl 63 OpenSSH 4.3 (protocol 2.0)
| ssh-hostkey: 
|   1024 ad:ee:5a:bb:69:37:fb:27:af:b8:30:72:a0:f9:6f:53 (DSA)
| ssh-dss AAAAB3NzaC1kc3MAAACBAI04jN+Sn7/9f2k+5UteAWn8KKj3FRGuF4LyeDmo/xxuHgSsdCjYuWtNS8m7stqgNH5edUu8vZ0pzF/quX5kphWg/UOz9weGeGyzde5lfb8epRlTQ2kfbP00l+kq9ztuWaXOsZQGcSR9iKE4lLRJhRCLYPaEbuxKnYz4WhAv4yD5AAAAFQDXgQ9BbvoxeDahe/ksAac2ECqflwAAAIEAiGdIue6mgTfdz/HikSp8DB6SkVh4xjpTTZE8L/HOVpTUYtFYKYj9eG0W1WYo+lGg6SveATlp3EE/7Y6BqdtJNm0RfR8kihoqSL0VzKT7myerJWmP2EavMRPjkbXw32fVBdCGjBqMgDl/QSEn2NNDu8OAyQUVBEHrE4xPGI825qgAAACANnqx2XdVmY8agjD7eFLmS+EovCIRz2+iE+5chaljGD/27OgpGcjdZNN+xm85PPFjUKJQuWmwMVTQRdza6TSp9vvQAgFh3bUtTV3dzDCuoR1D2Ybj9p/bMPnyw62jgBPxj5lVd27LTBi8IAH2fZnct7794Y3Ge+5r4Pm8Qbrpy68=
|   2048 bc:c6:73:59:13:a1:8a:4b:55:07:50:f6:65:1d:6d:0d (RSA)
|_ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA4SXumrUtyO/pcRLwmvnF25NG/ozHsxSVNRmTwEf7AYubgpAo4aUuvhZXg5iymwTcZd6vm46Y+TX39NQV/yT6ilAEtLbrj1PLjJl+UTS8HDIKl6QgIb1b3vuEjbVjDj1LTq0Puzx52Es0/86WJNRVwh4c9vN8MtYteMb/dE2Azk0SQMtpBP+4Lul4kQrNwl/qjg+lQ7XE+NU7Va22dpEjLv/TjHAKImQu2EqPsC99sePp8PP5LdNbda6KHsSrZXnK9hqpxnwattPHT19D94NHVmMHfea9gXN3NCI3NVfDHQsxhqVtR/LiZzpbKHldFU0lfZYH1aTdBfxvMLrVhasZcw==
25/tcp    open  smtp     syn-ack ttl 63 Postfix smtpd
|_smtp-commands: beep.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, ENHANCEDSTATUSCODES, 8BITMIME, DSN
80/tcp    open  http     syn-ack ttl 63 Apache httpd 2.2.3
|_http-server-header: Apache/2.2.3 (CentOS)
|_http-title: Did not follow redirect to https://10.10.10.7/
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
110/tcp   open  pop3     syn-ack ttl 63 Cyrus pop3d 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
|_pop3-capabilities: STLS RESP-CODES USER AUTH-RESP-CODE EXPIRE(NEVER) PIPELINING APOP IMPLEMENTATION(Cyrus POP3 server v2) UIDL TOP LOGIN-DELAY(0)
111/tcp   open  rpcbind  syn-ack ttl 63 2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100024  1            790/udp   status
|_  100024  1            793/tcp   status
143/tcp   open  imap     syn-ack ttl 63 Cyrus imapd 2.3.7-Invoca-RPM-2.3.7-7.el5_6.4
|_imap-capabilities: CHILDREN ID OK ACL X-NETSCAPE LITERAL+ MAILBOX-REFERRALS CONDSTORE IMAP4 NAMESPACE QUOTA ANNOTATEMORE ATOMIC LIST-SUBSCRIBED UIDPLUS IDLE IMAP4rev1 LISTEXT MULTIAPPEND CATENATE NO BINARY SORT SORT=MODSEQ THREAD=ORDEREDSUBJECT URLAUTHA0001 Completed UNSELECT RENAME STARTTLS RIGHTS=kxte THREAD=REFERENCES
443/tcp   open  ssl/http syn-ack ttl 63 Apache httpd 2.2.3 ((CentOS))
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--/emailAddress=root@localhost.localdomain/organizationalUnitName=SomeOrganizationalUnit/localityName=SomeCity
| Issuer: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--/emailAddress=root@localhost.localdomain/organizationalUnitName=SomeOrganizationalUnit/localityName=SomeCity
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2017-04-07T08:22:08
| Not valid after:  2018-04-07T08:22:08
| MD5:   621a:82b6:cf7e:1afa:5284:1c91:60c8:fbc8
| SHA-1: 800a:c6e7:065e:1198:0187:c452:0d9b:18ef:e557:a09f
| -----BEGIN CERTIFICATE-----
| MIIEDjCCA3egAwIBAgICfVUwDQYJKoZIhvcNAQEFBQAwgbsxCzAJBgNVBAYTAi0t
| MRIwEAYDVQQIEwlTb21lU3RhdGUxETAPBgNVBAcTCFNvbWVDaXR5MRkwFwYDVQQK
| ExBTb21lT3JnYW5pemF0aW9uMR8wHQYDVQQLExZTb21lT3JnYW5pemF0aW9uYWxV
| bml0MR4wHAYDVQQDExVsb2NhbGhvc3QubG9jYWxkb21haW4xKTAnBgkqhkiG9w0B
| CQEWGnJvb3RAbG9jYWxob3N0LmxvY2FsZG9tYWluMB4XDTE3MDQwNzA4MjIwOFoX
| DTE4MDQwNzA4MjIwOFowgbsxCzAJBgNVBAYTAi0tMRIwEAYDVQQIEwlTb21lU3Rh
| dGUxETAPBgNVBAcTCFNvbWVDaXR5MRkwFwYDVQQKExBTb21lT3JnYW5pemF0aW9u
| MR8wHQYDVQQLExZTb21lT3JnYW5pemF0aW9uYWxVbml0MR4wHAYDVQQDExVsb2Nh
| bGhvc3QubG9jYWxkb21haW4xKTAnBgkqhkiG9w0BCQEWGnJvb3RAbG9jYWxob3N0
| LmxvY2FsZG9tYWluMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC3e4HhLYPN
| gwJ4eKlW/UpmemPfK/a3mcafSqx/AJP34OC0Twj/cZNaqFPLOWfNjcq4mmiV++9a
| oJCkj4apDkyICI1emsrPaRdrlA/cCXcn3nupfOgcfpBV4vqNfqorEqpJCO7T4bcp
| Z6YHuxtRtP7gRJiE1ytAFP2jDvtvMqEWkwIDAQABo4IBHTCCARkwHQYDVR0OBBYE
| FL/OLJ7hJVedlL5Gk0fYvo6bZkqWMIHpBgNVHSMEgeEwgd6AFL/OLJ7hJVedlL5G
| k0fYvo6bZkqWoYHBpIG+MIG7MQswCQYDVQQGEwItLTESMBAGA1UECBMJU29tZVN0
| YXRlMREwDwYDVQQHEwhTb21lQ2l0eTEZMBcGA1UEChMQU29tZU9yZ2FuaXphdGlv
| bjEfMB0GA1UECxMWU29tZU9yZ2FuaXphdGlvbmFsVW5pdDEeMBwGA1UEAxMVbG9j
| YWxob3N0LmxvY2FsZG9tYWluMSkwJwYJKoZIhvcNAQkBFhpyb290QGxvY2FsaG9z
| dC5sb2NhbGRvbWFpboICfVUwDAYDVR0TBAUwAwEB/zANBgkqhkiG9w0BAQUFAAOB
| gQA+ah2n+bomON94KgibPEVPpmW+8N6Sq3f4qDG54urTnPD39GrYHvMwA3B2ang9
| l3zta5tXYAVj22kiNM2si4bOMQsa6FZR4AEzWCq9tZS/vTCCRaT79mWj3bUvtDkV
| 2ScJ9I/7b4/cPHDOrAKdzdKxEE2oM0cwKxSnYBJk/4aJIw==
|_-----END CERTIFICATE-----
|_http-title: Elastix - Login page
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/
|_ssl-date: 2025-09-18T08:56:24+00:00; 0s from scanner time.
|_http-server-header: Apache/2.2.3 (CentOS)
|_http-favicon: Unknown favicon MD5: 80DCC71362B27C7D0E608B0890C05E9F
793/tcp   open  status   syn-ack ttl 63 1 (RPC #100024)
993/tcp   open  ssl/imap syn-ack ttl 63 Cyrus imapd
|_imap-capabilities: CAPABILITY
995/tcp   open  pop3     syn-ack ttl 63 Cyrus pop3d
3306/tcp  open  mysql?   syn-ack ttl 63
5038/tcp  open  asterisk syn-ack ttl 63 Asterisk Call Manager 1.1
10000/tcp open  http     syn-ack ttl 63 MiniServ 1.570 (Webmin httpd)
|_http-favicon: Unknown favicon MD5: 74F7F6F633A027FA3EA36F05004C9341
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|WAP|remote management|broadband router|webcam
Running (JUST GUESSING): Linux 2.6.X|2.4.X (97%), Dell embedded (95%), D-Link embedded (95%), Raritan embedded (95%), Asus embedded (95%), AXIS embedded (95%)
OS CPE: cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:2.4.30 cpe:/o:linux:linux_kernel:2.6.21 cpe:/h:dlink:dir-300_nru cpe:/h:asus:rt-ac66u cpe:/h:asus:rt-n10 cpe:/h:axis:211_network_camera
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.18 - 2.6.24 (97%), OpenWrt White Russian 0.9 (Linux 2.4.30) (96%), Dell Chassis Management Controller (CMC) (95%), D-Link DIR-300 NRU router (Linux 2.6.21) (95%), Linux 2.6.16 - 2.6.21 (95%), Linux 2.6.18 - 2.6.27 (95%), Linux 2.6.21 (95%), Linux 2.6.26 (95%), Linux 2.6.8 - 2.6.30 (95%), Raritan Dominion KX II KVM (95%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.95%E=4%D=9/18%OT=22%CT=%CU=36057%PV=Y%DS=2%DC=T%G=N%TM=68CBCA01%P=x86_64-pc-linux-gnu)
SEQ(SP=C6%GCD=1%ISR=C4%TI=Z%CI=Z%II=I%TS=A)
SEQ(SP=CA%GCD=1%ISR=CE%TI=Z%CI=Z%II=I%TS=8)
OPS(O1=M542ST11NW7%O2=M542ST11NW7%O3=M542NNT11NW7%O4=M542ST11NW7%O5=M542ST11NW7%O6=M542ST11)
WIN(W1=16A0%W2=16A0%W3=16A0%W4=16A0%W5=16A0%W6=16A0)
ECN(R=Y%DF=Y%T=40%W=16D0%O=M542NNSNW7%CC=N%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 148.836 days (since Tue Apr 22 14:55:58 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=202 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: Hosts:  beep.localdomain, 127.0.0.1, example.com

Host script results:
|_clock-skew: 0s

TRACEROUTE (using port 143/tcp)
HOP RTT       ADDRESS
1   329.41 ms 10.10.16.1
2   167.67 ms 10.10.10.7

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:59
Completed NSE at 10:59, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:59
Completed NSE at 10:59, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:59
Completed NSE at 10:59, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 430.81 seconds
           Raw packets sent: 77 (5.080KB) | Rcvd: 49 (3.539KB)

```

The Nmap scan results show a lot of ports open , normally i skip ssh we we have no credentials and Port 80 is redirecting me to 443 And Getting a Secure Connection Failed since the certificate version is 1.0 i can curl the website like this **curl -k --tlsv1.0 https://beep.htb** but im not planning on working on curl all day so i asked chatgpt how to solve that problem.

![Alt-text](chatgpt)

After that i could access the webite.

![Alt-text](web)

The website is running Elastix so i search using searchsploit if elastix has any vulnerability found a few.

![Alt-text](search)

The last for looks interesting to me so I decided to try them i first tested the LFI vuln read it and It looks the https://beep.htb/vtigercrm/graph.php?current_language=../../../../../../../..//etc/hosts endpoint is vulnerable to lfi i couldnt access the /etc/passwd or other important files but the script is getting the config file of elastix **../../../../../../../..//etc/amportal.conf** which has a username and password

```
AMPDBUSER=asteriskuser # AMPDBPASS=amp109 AMPDBPASS=jEhdIekWmdjE AMPENGINE=asterisk AMPMGRUSER=admin #AMPMGRPASS=amp111 AMPMGRPASS=jEhdIekWmdjE
```

I tried SSH using The **asteriskuser** and using the password **jEhdIekWmdjE** but no luck then changed the user to root and got ssh

![Alt-text](root)

I got root access so i got the user and root flags

![Alt-text](flags)

![Alt-text](completed)

after wards I checked the descriptions and Walkthrough if there is anything or other ways to exploit the machine there was a CVE i think from 2012 which i tried but didnt work for me for some reason but i didnt spend much time to it so i moved on. Anyway Happy HAcking
