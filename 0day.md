[Link to room on TryHackMe.com](https://tryhackme.com/room/0day)

![](0day11.png)


First step : enumerating ports with rustcan and nmap:

```
┌─[✗]─[root@parrot]─[/home/parrot]
└──╼ #rustscan -a 10.10.105.222
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
RustScan: Making sure 'closed' isn't just a state of mind.

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.105.222:22
Open 10.10.105.222:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2023-05-06 22:02 +03
Initiating Ping Scan at 22:02
Scanning 10.10.105.222 [4 ports]
Completed Ping Scan at 22:02, 0.45s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:02
Completed Parallel DNS resolution of 1 host. at 22:02, 1.03s elapsed
DNS resolution of 1 IPs took 1.03s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 22:02
Scanning 10.10.105.222 [2 ports]
Discovered open port 22/tcp on 10.10.105.222
Discovered open port 80/tcp on 10.10.105.222
Completed SYN Stealth Scan at 22:02, 0.48s elapsed (2 total ports)
Nmap scan report for 10.10.105.222
Host is up, received echo-reply ttl 60 (0.42s latency).
Scanned at 2023-05-06 22:02:26 +03 for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 60
80/tcp open  http    syn-ack ttl 60

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.05 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (116B)
```
```
┌─[✗]─[root@parrot]─[/home/parrot]
└──╼ #nmap -p- -sC -sV 10.10.105.222       
Starting Nmap 7.80 ( https://nmap.org ) at 2023-10-22 07:47 CEST
Nmap scan report for 10.10.105.222
Host is up (0.047s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 57:20:82:3c:62:aa:8f:42:23:c0:b8:93:99:6f:49:9c (DSA)
|   2048 4c:40:db:32:64:0d:11:0c:ef:4f:b8:5b:73:9b:c7:6b (RSA)
|   256 f7:6f:78:d5:83:52:a6:4d:da:21:3c:55:47:b7:2d:6d (ECDSA)
|_  256 a5:b4:f0:84:b6:a7:8d:eb:0a:9d:3e:74:37:33:65:16 (ED25519)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: 0day
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.16 seconds
```
after this results we see there is only two ports are open. İf we search exploit for this versions of services we cant find something useful. so we continue to enumaration for port 80 with gobuster:

```
┌─[root@parrot]─[/home/parrot]
└──╼ #gobuster dir -u http://10.10.105.222/ -w common.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.105.222
[+] Threads:        10
[+] Wordlist:       common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2023/10/21 19:55:44 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htaccess (Status: 403)
/.htpasswd (Status: 403)
/admin (Status: 301)
/backup (Status: 301)
/cgi-bin/ (Status: 403)
/cgi-bin (Status: 301)
/css (Status: 301)
/img (Status: 301)
/index.html (Status: 200)
/js (Status: 301)
/robots.txt (Status: 200)
/secret (Status: 301)
/server-status (Status: 403)
/uploads (Status: 301)
```


