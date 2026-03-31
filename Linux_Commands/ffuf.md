# ffuf

A versatile command-line web fuzzing tool for directory discovery, brute-forcing parameters, and more.

**Basic Usage**
- ffuf -w wordlist.txt -u https://target.com/FUZZ
	- Replace *wordlist.txt* with your desired wordlist
	- Replace *https://target.com/FUZZ* with the URL, placing *FUZZ* where you want wordlist items inserted.

**Common Options**
- -u: The target URL
- -w: Wordlist file. Use multiple -w to provide several wordlists
- -H: Add headers (e.g., -H "Cookie: sessionid=12345")
- -X: HTTP method (GET, POST, PUT, DELETE, HEAD, etc.)
- -d: POST data (e.g., -d "username=test&password=FUZZ")
- -t: Number of concurrent threads (increase for speed at the cost of higher bandwidth use)
- -o: Output results to a file in various formats:
	- -of csv
	- -of json
	- -of html

**Filtering Results**
- -mc: Match response by HTTP status code (e.g., -mc 200 for OK)
- -ms: Match response by size (e.g., -ms 500 for sizes around 500 bytes)
- -fc: Filter by status code (e.g., -fc 404 to exclude Not Found)
- -fs: Filter by response size
- -fw: Filter by words present in the response

**Examples ffuff Cheat Sheet**

- **Simple Directory Discovery**
	- ffuf - w /path/to/directory_wordlist.txt -u https://target.com/FUZZ
- **Fuzzing with Headers**
	- ffuf - w passwords.txt -u https://example.org/login -X POST -d "username=admin&password=FUZZ" -H "User-Agent: EvilCorp-Browser"
- **Match and Filter**
	- ffuf -w wordlist.txt -u https://example.org/FUZZ -fs 42 -mc 200
		- \# Find responses with content size around 42 bytes AND status code 200
- **Virtual Host Discovery**
	- ffuf -w vhosts.txt -u https://target.com/ -H "Host: FUZZ" -mc 200


Further results from ChatGPT Research:

# FFUF Command Cheat Sheet

## Executive Summary  
**ffuf** (*Fuzz Faster U Fool*) is a fast command-line web fuzzer (written in Go) used for discovering hidden resources and testing input points in web applications【96†L257-L266】. It automates brute-forcing of URLs, headers, or request data using wordlists. Typical use cases include directory/file discovery, virtual-host probing, parameter fuzzing, and API/JSON payload fuzzing. This report provides categorized **ffuf** command examples for common pentest tasks, explains key flags, recommends wordlists (e.g. from SecLists【95†L108-L114】【95†L238-L242】), notes pitfalls (like avoiding too-large scopes or legal issues), and offers tips for speed/accuracy (such as filtering results and tuning threads). An example workflow (fuzz → verify → exploit → report) is illustrated below, along with a cheat-sheet table of high-value commands.

【74†embed_image】 *Figure: Example FFUF workflow – fuzz (discover) targets, verify interesting results, exploit findings, and report.*  

## ffuf Overview  
- **What is ffuf?** A high-performance web fuzzing tool for discovering hidden content (files, directories, virtual hosts, parameters, etc.) by sending many HTTP requests and filtering results【96†L257-L266】.  
- **When to use it?** In penetration tests to find unlinked pages, subdomains (via Host header fuzzing), or to brute-force API parameters and JSON fields. It’s especially useful when you have or can craft wordlists of likely names.  
- **Key Concepts:** Use the `FUZZ` keyword as a placeholder in the URL, header, or data. Supply a wordlist with `-w`; ffuf replaces `FUZZ` with each entry. You can filter or match by HTTP status (`-mc`, `-fc`), size (`-fs`, `-ms`), word count, regex, etc. Threads (`-t`) and delay (`-p`/`-rate`) control speed. See official docs【96†L290-L299】【98†L491-L500】.

## Command Examples by Use Case  

### Directory/File Discovery  
- **Basic Fuzzing:**  
  ```bash
  ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://target/FUZZ
  ```  
  *Explanation:* Fuzz paths under `https://target/` using a common wordlist (replace `FUZZ`). Hits with valid resources typically return status 200. Use `-mc`/`-fc` to filter specific codes (e.g. `-mc 200`) or `-fs` to filter by size【100†L356-L364】.  
- **Extension Brute-forcing:**  
  ```bash
  ffuf -w common.txt -u http://target/FUZZ -e .php,.html -mc 200
  ```  
  *Explanation:* The `-e` flag appends extensions to each word in `common.txt`. E.g., it tries `FUZZ.php` and `FUZZ.html`【98†L517-L526】.  
- **Recursive Fuzzing:**  
  ```bash
  ffuf -w small.txt -u http://target/FUZZ -recursion -recursion-depth 1 -e .php -v
  ```  
  *Explanation:* Enables recursive scanning (automatically fuzz subdirectories)【95†L163-L172】. Depth 1 means one level down. `-v` for verbose URLs. Use recursion carefully to avoid infinite loops.  

### Virtual Host (vhost) Discovery  
- **Host Header Fuzzing:**  
  ```bash
  ffuf -w subdomains.txt -u https://target/ -H "Host: FUZZ.target.com" -fs 4242
  ```  
  *Explanation:* Fuzzes the `Host:` header, injecting entries (like subdomains) in place of `FUZZ`【96†L318-L325】. Filter out default responses by size (`-fs` 4242 as example). Valid vhosts may return HTTP 200.  
- **DNS-less Subdomain Fuzzing:**  
  ```bash
  ffuf -w subdomains-top1million-1000.txt -u https://FUZZ.example.com/ -mc 200
  ```  
  *Explanation:* Directly fuzz subdomains in the URL (requires that names resolve). Use `-mc 200` to only show successful responses【95†L238-L242】. If DNS isn’t set, this method won’t find anything – consider manual host entries if needed.  

### Parameter and Header Fuzzing  
- **GET Parameter Name:**  
  ```bash
  ffuf -w param-names.txt -u http://target/page.php?FUZZ=test -fc 404
  ```  
  *Explanation:* Replaces `FUZZ` with parameter names. Filtering out 404s helps spot valid params【100†L358-L370】. For known parameter names, fuzz values instead:  
  ```bash
  ffuf -w values.txt -u http://target/page.php?known=FUZZ -mc 200
  ```  
  *Explanation:* Fuzzes parameter values for parameter `known`. Only matches code 200 by default.  
- **Header Field Fuzzing:**  
  ```bash
  ffuf -w header-values.txt -u https://target/ -H "X-Forwarded-For: FUZZ" -mc all -fs 1024
  ```  
  *Explanation:* Fuzzes an HTTP header (`X-Forwarded-For`) values. Use `-mc all` to match any code, then filter by size or regex as needed. Common in finding hidden behavior on certain headers.  

### POST Data / JSON Fuzzing  
- **Simple POST Field:**  
  ```bash
  ffuf -w passlist.txt -u https://target/login -X POST -d "user=admin&pass=FUZZ" -fc 401
  ```  
  *Explanation:* Brute-forces the `pass` value. `-X POST` sets method, `-d` provides data with `FUZZ` placeholder. Here it filters out 401 (failures), showing any success or different responses【96†L348-L349】【100†L378-L380】.  
- **JSON Fuzzing with Mutator:**  
  ```bash
  ffuf --input-cmd 'radamsa --seed $FFUF_NUM example.json' -H "Content-Type: application/json" -X POST -u https://api.example.com/ -mc all -fc 400
  ```  
  *Explanation:* Uses `--input-cmd` with Radamsa (a mutator) to generate JSON payloads on the fly. `$FFUF_NUM` is ffuf’s current position, used as seed【100†L401-L410】. Matches all codes but filters 400. This is advanced, and pre-generation may be faster (see README).  

### Wordlist and Mode Options  
- **Multiple Wordlists (ClusterBomb):**  
  ```bash
  ffuf -w params.txt:PARAM -w values.txt:VAL -u https://target/?PARAM=VAL -mr "admin" -c
  ```  
  *Explanation:* Uses two lists in “clusterbomb” mode (default), fuzzing each `PARAM` with each `VAL`【98†L559-L564】. `-mr "admin"` matches responses containing “admin”. `-c` colorizes output.  
- **Pitchfork Mode:**  
  ```bash
  ffuf -w list1.txt:VAR1 -w list2.txt:VAR2 -u https://target/?VAR1=FUZZ&VAR2=FUZZ -mode pitchfork
  ```  
  *Explanation:* Synchronizes two lists (each position), useful if you have two wordlists of equal length to combine.  

### Filtering and Matching Results  
- **HTTP Status Filtering:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -mc 200,301 -fc 404,500
  ```  
  *Explanation:* `-mc 200,301` only show matches with status 200 or 301. `-fc 404,500` filters out 404 and 500. By default ffuf shows many codes (200-299, 301,302, etc)【98†L491-L500】.  
- **Size/Content Filtering:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -fs 1024 -fr "Error"
  ```  
  *Explanation:* Filters out responses that have size 1024 bytes (`-fs 1024`), and filters out any response containing regex “Error” (`-fr "Error"`)【98†L502-L510】. These help ignore common uninteresting pages.  
- **Regex Matching:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -mr "<title>.*</title>"
  ```  
  *Explanation:* Only shows responses where the HTML `<title>` tag matches the given regex. Use `-mr` to match patterns in the response body【98†L491-L500】.  

### Speed and Control  
- **Threads and Rate:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -t 100 -rate 50
  ```  
  *Explanation:* `-t 100` runs 100 concurrent threads, boosting speed (default 40【98†L485-L493】). `-rate 50` limits to 50 requests/sec to avoid overwhelming the target. Adjust based on target tolerance.  
- **Delay Between Requests:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -p 0.2-1.0
  ```  
  *Explanation:* Random delay between 0.2 and 1.0 seconds (`-p`) to evade rate limits or WAFs【98†L474-L481】.  
- **Timeouts and Retries:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -timeout 5 -replay-proxy https://proxy:8080
  ```  
  *Explanation:* `-timeout 5` seconds per request (default 10)【100†L479-L484】. `-replay-proxy` not for retries but for proxying matched requests (see below). ffuf automatically retries timeouts once by default; use `-timeout` to shorten/lengthen.  

### Output and Reporting  
- **Save Output to File:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -o results.json -of json
  ```  
  *Explanation:* `-o results.json -of json` saves findings in JSON format. ffuf also supports `csv`, `md`, `html`, etc【98†L536-L544】. `-or` avoids creating a file if no matches.  
- **Multi-format Output:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -o output -of all
  ```  
  *Explanation:* `-of all` creates JSON, HTML, Markdown, CSV, etc, all with base name `output`. Good for sharing or documentation.  
- **Silent Mode:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -s
  ```  
  *Explanation:* `-s` (silent) only prints matching results. Useful in scripts or when piping output【98†L474-L481】.  

### Misc and Advanced Features  
- **Cookie/Auth:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -b "SESSION=abcd1234" -H "Authorization: Bearer TOKEN"
  ```  
  *Explanation:* Use `-b` to send cookies, and `-H` multiple times for headers (e.g. tokens). The README notes that multi `-H` flags append to config file【100†L469-L478】. Useful if authentication is needed.  
- **Proxy Usage:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -x http://127.0.0.1:8080
  ```  
  *Explanation:* `-x` sets an HTTP/SOCKS proxy. All ffuf requests will route through this proxy (good for monitoring with Burp). Requires ffuf v2.0+.  
- **TLS Options:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -http2 -r -sni foobar
  ```  
  *Explanation:* `-http2` enables HTTP/2. `-r` follows redirects. `-sni foobar` forces SNI to "foobar". Useful if fuzzing HTTPS with multiple hostnames.  
- **Auth Certs:**  
  ```bash
  ffuf -w dict.txt -u https://target/FUZZ -cc client.pem -ck client.key
  ```  
  *Explanation:* For client-certificate auth, use `-cc`/`-ck` to provide cert and key (must be valid). This allows fuzzing behind mutual TLS.  

## Common Pitfalls & Tips  
- **Wordlist Quality:** Use curated lists (e.g. SecLists【95†L108-L114】). Remove comments (`-ic`) and empty lines from lists to avoid noise. SecLists/Discovery includes many suited for path/param fuzzing.  
- **Scope Caution:** Never run large scans indiscriminately. Fuzzing everything on a production server can crash it or trigger alerts. Always have permission and start small (`-p` delay, limited threads), then ramp up.  
- **Filtering:** Many hits will be 404s or boilerplate errors. Use `-fc`, `-fs`, `-fl` to filter common sizes and statuses. For example, identify the typical “not found” size and `-fs` it out.  
- **Recursion Explosion:** Recursive fuzzing can loop endlessly in directory structures. Always set a safe `-recursion-depth` and monitor output.  
- **Interactive Mode:** Hit `ENTER` during a run to pause and get an interactive shell with ffuf. Useful to adjust filters on the fly (see `help` menu in README)【98†L567-L576】.  
- **Rate-limiting:** If requests are too fast, add `-rate` or delay (`-p`). Also consider `-replay-proxy` to send matched requests through a proxy that can slow them.  
- **Collisions in Multi-wordlists:** In multi modes (clusterbomb/pitchfork), make sure you understand combination logic. `pitchfork` pairs items by index; `clusterbomb` does all pairs.  

## Cheat-Sheet Table (High-Value Commands)

| Use Case                           | Command                                                                                                                                                   | Explanation                                                                               | Notes                                                                                              |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **Dir/File Discovery**             | `ffuf -w /usr/share/wordlists/common.txt -u https://example.com/FUZZ`                                                                                     | Fuzz URL paths using wordlist. Hits (200) indicate valid pages.                          | Use `-mc`/`-fs` to filter. Wordlists: SecLists *Discovery/Web-Content/*【95†L108-L114】.              |
| **Extension Brute (Dir)**          | `ffuf -w names.txt -u http://ex.com/FUZZ -e .php,.html -mc 200`                                                                                            | Append `.php` and `.html` to each word.                                                  | `-e` extends FUZZ. Handles sites where directories without extension give 404.                     |
| **Recursive Fuzzing**              | `ffuf -w small.txt -u https://ex.com/FUZZ -recursion -recursion-depth 2 -e .php`                                                                          | Fuzz subdirs recursively (depth 2), adding .php.                                         | Requires trailing FUZZ in URL. `-v` for full URLs. Danger: huge scope.                            |
| **Virtual Host Discovery**         | `ffuf -w subdomains.txt -u https://target/ -H "Host: FUZZ.target.com" -fs 4242`                                                                            | Fuzz Host header for vhosts, filtering default size 4242.                               | Ensure default host returns fixed size to filter. Subdomains can also be resolved.                 |
| **Subdomain Discovery (DNS)**      | `ffuf -w subnames.txt -u https://FUZZ.example.com/ -mc 200`                                                                                                | Fuzz subdomain names via URL.                                                           | Only works if DNS for `FUZZ.example.com` exists. SecLists has DNS lists (e.g. *Discovery/DNS*).   |
| **GET Param Name**                 | `ffuf -w params.txt -u http://ex.com/page.php?FUZZ=test -fc 404`                                                                                          | Fuzz parameter names. Filters out 404.                                                  | Valid param names may give 200/other codes.                                                       |
| **GET Param Value**                | `ffuf -w words.txt -u http://ex.com/page.php?id=FUZZ -mc 200`                                                                                             | Fuzz known param `id` values, only match 200.                                           | Adjust `-mc` or add `-fc` for others (e.g. 401 auth).                                             |
| **Header Value Fuzzing**           | `ffuf -w proxies.txt -u https://target/ -H "X-Forwarded-For: FUZZ" -mc all -fs 0`                                                                          | Fuzz XFF header with proxies list, show anything with content (size>0).                  | Often reveals hidden logs/blocks.                                                                |
| **POST Form Fuzzing**              | `ffuf -w passwords.txt -u https://ex.com/login -X POST -d "user=admin&pass=FUZZ" -fc 401`                                                                  | Brute-forces password field. Filters 401.                                               | Combine with `-H "Content-Type: application/x-www-form-urlencoded"`.                              |
| **JSON API Fuzzing**               | `ffuf -w inputs.txt -X POST -H "Content-Type: application/json" -d '{"user":"admin","val":FUZZ}' -u https://api/ex -mr "success"`                           | Fuzz JSON value field. Matches JSON “success” in response.                              | Use `--raw` if values require no URL-encoding.                                                  |
| **Multi (ClusterBomb)**            | `ffuf -w keys.txt:K -w values.txt:V -u https://site/?K=V -mr "admin"`                                                                                     | Brute-forces combos of key/value pairs. Matches if “admin” in body.                      | Mode defaults to clusterbomb.                                                                   |
| **Multi (Pitchfork)**              | `ffuf -w users.txt:U -w pass.txt:P -u https://site/login?user=U&pass=P -mode pitchfork -mc 200`                                                           | Pairs each user with password by index.                                                | Useful when two lists align.                                                                    |
| **Status Filter (match)**          | `ffuf -w dict.txt -u https://example/FUZZ -mc 200,301 -fc 404`                                                                                           | Show only 200/301, filter 404s.                                                         | `-mc` = match codes, `-fc` = filter codes.                                                      |
| **Size Filter**                    | `ffuf -w dict.txt -u https://target/FUZZ -fs 1432`                                                                                                       | Filter out responses of 1432 bytes (e.g. default “not found”).                         | Find common 404 size then use `-fs` to remove noise.                                             |
| **Word/Line Filter**               | `ffuf -w dict.txt -u http://ex/FUZZ -fw 100 -fl 5`                                                                                                       | Only show results with 100 words and 5 lines.                                           | Useful if 404s have a known word/line count.                                                   |
| **Regex Filter**                   | `ffuf -w list.txt -u https://target/FUZZ -fr "(?i)Error"`                                                                                                 | Exclude any response containing “Error” (case-insensitive).                             | Useful to eliminate known error pages.                                                         |
| **Threads & Rate**                 | `ffuf -w dict.txt -u http://site/FUZZ -t 100 -rate 50`                                                                                                   | Use 100 threads, limit to 50 req/sec.                                                  | Adjust `-t` and `-rate` based on target capacity.                                               |
| **Delay**                          | `ffuf -w dict.txt -u https://target/FUZZ -p 0.5`                                                                                                         | Delay 0.5s between requests.                                                           | Can specify a range (`-p 0.1-1.0`) for random sleep.                                           |
| **Timeout/Max Time**               | `ffuf -w dict.txt -u https://example/FUZZ -timeout 3 -maxtime 60`                                                                                       | Per-request timeout 3s, overall run max 60s.                                          | Avoids long hangs. Note `-maxtime-job` for recursion contexts【96†L353-L363】【100†L389-L396】.  |
| **Output to JSON**                 | `ffuf -w dict.txt -u https://target/FUZZ -o results.json -of json`                                                                                       | Save findings to `results.json` in JSON format.                                       | Also supports `csv`, `html`, `md`, etc【98†L536-L544】.                                         |
| **Multi-format Output**            | `ffuf -w dict.txt -u https://target/FUZZ -o out -of all`                                                                                                 | Generate all supported formats (json, html, csv, etc) with base name “out”.            | Great for full reporting; large files.                                                         |
| **Silent Mode**                    | `ffuf -w dict.txt -u https://site/FUZZ -s`                                                                                                               | Only print matched results (no progress/details).                                     | Useful in scripts or piping.                                                                   |
| **Authentication (Cookie)**        | `ffuf -w dict.txt -u https://target/FUZZ -b "SESSION=abcd"`                                                                                              | Include cookie in requests.                                                            | Also `-H "Auth: token"` for header tokens.                                                     |
| **Proxy**                          | `ffuf -w list.txt -u https://ex/FUZZ -x http://127.0.0.1:8080`                                                                                           | Route requests through proxy (HTTP/SOCKS).                                            | Works with tools like Burp for interception.                                                   |
| **TLS/SNI Options**                | `ffuf -w list.txt -u https://ex/FUZZ -http2 -r -sni foo`                                                                                                 | Enable HTTP/2 (`-http2`), follow redirects (`-r`), force SNI “foo”.                    | Useful when testing virtual hosts over TLS.                                                   |
| **POST JSON (simple)**             | `ffuf -w values.txt -X POST -H "Content-Type: application/json" -d '{"a":"FUZZ"}' -u https://api/ex -mc 200`                                          | Fuzz JSON field “a”. Only 200s shown.                                                | Use `-raw` if `FUZZ` contains URL-unsafe chars.                                               |
| **Parameter List (DirSearch)**     | `ffuf -w dirsearch:FUZZ -u http://target/FUZZ -e .php,.bak -mc 200`                                                                                      | Use DirSearch-format wordlist (prefix `dirsearch:`) to auto-handle comments etc.       | `-ic` can also ignore `#` comments【98†L521-L526】.                                            |
| **Extensive Match (all codes)**    | `ffuf -w dict.txt -u https://target/FUZZ -mc all`                                                                                                        | Show results for any HTTP status.                                                      | Good for seeing all responses, then filtering manually.                                      |
| **Match on Content**               | `ffuf -w dict.txt -u https://target/FUZZ -mr "<h1>(.*?)</h1>"`                                                                                            | Show only responses where regex `<h1>...</h1>` matches.                               | Useful to find pages with specific content.                                                  |
| **No Output File**                 | `ffuf -w dict.txt -u https://target/FUZZ -o out.json -of json -or`                                                                                        | Skip writing file if no results (due to `-or`).                                      | Prevents empty result files.                                                                 |

*Notes:* Replace `FUZZ` with actual keywords or use `:KEYWORD` syntax with `-w`. Always choose appropriate wordlists (SecLists: e.g. *Discovery/Web-Content/*, *Discovery/DNS/*)【95†L108-L114】【95†L238-L242】. Adjust threads and filters for the target’s tolerance. Avoid sweeping sensitive systems or performing fuzzing on production without permission. Use `-w` with care: massive lists can overload targets or produce too many results to analyze.

**Sources:** ffuf official README and Wiki【100†L356-L364】【98†L549-L558】; SecLists wordlist repository【95†L108-L114】; community writeups【95†L163-L172】【95†L238-L242】. These examples reflect common usage patterns in modern penetration tests.