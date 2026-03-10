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