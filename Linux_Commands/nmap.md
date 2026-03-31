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


Extra information from ChatGPT research:

# Nmap Command Cheat Sheet  

## Executive Summary  
**Nmap** (*Network Mapper*) is a free, open-source tool for network discovery and security auditing【133†L72-L80】. It is commonly used in penetration testing to find live hosts, open ports, services, and OS details on a network. Nmap sends crafted packets and analyzes responses to determine which hosts are up, which ports/protocols are open, and what software versions they run【133†L72-L80】【124†L65-L74】. It supports many scan types (TCP SYN, connect, UDP, FIN/NULL/XMAS, etc) and advanced features (OS detection `-O`, version detection `-sV`, scripting `-sC`/`--script`, timing templates, decoys/spoofing, etc)【124†L65-L74】【107†L74-L83】. In practice, a typical workflow is: **discover** active hosts (ping sweeps, ARP, etc), **scan** ports/services (using appropriate scan types and NSE scripts), **enumerate** details (version/OS detection, traceroute), and **report** findings. This guide provides categorized Nmap command examples for common pentest use cases, each with explanations and tips. An example scanning workflow is illustrated below, along with a cheat-sheet table of high-value commands.

【74†embed_image】 *Figure: Example scanning workflow (host discovery → port scanning → service enumeration → reporting).*  

## Host Discovery  
Discovering which hosts are up is the first step. By default, Nmap does a “ping scan” (ICMP echo, TCP SYN to 443, ACK to 80, etc) to find live hosts【104†L45-L53】. Useful options include:  
- **Ping sweep (no port scan):** `nmap -sn 192.168.1.0/24` – sends ping probes and lists up hosts【104†L45-L53】. Formerly `-sP`.  
- **List scan (no probes):** `nmap -sL 10.0.0.0/24` – prints the targets (with DNS lookup) but sends no packets【104†L69-L77】. Good as a sanity check.  
- **Skip discovery:** `nmap -Pn 10.0.0.1-50` – treats all specified targets as up and scans them (no ping). Useful when targets block ping or when you trust your target list【104†L118-L126】. Risky on large ranges, as it can be very slow.  
- **TCP ping:** e.g. `nmap -PS22,80 target.com` – sends TCP SYN “pings” to the given ports instead of ICMP. Ports default to 80 if not given【104†L45-L53】. There is also `-PA` (ACK ping) and `-PU` (UDP ping). These can bypass networks that block ICMP.  

**Tip:** Use `-sn` or `-n` (no DNS) to speed up host discovery. Observe that host discovery may miss hosts behind strict firewalls; consider combining multiple ping types (e.g. `-PE -PS80 -PA443`)【104†L45-L53】【104†L63-L72】. Always obtain authorization before scanning.  

## Port Scanning Techniques  
After identifying up hosts, port scanning finds open ports. Nmap offers many scan types, each with trade-offs【124†L65-L74】. Common ones include:  
- **TCP SYN (half-open) scan:** `nmap -sS target.com` – the default stealthy scan (requires root). Sends SYN, waits for SYN/ACK (open) or RST (closed). Fast and stealthier than a full connect【124†L65-L74】. Most popular choice on pentests.  
- **TCP Connect scan:** `nmap -sT target.com` – fallback for unprivileged users. Completes full TCP handshake (slower and more obvious)【124†L87-L96】. Use if root access is not available.  
- **UDP scan:** `nmap -sU -p 53,161 192.168.1.1` – scans UDP ports (e.g. DNS, SNMP). UDP is slower (no handshake). Nmap sends empty UDP and relies on ICMP unreachable or no response【124†L112-L120】. Many UDP ports appear “open|filtered” if no response; this is expected.  
- **FIN/NULL/XMAS scans:** `nmap -sF target.com` / `-sN` / `-sX` – send FIN, no flag, or FIN+PSH+URG packets respectively【126†L192-L202】. On open ports, these typically elicit no response, on closed ports they provoke RST. Useful for stealth (some firewalls/IDS don’t log these), but many modern systems (especially Windows) ignore this and mark all ports closed【126†L204-L213】. Use with caution.  
- **ACK scan:** `nmap -sA target.com` – sends ACK packets. It never finds open ports; instead it reveals filtered/unfiltered to map firewall rules【126†L222-L231】. Labeled ports show as “unfiltered” if reachable. Good for firewall/ACL analysis.  
- **Window scan:** `nmap -sW target.com` – similar to ACK, but examines TCP Window size in the RST to guess open ports【126†L236-L245】. Very rare, depends on uncommon TCP behavior.  
- **Maimon scan:** `nmap -sM target.com` – sends FIN/ACK. Some BSD systems drop it on open ports (so finds open), but others (e.g. Linux) reset on both, showing none【126†L257-L266】. Rare.  
- **SCTP scans:** e.g. `nmap -sY target.com` (INIT) or `-sZ` (COOKIE-ECHO) for scanning SCTP transport (rare on IPv4). Use when dealing with SCTP networks.  

Specify port ranges or lists with `-p`. For example: `nmap -p 1-65535 -sS target.com` scans all TCP ports. Use `--top-ports <N>` for common top ports. Beware that scanning large port ranges and UDP takes much longer.  

## Service and Version Detection  
Knowing the service version is key for vulnerability assessment【107†L29-L38】. Nmap sends probes from the `nmap-service-probes` database to identify service and version. Common options:  
- **Version detection:** `nmap -sV target.com` – tries to detect service versions on open ports【107†L74-L83】. Often used after port scan or with `-A`.  
- **Aggressive scan:** `nmap -A target.com` – runs `-sV`, OS detection, default scripts, and traceroute in one shot【107†L74-L83】【109†L65-L72】. Quick overall fingerprint. Note: very noisy.  
- **All ports:** `nmap --version-all target.com` – tests every probe (max intensity 9) to improve detection【107†L114-L117】. Much slower; use sparingly.  
- **Version intensity:** `nmap --version-intensity 4 target.com` – lower levels (0–9) tune speed vs accuracy【107†L94-L103】. Default is 7. Use `--version-light` (intensity 2) for faster but less thorough checks【107†L108-L112】.  
- **Specific script categories:** e.g. `nmap --script http-title --script-args default or` (no, hmm). Actually for version detection, use `-sV` or mention scripts in NSE.

**Notes:** Version detection is more intrusive (pulls banners). Some services (e.g. printers on 9100) may flood with output; Nmap skips them by default. Use `--allports` to include excluded ones or modify `nmap-service-probes`. Also, `-A` includes version detection by default【107†L74-L83】.

## OS Detection and Traceroute  
Fingerprinting the OS uses TCP/IP stack quirks【109†L21-L30】. Key commands:  
- **OS detection:** `nmap -O target.com` – attempts to identify OS by probing TCP/IP behavior【109†L21-L30】. Requires at least one open and one closed TCP port to be reliable.  
- **Aggressive scan (`-A`):** also enables OS detection【109†L65-L68】.  
- **OS scan limit:** `nmap --osscan-limit target.com` – skip OS detection on targets that don’t have both open and closed ports (saves time)【109†L70-L79】.  
- **Aggressive OS guess:** `nmap --osscan-guess target.com` – report best guesses when no perfect match is found【109†L78-L86】 (may give lower-confidence results).  
- **Traceroute:** `nmap --traceroute target.com` – appends a traceroute to the Nmap scan, showing hops to the target. Useful for mapping network path (as seen in sample output)【119†L62-L71】. Nmap automatically traceroutes after an `-A` scan, but you can force it with `--traceroute`.  

## NSE Scripting and Enumeration  
Nmap’s Scripting Engine (NSE) provides hundreds of scripts for vulnerability discovery and enumeration【113†L21-L30】. Common usage:  
- **Default scripts:** `nmap -sC target.com` – runs “default” category scripts (same as `--script=default`), such as basic version probes, safe checks, and common vuln checks【113†L21-L30】. Equivalent to adding `-sC` or using `-A`.  
- **Category scans:** `nmap --script vuln target.com` – run all vulnerability-related scripts (e.g. `ms17-010`, heartbleed, etc). Combine with `-p` to focus on a port.  
- **Specific scripts:** e.g. `nmap --script http-vuln-cve2017-5638 target.com:8080` to run a named script (CVE-2017-5638 for Struts).  
- **Script arguments:** Use `--script-args` to supply parameters, or `--script-args-file`.  
- **Safe vs intrusive:** Use `-sC` (default safe) during a test. Intrusive scripts (e.g. brute force) should be chosen explicitly. Avoid `--script=external` (e.g. whois) if privacy is a concern【113†L46-L54】【113†L74-L83】.  

**Tip:** Running all scripts can be very slow. Target specific categories or scripts for likely issues (e.g. `--script ssl-enum-ciphers,default`). Always review script documentation (`--script-help <script>`) before use.

## Timing and Performance  
Nmap’s timing templates (`-T0` to `-T5`) adjust speed vs stealth【117†L158-L163】. Examples:  
- **Paranoid:** `-T0` (serial, very slow, avoids IDS).  
- **Sneaky:** `-T1`.  
- **Polite:** `-T2` (slower to reduce load).  
- **Normal:** `-T3` (default).  
- **Aggressive:** `-T4` (faster, slight risk of missing devices or causing IDS alerts).  
- **Insane:** `-T5` (max speed; uses minimal waits).  

Choosing a higher `-T` makes scans faster but noisier. Use `-T0`/`1` behind strong defenses to avoid detection, or `-T4`/`5` on trusted networks for speed. The GeeksforGeeks guide notes: “Low scan speeds (-T0/1) are virtually undetectable but take much longer”【117†L158-L163】. Combine with `--min-rate` or `--max-rate` to set custom packet rates.  

Use `--host-timeout` to abort slow hosts (e.g. `--host-timeout 10m` to skip a host after 10 minutes). Use `--max-retries` and `--initial-rtt-timeout` to tune retries/timeouts (detailed in man page). 

## Firewall/IDS Evasion  
Nmap offers flags to obfuscate scans:  
- **Decoys:** `nmap -D RND:10,ME target.com` – spoof decoy IPs in scan. “ME” represents your IP; others are random or specified. Increases noise footprint to confuse IDS. IDS can often filter these, so not foolproof【129†L378-L384】.  
- **IP Spoof:** `nmap -S 1.2.3.4 target.com` – set a fake source address (requires that spoofing is possible on your network). Responses will go to that IP, so not normally used without interception.  
- **Fragmentation:** `nmap -f target.com` – fragment packets (IPv4 only). May bypass simple packet filters. Not very effective against modern firewalls.  
- **Source port:** `nmap --source-port 53 target.com` – send all probes from a specific source port (e.g. 53 DNS) that may bypass ACLs. Some admins filter based on source port.  
- **Interface selection:** `nmap -e wlan0 target.com` – choose a specific interface (useful on hosts with multiple NICs, or with tools like bettercap).  
- **Randomize hosts:** `nmap --randomize-hosts -iL targets.txt` – randomize scanning order (may evade pattern-based detection).  

**Caution:** Evasive scans can consume more time or arouse suspicion if misused. IPv6 scans (`-6`) also require careful handling (skip e.g. multicast, etc). Always avoid interfering with unrelated networks when using spoofing or decoys.

## Output and Logging  
Capture results for analysis:  
- **Normal (`-oN`):** `nmap -oN scan.txt target.com` – saves human-readable output.  
- **XML (`-oX`):** `nmap -oX scan.xml target.com` – XML format (parsable by tools). Often used for integration (e.g. with vulnerability scanners).  
- **Grepable (`-oG`):** `nmap -oG scan.gnmap target.com` – old “grepable” format (semi-deprecated). Still used in some scripts.  
- **All (`-oA`):** `nmap -oA outbase target.com` – produces `outbase.nmap`, `.xml`, and `.gnmap`. Convenient for saving all.  
- **Append to file:** `-oN -` writes to stdout (useful for piping), or `-append-output` to append instead of overwrite.  
- **Live console:** `-v` (verbose) or `-d` (debug) for on-screen details.  
- **Max rate:** `--max-rate 1000` to cap packets/sec. For very large networks, consider `--min-hostgroup` and `--min-rtt-timeout`.

Always interpret output carefully. Example snippet (SYN scan with version/OS/traceroute)【119†L41-L49】:

```
# nmap -T4 -A -p- -oN - scanme.nmap.org
Nmap scan report for scanme.nmap.org (64.13.134.52)
Host is up (0.045s latency).
Not shown: 993 filtered ports
PORT      STATE  SERVICE VERSION
22/tcp    open   ssh     OpenSSH 4.3 (protocol 2.0)
80/tcp    open   http    Apache httpd 2.2.3 ((CentOS))
...
Device type: general purpose
Running: Linux 2.6.X
OS details: Linux 2.6.13 - 2.6.31
...
TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
...
```

This shows discovered ports with services/versions, inferred OS, and traceroute hops【119†L41-L49】【119†L62-L70】. 

**Safety Note:** Nmap scans can be intrusive and are often logged. Only scan networks you have permission to test. UDP scans and Version scans, in particular, can cause higher traffic or trigger IDS alarms. Always verify legality and work scope before scanning.

## Cheat-Sheet Table (High-Value Commands)

| Use Case                    | Command                                           | Explanation                                     | Notes                                           |
|-----------------------------|----------------------------------------------------|-------------------------------------------------|-------------------------------------------------|
| **Host Discovery (ping)**   | `nmap -sn 192.168.1.0/24`                         | Ping sweep (no port scan): lists alive hosts.   | Formerly `-sP`. Useful to map online devices.   |
| **List Scan**               | `nmap -sL 10.0.0.0/24`                            | List targets (DNS resolution only).             | No packets sent. Use for sanity check of targets. |
| **Skip Ping**               | `nmap -Pn 10.0.0.1-50`                            | Treat all as up and scan ports.                 | Use when hosts block ICMP. Can be slow on large ranges. |
| **TCP SYN Scan**            | `nmap -sS target.com`                             | Stealthy SYN scan (fast, requires root).        | Default method. Detects open/closed vs filtered【124†L65-L74】. |
| **TCP Connect Scan**        | `nmap -sT target.com`                             | Full TCP handshake (no raw sockets needed).     | Less stealthy. Use if not root.                |
| **UDP Scan**                | `nmap -sU -p 53,161 target.com`                   | Scan UDP ports (DNS, SNMP). Slow (no handshake). | Often report many “open|filtered”. Requires patience. |
| **Top Ports**               | `nmap --top-ports 100 target.com`                 | Scan the 100 most common ports.                 | Faster than full range for quick scan.         |
| **Aggressive Scan**         | `nmap -A target.com`                              | OS + version + default scripts + traceroute.   | Very noisy. Use when comprehensive info needed. |
| **Version Detection**       | `nmap -sV target.com`                             | Identify service versions on open ports.       | Increases accuracy of service ID.              |
| **Version Intensity**       | `nmap --version-intensity 9 target.com`           | Full-intensity version scan (slow).            | Intensity 0–9 (default 7)【107†L94-L103】.       |
| **Light Version Scan**      | `nmap --version-light target.com`                 | Shorthand for `--version-intensity 2`.         | Faster, less comprehensive【107†L108-L112】.   |
| **OS Detection**            | `nmap -O target.com`                              | Remote OS fingerprinting (requires open+closed port)【109†L63-L72】. | Use with `-A` or after port scan.              |
| **OS Guess**                | `nmap --osscan-guess target.com`                  | More aggressive OS guesses if no exact match.  | May produce lower-confidence results【109†L78-L86】. |
| **Traceroute**              | `nmap --traceroute target.com`                    | Trace route to host (appended to scan results). | Useful for network mapping.                   |
| **SYN/FIN/NULL/XMAS**       | `nmap -sS -sF -sN -sX target.com`                 | Stealth scans: SYN, FIN, Null, and Xmas.       | Try each separately. Can bypass some firewalls. |
| **FIN Scan**                | `nmap -sF target.com`                             | TCP FIN scan (no SYN).                          | No response = open|filtered; RST = closed【126†L204-L213】. |
| **NULL Scan**               | `nmap -sN target.com`                             | TCP NULL scan (no flags).                      | Same behavior as FIN/XMAS【126†L204-L213】.      |
| **XMAS Scan**               | `nmap -sX target.com`                             | TCP Xmas scan (FIN,PSH,URG).                   | Same behavior; opens “light up” a Xmas tree.   |
| **ACK Scan**                | `nmap -sA target.com`                             | TCP ACK scan (firewall rule discovery).       | Reveals filtered (no response) vs unfiltered【126†L224-L233】. |
| **Window Scan**             | `nmap -sW target.com`                             | TCP Window scan (variant of ACK).              | Tries to infer open vs closed via RST window【126†L236-L245】. |
| **FTP Bounce**              | `nmap -b user:pass@ftp.example.com:21 target`     | FTP bounce scan via third-party FTP server.    | Very old technique (mostly disabled now).      |
| **Default Scripts**         | `nmap -sC target.com`                             | Run default NSE scripts (same as `--script=default`). | Includes safe version checks, auth, etc【113†L21-L30】. |
| **Specific Script**         | `nmap --script http-title target.com`            | Run named NSE script(s).                       | `--script=category` or path also possible.    |
| **Brute Force (NSE)**       | `nmap --script ssh-brute -p 22 target.com`       | Brute-force SSH (example brute script).         | Very slow and intrusive; use carefully.       |
| **Timing: Aggressive**      | `nmap -T4 target.com`                              | Faster scan (adjusts timeouts/retries).       | `-T0..-T5` templates available. See timing tips【117†L158-L163】. |
| **Verbose**                 | `nmap -v target.com`                              | Increase output detail.                        | Add multiple `-v` for more verbosity.        |
| **Mass Scan (list)**        | `nmap -iL targets.txt -T4`                        | Read targets from file, use faster timing.    | Combine with `-Pn` to scan all listed.       |
| **Exclude Hosts**           | `nmap 10.0.0.0/24 --exclude 10.0.0.5`            | Scan range but skip listed IPs.               | Comma-separated excludes.                    |
| **Interface/IP Spoof**      | `nmap -e eth0 target.com`                         | Specify outgoing interface (or source IP).    | Useful for multi-homed hosts or spoofing.    |
| **Decoys**                  | `nmap -D decoy1,ME,decoy2 target.com`             | Add decoy spoofed hosts (ME=you).             | Confuse IDS, but can be filtered.            |
| **Fragment Packets**        | `nmap -f target.com`                              | Fragment IP packets into tiny pieces.         | May slip past simple filters.                |
| **IPv6 Scan**               | `nmap -6 [2001:db8::1]`                           | Scan IPv6 addresses.                          | IPv6 hosts must respond to IPv6 probes.      |
| **Output All Formats**      | `nmap -oA scanall target.com`                     | Save to `scanall.nmap/.xml/.gnmap`.            | Combines -oN, -oX, -oG.                      |
| **XML Output**              | `nmap -oX results.xml target.com`                | Save XML for parsing/import.                 | Useful for tools integration.                |
| **Normal Output**           | `nmap -oN scan.txt target.com`                    | Save human-readable output.                   | Can be grepped later.                        |
| **Proxy (via socks)**       | *Use proxychains or socksifier; nmap has no native proxy option.* | Use external tool to route Nmap through a proxy. | Nmap must see target as reachable (socks).   |

*Notes:* Customize each command to the target. E.g., use `-p` to specify ports; add `-v` for verbosity or `-d` for debug output. Always run Nmap with root/admin privileges for raw scans (`-sS`, `-sU`, `-O`, etc). Watch out for IDS/IPS and obtain permission before scanning. UDP scans should be used judiciously (they are slow and may produce many filtered results). When scanning large networks, consider breaking into smaller subnets, using `-T3` or lower for stealth, and using `-oX` to easily aggregate results. For automation, parse XML or grepable output, or use `ndiff` to compare scans.

**Sources:** Official Nmap documentation and reference guide【104†L21-L30】【124†L65-L74】【107†L74-L83】【109†L63-L72】, Nmap security scanner book, and community write-ups. Sample output and flags are based on Nmap usage best practices【119†L41-L49】【117†L158-L163】. All information reflects Nmap version 7.x (as of 2026) and authoritative Nmap resources.