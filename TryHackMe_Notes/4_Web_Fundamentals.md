# Web Fundamentals
## How The Web Works
### DNS in Detail
- Refer to [[1_Pre_Security]]
### HTTP in Detail
- Refer to [[1_Pre_Security]]
### How Websites Work
- Refer to [[1_Pre_Security]]
### Putting it all together
- Refer to [[1_Pre_Security]]
## Introduction to Web Hacking
### Walking An Application
- Refer to [[3_Jr_Penetration_Tester]]
### Content Discovery
- Refer to [[3_Jr_Penetration_Tester]]
### Subdomain Enumeration
- Refer to [[3_Jr_Penetration_Tester]]
### Authentication Bypass
- Refer to [[3_Jr_Penetration_Tester]]
### IDOR
- Refer to [[3_Jr_Penetration_Tester]]
### File Inclusion
- Refer to [[3_Jr_Penetration_Tester]]
### Intro to SSRF
- Refer to [[3_Jr_Penetration_Tester]]
### Intro to Cross-site Scripting
- Refer to [[3_Jr_Penetration_Tester]]
### Race Conditions
- Refer to [[3_Jr_Penetration_Tester]]
### Command Injection
- Refer to [[3_Jr_Penetration_Tester]]
### SQL Injection
- Refer to [[3_Jr_Penetration_Tester]]
## Burp Suite
### Burp Suite: The Basics
- Refer to [[3_Jr_Penetration_Tester]]
### Burp Suite: Repeater
 - Refer to [[3_Jr_Penetration_Tester]]
### Burp Suite: Intruder
- Refer to [[3_Jr_Penetration_Tester]]
### Burp Suite: Other Modules
- Refer to [[3_Jr_Penetration_Tester]]
### Burp Suite: Extensions
- Refer to [[3_Jr_Penetration_Tester]]
## Web Hacking Fundamentals
### How Websites Work
- When you visit a website, your browser (like Safari or Google Chrome) makes a request to a web server asking for information about the page you're visiting. It will respond with data that your browser uses to show you the page; a web server is just a dedicated computer somewhere else in the world that handles your requests.
- There are two major components that make up a website:
	- Front End (Client-Side) - the way your browser renders a website.
	- Back End (Server-Side) - a server that processes your request and returns a response.
- Websites are primarily created using:
	- HTML, to build websites and define their structure.
	- CSS, to make websites look pretty by adding styling options.
	- JavaScript, implement complex features on pages using interactivity.
- HyperText Markup Language (HTML) is the language websites are written in. Elements (also known as tags) are the building blocks of HTML pages and tells the browser how to display content. 
- JavaScript (JS) is one of the most popular coding languages in the world and allows pages to become interactive. HTML is used to create the website structure and content, while JavaScript is used to control the functionality of web pages - without JavaScript, a page would not have interactive elements and would always be static.
- Sensitive Data Exposure occurs when a website doesn't properly protect (or remove) sensitive clear-text information to the end-user; usually found in a site's frontend source code.
- We now know that websites are built using many HTML elements (tags), all of which we can see simply by "viewing the page source". A website developer may have forgotten to remove login credentials, hidden links to private parts of the website or other sensitive data shown in HTML or JavaScript.
- **HTML Injection** - HTML Injection is a vulnerability that occurs when unfiltered user input is displayed on the page. If a website fails to sanitize user input (filer any "malicious" text that a user inputs into a website), and that input is used on the page, an attacker can inject HTML code into a vulnerable website.
![[Pasted image 20260304135505.png]]
### HTTP in Detail
- HyperText Transfer Protocol (HTTP) is what's used whenever you view a website, developed by Tim Berners-Lee and his team between 1989 - 1991.
- HyperText Transfer Protocol Secure (HTTPS) is a secure version of HTTP. HTTPS data is encrypted so it not only stops people from seeing the data you are receiving and sending, but it also give you assurances that you're talking to the correct web server and not something impersonating it.
- A URL (Uniform Resource Locator) is predominately an instruction on how to access a resource on the internet. The below image shows what a URL looks like with all of its features (it does not use all features in every request). 
![[Pasted image 20260304140557.png]]
	- **Scheme**: This instructs on what protocol to use for accessing the resource such as HTTP, HTTPS, FTP (File Transfer Protocol)
	- **User**: Some services require authentication to log in, you can put a username and password into the URL to log in.
	- **Host**: The domain name or IP address of the server you wish to access.
	- **Port**: The Port that you are going to connect to, usually 80 for HTTP and 443 for HTTPS, but this can be hosted on any port between 1 - 65535.
	- **Path:** The file name or location of the resource you are trying to access.
	- **Query String**: Extra bits of information that can be sent to the requested path. For example, /blog?id=1 would tell the blog path that you wish to receive the blog article with the id of 1.
	- **Fragment**: This is a reference to a location on the actual page requested. This is commonly used for pages with long content and can have a certain part of the page directly linked to it, so it is viewable to the user as soon as they access the page.
- It's possible to make a request to a web server with just one line **GET / HTTP/1.1** 
- **HTTP Methods**: HTTP Methods are a way for the client to show their intended action when making an HTTP request. There are a lot of HTTP methods but we'll cover the most common ones, although mostly you'll deal with the GET and POST method.
	- **GET Request** - This is used for getting information from a web server.
	- **POST Request** - This is used for submitting data to the web server and potentially creating new records.
	- **PUT Request** - This is used for submitting data to a web server to update information.
	- **DELETE Request** - This is used for deleting information/records from a web server.
- **HTTP Status Codes** [[HTTP_Status_Codes]]: The status codes can be broken down into 5 different ranges:

| 100-199 - Information Response | These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common. |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200 - 299 - Success            | This range of status codes is used to tell the client their request was successful.                                                                                                    |
| 300 - 399 - Redirection        | These are used to redirect the client's request to another resource. This can be either to a different webpage or a different website altogether.                                      |
| 400 - 499 - Client Errors      | Used to inform the client that there was an error with their request.                                                                                                                  |
| 500 - 599 - Server Errors      | This is reserved for errors happening on the server-side and usually indicate quite a major problem with the server handling the request.                                              |
- **Common HTTP Status Codes**:

| 200 - OK                     | The request was completed successfully.                                                                                                                                                                                       |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 201 - Created                | A resource has been created (for example a new user or new blog post)                                                                                                                                                         |
| 301 - Moved Permanently      | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.                                                                                |
| 302 - Found                  | Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future.                                                                                |
| 400 - Bad Request            | This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send. |
| 401 - Not Authorized         | You are not currently allowed to view this resource until you have authorized with the web application, most commonly with a username and password.                                                                           |
| 403 - Forbidden              | You do not have permission to view this resource whether you are logged in or not.                                                                                                                                            |
| 404 - Page Not Found         | The page/resource you requested does not exist.                                                                                                                                                                               |
| 405 - Method Not Allowed     | The resource does not allow this method request, for example, you send a GET request to the resource/create-account when it was expecting a POST request instead.                                                             |
| 500 - Internal Service Error | The server has encountered some kind of error with your request that is doesn't know how to handle properly.                                                                                                                  |
| 503 - Service Unavailable    | This server cannot handle your request as it's either overloaded or down for maintenance.                                                                                                                                     |
- **Headers** - Headers are additional bits of data you can send to the web server when making requests. 
- **Common Request Headers** - These are headers that are sent from the client (usually your browser) to the server.
	- **Host**: Some web servers host multiple websites so by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the server.
	- **User-Agent**: This is your browser software and version number, telling the web server your browser software helps it format the website properly for your browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.
	- **Content-Length**: When sending data to a web server such as in a form, the content length tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.
	- **Accept-Encoding**: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.
	- **Cookie**: Data sent to the server to help remember your information.
- **Common Response Headers**: These are the headers that are returned to the client from the server after a request.
	- **Set-Cookie**: Information to store which gets sent back to the web server on each request.
	- **Cache-Control**: How long to store the content of the response in the browser's cache before it requests it again.
	- **Content-Type**: This tells the client what type of data is being returned, i.e., HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content-type header the browser then knows how to process the data.
	- **Content-Encoding**: What method has been used to compress the data to make it smaller when sending it over the internet.
- **Cookies** - Cookies are just a small piece of data that is stored on your computer. Cookies are save when you receive a "Set-Cookie" header from a web server. Then every further request you make, you'll send the cookie data back to the web server. 
![[Pasted image 20260304143203.png]]
### Burp Suite: The Basics
- Refer to [[3_Jr_Penetration_Tester]]
### OWASP API Security Top 10-1
- Open Worldwide Application Security Project (OWASP) is an non-profit and collaborative online community that aims to improve application security via a set of security principles, articles, documentation etc.
- API stands for Application Programming Interface. It is a middleware that facilitates the communication of two software components utilizing a set of protocols and definitions. In the API  context, the term 'application' refers to any software having specific functionality, and 'interface' refers to the service contract between the two apps that make communication possible via requests and responses. 
- **Vulnerability I - Broken Object Level Authorization (BOLA)** - Generally, API endpoints are utilized for a common practice of retrieving and manipulating data through object identifiers. BOLA refers to Insecure Direct Object Reference (IDOR) - which creates a scenario where the user uses the **input functionality and gets access to the resources they are not authorized to access.** 
- **Likely Impact** - The absence of controls to prevent **unauthorized object access can lead to data leakage** and, in some cases, complete account takeover.
- **Vulnerability II - Broken User Authentication (BUA)** - User authentication is the core aspect of developing any application containing sensitive data. Broken User Authentication (BUA) reflects a scenario where an API endpoint allows an attacker to access a database or acquire a higher privilege than the existing one. The primary reason behind BUA is either **invalid implementation of authentication** like using incorrect email/password queries etc., or the absence of security mechanisms like authorization headers, tokens etc.
- **Vulnerability III - Excessive Data Exposure** - Excessive data exposure occurs when applications tend to **disclose more than desired information** to the user through an API response. The application developers tend to expose all object properties (considering the generic implementations) without considering their sensitivity level.
- **Vulnerability IV - Lack of Resources & Rate Limiting** - Lack of resources and rate limiting means that **APIs do not enforce any restriction on** the frequency of clients' requested resources or the files' size, which badly affects the API server performance and leads to the DoS (Denial of Service) or non-availability of service.
- **Vulnerability V - Broken Function Level Authorization** - Broken Function Level Authorization reflects a scenario where a low privileged user (e.g., sales) bypasses system checks and gets access to **confidential data by impersonating a high privileged user (Admin).** 
### OWASP Juice Shop
- [OWASP Top Ten Web Application Security Risks | OWASP Foundation](https://owasp.org/www-project-top-ten/)
### Upload Vulnerabilities
- With unrestricted upload access to a server (and the ability to retrieve data at will), an attacker could deface or otherwise alter existing content -- up to and including injecting malicious webpages, which lead to further vulnerabilities such as XSS or CSRF.
- By uploading arbitrary files, an attacker could potentially also use the server to host and/or serve illegal content, or to leak sensistive information.
- As with any kind of hacking, enumeration is key. The more we understand about our environment, the more we're able to do with it. Looking at the source code for the page is good to see if any kind of client-side filtering is being applied.
- Scanning with a directory bruteforcer such as Gobuster is usually helpful in web attacks, and may reveal where files are being uploaded to; Gobuster is not longer installed by default on Kali, but can be installed with **sudo apt install gobuster**. 
### Pickle Rick
- 
## OWASP Top 10 (2025)
### OWASP Top 10 2025: IAAA Failures
- IAAA is a simple way to think about how users and their actions are verified on applications. Each item plays a crucial role and it isn't possible to skip a level. That means, if a previous item isn't being performed, you cannot perform the later times. The four items are:
	- **Identity** - the unique account (e.g., user ID/email) that represents a person or service.
	- **Authentication** - proving that identity (passwords, OTP, passkeys).
	- **Authorization** - what that identity is allowed to do.
	- **Accountability** - recording and alerting on who did what, when, and from where.
- **A01: Broken Access Control** - Broken Access Control happens when the server doesn't properly enforce **who can access what** on every request. A common occurrence of this is IDOR (Insecure Direct Object Reference): if changing an ID (like **?id=7 -> ?id=6**) lets you see or edit someone else's data, access control is broken.
- **A07: Authentication Failures** - Authentication Failures happen when an application can't verify or bind a user's identity. Common issues include:
	- username enumeration
	- weak/guessable passwords (no lockout/rate limits)
	- logic flaws in the login/registration flow
	- insecure session or cookie handling
- **A09: Logging & Alerting Failures** - When applications don't record or alert on security-relevant events, defenders can't detect or investigate attacks. Good logging underpins accountability (being able to prove who did what, when, and from where). In practice, failures look like missing authentication events, vague error logs, no alerting on brute-force or privilege changes, short retention, or logs stored where attackers can tamper with them.
### OWASP Top 10 2025: Application Design Flaws
- **AS02: Security Misconfigurations** - Security misconfigurations happen when systems, servers, or applications are deployed with unsafe defaults, incomplete settings, or exposed services. These are not code bugs but mistakes in how the environment, software, or network is set up. They create easy entry points for attackers.
- Even small misconfigurations can expose sensitive data, enable privilege escalation, or give attackers a foothold into the system. 
- **AS03: Software Supply Chain Failures** - Software supply chain failures happen when applications rely on components, libraries, services, or models that are compromised, outdated, or improperly verified. These weaknesses are not inherent in  your code, but rather in the software and tools you depend on. Attackers exploit these weak links to inject malicious code, bypass security, or steal sensitive data.
- **AS04: Cryptographic Failures** - Cryptographic failures happen when encryption is used incorrectly or not at all. This includes weak algorithms, hard-coded keys, poor key handling, or unencrypted sensitive data. These flaws let attackers access information that should be private.
- **AS06: Insecure Design** - Insecure design happens when flawed logic or architecture is built into a system from the start. These flaws stem from skipped threat modelling, no design requirements or reviews, or accidental errors. 
### OWASP Top 10 2025: Insecure Data Handling
- **A04: Cryptographic Failures** - Cryptographic failures happen when sensitive data isn't adequately protected due to lack of encryption, faulty implementation, or insufficient security measures. This includes storing passwords without hashing, using outdated or weak algorithms (such as MD5, SHA1, or DES), exposing encryption keys, or failing to secure data during transmission.
- **A05: Injection** - Injection occurs when an application takes user input and mishandles it. Instead of processing the input securely, the application passes it directly into a system that can execute commands or queriers, such as database, a shell, a templating engine, or API. 
- The following are some classic examples of injection:
	- SQL Injection
	- Command Injection
	- API Prompts
	- Server Side Template Inejection (SSTI)
- **A08: Software or Data Integrity Failures** - Software or Data Integrity Failures occur when an application relies on code, updates, or data it assumes are safe, without verifying their authenticity, integrity, or origin. This includes trusting software updates without verification, loading scripts or configuration files from untrusted sources, failing to validate data that impacts application logic, or accepting data such as binaries, templates, or JSON files without confirming whether it has been altered.



