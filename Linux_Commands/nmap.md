# nmap
- Nmap (**Network Mapper**) is a powerful open-source tool for network discovery and security auditing. On Windows, it works via the command line (CMD or PowerShell) and supports the same syntax as on Linux. Below is a concise cheat sheet for common and advanced usage.

**Basic Target Scans**
- nmap 192.168.1.10 # Scan a single host
- nmap 192.168.1.1,192.168.1.5 # Scan multiple hosts
- nmap -iL targets.txt # Scan hosts from a file
- nmap 192.168.1.0/24 # Scan an entire subnet
- nmap -iR 5 # Scan 5 random hosts

**Port Scanning** 
- nmap -p80 192.168.1.10 # Scan specific port
- nmap -p20-25 192.168.1.10 # Scan a range of ports
- nmap -p- 192.168.1.10 # Scan all 65535 ports
- nmap -F 192.168.1.10 # Fast scan (top 100 ports)

**Scan Types** 
- nmap -sS 192.168.1.10 # TCP SYN scan (stealth)
- nmap -sT 192.168.1.10 # TCP connect scan
- nmap -sU 192.168.1.10 # UDP scan
- nmap -A 192.168.1.10 # Aggressive scan (OS, version, scripts, traceroute)

**Host Discovery**
- nmap -sn 192.168.1.0/24 # Ping scan only
- nmap -Pn 192.168.1.0/24 # Skip host discovery
- nmap -PS22,80 192.168.1.0/24 # TCP SYN ping on specific ports
- nmap -PE 192.168.1.0/24 # ICMP echo ping

**Firewall Evasion**
- nmap -f 192.168.1.10 # Fragment packets
- nmap --source-port 53 192.168.1.10 # Use specific source port
- nmap -D RND:5 192.168.1.10 # Use decoys

**Version & OS Detection**
- nmap -sV 192.168.1.10 # Service version detection
- nmap -O 192.168.1.10 # OS detection
- nmap -O --osscan-guess 192.168.1.10 # Guess OS if uncertain

**Output Options**
- nmap -oN scan.txt 192.168.1.10 # Normal text output
- nmap -oX scan.xml 192.168.1.10 # XML output
- nmap -oA results 192.168.1.10 # All formats (normal, XML, grepable)

**Nmap Scripting Engine (NSE)**
- nmap --script vuln 192.168.1.10 # Run vulnerability scripts
- nmap --script http-waf-detect 192.168.1.10 # Detect WAF
- nmap --script-updatedb # Update script database