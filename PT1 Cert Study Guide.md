# TryHackMe PT1 Certification Study Guide

Your notes are comprehensive and well-organized. Below is a structured study guide aligned with the PT1 exam domains, incorporating your existing material with command reference tables and a phased penetration testing methodology.

## Exam Structure Overview

| Section              | Weight | Focus Areas                                                                |
| -------------------- | ------ | -------------------------------------------------------------------------- |
| **Web Application**  | ~40%   | OWASP Top 10, Burp Suite, authentication flaws, file inclusion, injection  |
| **Network**          | ~36%   | Service enumeration, protocol exploitation, pivoting, password attacks     |
| **Active Directory** | ~24%   | Kerberos attacks, LDAP enumeration, lateral movement, privilege escalation |
| **Reporting**        | Graded | Professional documentation, CVSS scoring, remediation recommendations      |

## Phase 1: Reconnaissance

### Passive Reconnaissance

|Tool/Technique|Purpose|Example|
|---|---|---|
|`whois`|Domain registration info|`whois example.com`|
|`nslookup`|DNS record lookup|`nslookup -type=any example.com`|
|`dig`|Advanced DNS queries|`dig example.com MX +short`|
|DNSDumpster|Subdomain discovery|Web-based|
|Shodan|Internet-connected device search|`shodan search hostname:example.com`|
|theHarvester|Email/subdomain enumeration|`theHarvester -d example.com -b google`|
|Google Dorking|Indexed sensitive data|`site:example.com filetype:pdf`|

### Active Reconnaissance

|Tool|Purpose|Example|
|---|---|---|
|`ping`|Host availability (ICMP)|`ping -c 4 10.10.10.10`|
|`traceroute`|Network path mapping|`traceroute 10.10.10.10`|
|`netcat`|Banner grabbing|`nc -nv 10.10.10.10 80`|

## Phase 2: Scanning & Enumeration

### Nmap Command Reference

|Flag|Purpose|Example|
|---|---|---|
|`-sn`|Host discovery only (no port scan)|`nmap -sn 192.168.1.0/24`|
|`-sT`|TCP connect scan|`nmap -sT 10.10.10.10`|
|`-sS`|SYN stealth scan|`sudo nmap -sS 10.10.10.10`|
|`-sU`|UDP scan|`sudo nmap -sU 10.10.10.10`|
|`-sV`|Service version detection|`nmap -sV 10.10.10.10`|
|`-O`|OS detection|`sudo nmap -O 10.10.10.10`|
|`-A`|Aggressive (OS + version + scripts + traceroute)|`nmap -A 10.10.10.10`|
|`-p`|Specify ports|`nmap -p 22,80,443 10.10.10.10`|
|`-p-`|All 65535 ports|`nmap -p- 10.10.10.10`|
|`-F`|Fast (top 100 ports)|`nmap -F 10.10.10.10`|
|`--script`|NSE scripts|`nmap --script vuln 10.10.10.10`|
|`-oN`|Normal output|`nmap -oN scan.txt 10.10.10.10`|
|`-oX`|XML output|`nmap -oX scan.xml 10.10.10.10`|
|`-oG`|Grepable output|`nmap -oG scan.gnmap 10.10.10.10`|
|`-T<0-5>`|Timing template|`nmap -T4 10.10.10.10`|
|`-Pn`|Skip host discovery|`nmap -Pn 10.10.10.10`|

### Common Port Reference

|Port|Service|Protocol|
|---|---|---|
|21|FTP|TCP|
|22|SSH|TCP|
|23|Telnet|TCP|
|25|SMTP|TCP|
|53|DNS|TCP/UDP|
|80|HTTP|TCP|
|88|Kerberos|TCP|
|110|POP3|TCP|
|135|MSRPC|TCP|
|139|NetBIOS|TCP|
|143|IMAP|TCP|
|389|LDAP|TCP|
|443|HTTPS|TCP|
|445|SMB|TCP|
|636|LDAPS|TCP|
|1433|MSSQL|TCP|
|3306|MySQL|TCP|
|3389|RDP|TCP|
|5985|WinRM (HTTP)|TCP|
|5986|WinRM (HTTPS)|TCP|

## Phase 3: Web Application Testing

### Directory & Content Discovery

#### Gobuster Command Reference

|Flag|Purpose|Example|
|---|---|---|
|`dir`|Directory/file enumeration|`gobuster dir -u http://target -w wordlist.txt`|
|`dns`|Subdomain enumeration|`gobuster dns -d example.com -w subdomains.txt`|
|`vhost`|Virtual host discovery|`gobuster vhost -u http://target -w vhosts.txt`|
|`-w`|Wordlist|`-w /usr/share/wordlists/dirb/common.txt`|
|`-x`|File extensions|`-x php,html,txt,bak`|
|`-t`|Threads|`-t 50`|
|`-o`|Output file|`-o results.txt`|
|`-k`|Skip TLS verification|`-k`|
|`-b`|Exclude status codes|`-b 404,403`|
|`-s`|Include status codes|`-s 200,301`|

#### ffuf Command Reference

|Flag|Purpose|Example|
|---|---|---|
|`-u`|Target URL with FUZZ keyword|`-u http://target/FUZZ`|
|`-w`|Wordlist|`-w /usr/share/seclists/Discovery/Web-Content/common.txt`|
|`-H`|Custom header|`-H "Host: FUZZ.target.com"`|
|`-X`|HTTP method|`-X POST`|
|`-d`|POST data|`-d "user=admin&pass=FUZZ"`|
|`-mc`|Match status codes|`-mc 200,301`|
|`-fc`|Filter status codes|`-fc 404`|
|`-fs`|Filter by size|`-fs 4242`|
|`-fw`|Filter by word count|`-fw 100`|
|`-t`|Threads|`-t 100`|
|`-rate`|Requests per second|`-rate 50`|
|`-o`|Output file|`-o results.json`|
|`-of`|Output format|`-of json`|
|`-e`|Extensions|`-e .php,.html`|
|`-recursion`|Recursive scanning|`-recursion -recursion-depth 2`|

### Burp Suite Workflow

```
1. Configure browser proxy → 127.0.0.1:8080
2. Intercept requests → Analyze parameters
3. Send to Repeater → Manual testing
4. Send to Intruder → Automated fuzzing
5. Review results → Document findings
```

#### Intruder Attack Types

|Type|Use Case|
|---|---|
|**Sniper**|Single payload position, one-at-a-time|
|**Battering Ram**|Same payload in all positions simultaneously|
|**Pitchfork**|Multiple payloads, synchronized (1:1 mapping)|
|**Cluster Bomb**|Multiple payloads, all combinations|

### OWASP Top 10 Testing Checklist

|Vulnerability|Test Method|Tools|
|---|---|---|
|**Broken Access Control**|IDOR testing, privilege escalation|Burp, manual|
|**Cryptographic Failures**|Check for HTTP, weak ciphers|Nmap scripts, SSLScan|
|**Injection (SQL/Command)**|Input validation testing|SQLMap, Burp, manual|
|**Insecure Design**|Business logic flaws|Manual analysis|
|**Security Misconfiguration**|Default creds, exposed services|Nmap, Nikto|
|**Vulnerable Components**|Version detection|Nmap -sV, searchsploit|
|**Authentication Failures**|Credential stuffing, session testing|Hydra, Burp|
|**Integrity Failures**|Deserialization, unsigned updates|Manual|
|**Logging Failures**|Error handling, verbose errors|Manual|
|**SSRF**|Internal resource access|Burp, manual|

### SQLMap Command Reference

|Flag|Purpose|Example|
|---|---|---|
|`-u`|Target URL with parameter|`-u "http://target/page?id=1"`|
|`-r`|Request file (from Burp)|`-r request.txt`|
|`--dbs`|Enumerate databases|`--dbs`|
|`-D`|Specify database|`-D dbname`|
|`--tables`|Enumerate tables|`--tables`|
|`-T`|Specify table|`-T users`|
|`--columns`|Enumerate columns|`--columns`|
|`--dump`|Dump table data|`--dump`|
|`--os-shell`|OS command shell|`--os-shell`|
|`--level`|Test level (1-5)|`--level 3`|
|`--risk`|Risk level (1-3)|`--risk 2`|
|`--batch`|Non-interactive|`--batch`|
|`--wizard`|Guided mode|`--wizard`|

## Phase 4: Network Exploitation

### SMB Enumeration & Exploitation

|Tool/Command|Purpose|
|---|---|
|`smbclient -L //target -N`|List shares (null session)|
|`smbclient //target/share -U user`|Connect to share|
|`smbmap -H target`|Enumerate share permissions|
|`enum4linux -a target`|Full SMB enumeration|
|`crackmapexec smb target -u user -p pass`|Credential validation|
|`crackmapexec smb target -u user -p pass --shares`|List shares with creds|

### Password Attacks

#### Hydra Command Reference

|Flag|Purpose|Example|
|---|---|---|
|`-l`|Single username|`-l admin`|
|`-L`|Username list|`-L users.txt`|
|`-p`|Single password|`-p password123`|
|`-P`|Password list|`-P rockyou.txt`|
|`-t`|Parallel tasks|`-t 16`|
|`-f`|Stop on first success|`-f`|
|`-V`|Verbose|`-V`|
|`-s`|Custom port|`-s 2222`|

**Protocol Examples:**

```bash
# SSH
hydra -l admin -P passwords.txt ssh://10.10.10.10
# FTP
hydra -L users.txt -P passwords.txt ftp://10.10.10.10
# HTTP POST Form
hydra -l admin -P passwords.txt 10.10.10.10 http-post-form "/login:user=^USER^&pass=^PASS^:F=incorrect"
# SMB
hydra -L users.txt -P passwords.txt smb://10.10.10.10
# RDP
hydra -l admin -P passwords.txt rdp://10.10.10.10
```

## Phase 5: Active Directory Attacks

### AD Enumeration Workflow

```
1. Identify Domain Controller (port 88, 389, 445)
2. Enumerate users/groups (LDAP, RPC)
3. Identify SPNs (Kerberoasting targets)
4. Check for AS-REP roastable accounts
5. Map trust relationships
6. Run BloodHound for attack paths
```

### Key AD Ports

|Port|Service|Attack Relevance|
|---|---|---|
|88|Kerberos|Kerberoasting, AS-REP roasting|
|389|LDAP|User/group enumeration|
|636|LDAPS|Encrypted LDAP|
|445|SMB|Pass-the-Hash, relay attacks|
|135|RPC|User enumeration|
|5985|WinRM|Remote command execution|

### Attack Techniques

| Attack              | Requirement          | Tool                                |
| ------------------- | -------------------- | ----------------------------------- |
| **Kerberoasting**   | Valid domain creds   | Impacket `GetUserSPNs.py`, Rubeus   |
| **AS-REP Roasting** | No pre-auth accounts | Impacket `GetNPUsers.py`, Rubeus    |
| **Pass-the-Hash**   | NTLM hash            | Impacket, CrackMapExec, Mimikatz    |
| **Pass-the-Ticket** | Kerberos ticket      | Mimikatz, Rubeus                    |
| **DCSync**          | Replication rights   | Mimikatz, Impacket `secretsdump.py` |
| **Golden Ticket**   | KRBTGT hash          | Mimikatz                            |

### Impacket Commands

```bash
# Kerberoasting
GetUserSPNs.py domain/user:password -dc-ip 10.10.10.10 -request
# AS-REP Roasting
GetNPUsers.py domain/ -usersfile users.txt -dc-ip 10.10.10.10 -format hashcat
# Pass-the-Hash
psexec.py domain/user@10.10.10.10 -hashes LM:NTLM
# Dump hashes (DCSync)
secretsdump.py domain/user:password@10.10.10.10
```

### BloodHound Workflow

```
1. Collect data: SharpHound.exe -c All
2. Import into BloodHound
3. Query for:
   - Shortest path to Domain Admins
   - Kerberoastable users
   - AS-REP roastable users
   - Users with DCSync rights
```

## Phase 6: Post-Exploitation

### Linux Privilege Escalation Checklist

|Check|Command|
|---|---|
|Current user|`whoami && id`|
|Sudo permissions|`sudo -l`|
|SUID binaries|`find / -perm -4000 2>/dev/null`|
|Capabilities|`getcap -r / 2>/dev/null`|
|Cron jobs|`cat /etc/crontab && ls -la /etc/cron.*`|
|Writable paths|`find / -writable -type d 2>/dev/null`|
|Kernel version|`uname -a`|
|Running services|`ps aux`|
|Network connections|`netstat -tulpn`|
|Password files|`cat /etc/passwd && cat /etc/shadow`|

**Automation:** LinPEAS, LinEnum, Linux Exploit Suggester

### Windows Privilege Escalation Checklist

|Check|Command|
|---|---|
|Current user|`whoami /all`|
|System info|`systeminfo`|
|Running processes|`tasklist /v`|
|Services|`wmic service list brief`|
|Scheduled tasks|`schtasks /query /fo LIST /v`|
|Network info|`ipconfig /all && netstat -ano`|
|Unquoted service paths|`wmic service get name,pathname`|
|AlwaysInstallElevated|Check registry keys|
|Stored credentials|`cmdkey /list`|
|PowerShell history|Check `ConsoleHost_history.txt`|

**Automation:** WinPEAS, PowerUp, PrivescCheck

## Phase 7: Reporting

### Report Structure

1. **Executive Summary** — High-level findings for leadership
2. **Methodology** — Tools and approach used
3. **Findings** — Each vulnerability with:
    - Title and CVSS score
    - Description
    - Evidence (screenshots, logs)
    - Impact
    - Remediation
4. **Conclusion** — Overall risk assessment
5. **Appendices** — Raw output, additional evidence

### CVSS Scoring Reference

|Score|Severity|
|---|---|
|0.0|None|
|0.1–3.9|Low|
|4.0–6.9|Medium|
|7.0–8.9|High|
|9.0–10.0|Critical|

## Recommended Wordlists (SecLists)

|Purpose|Path|
|---|---|
|Directory brute-forcing|`Discovery/Web-Content/directory-list-2.3-medium.txt`|
|Common files|`Discovery/Web-Content/common.txt`|
|Subdomains|`Discovery/DNS/subdomains-top1million-5000.txt`|
|Usernames|`Usernames/Names/names.txt`|
|Passwords|`Passwords/Leaked-Databases/rockyou.txt`|

## Quick Reference: Tools by Phase

|Phase|Tools|
|---|---|
|**Passive Recon**|whois, dig, theHarvester, Shodan, Google Dorking|
|**Active Recon**|Nmap, ping, traceroute, netcat|
|**Web Scanning**|Gobuster, ffuf, Nikto, Burp Suite|
|**Exploitation**|Metasploit, SQLMap, searchsploit, manual exploits|
|**Password Attacks**|Hydra, John the Ripper, Hashcat, CrackMapExec|
|**AD Attacks**|BloodHound, Impacket, Mimikatz, Rubeus|
|**Post-Exploitation**|LinPEAS, WinPEAS, Mimikatz, PowerUp|
|**Pivoting**|Chisel, ligolo-ng, SSH tunneling, proxychains|
