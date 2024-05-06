0Day - TryHackMe.com

[Link to room on TryHackMe.com](https://tryhackme.com/room/0day)

![](0day11.png)


First step as always: enumerating ports with rustcan and nmap:

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
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-06 22:02 +03
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
Scanned at 2024-05-06 22:02:26 +03 for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 60
80/tcp open  http    syn-ack ttl 60

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.05 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (116B)
```

